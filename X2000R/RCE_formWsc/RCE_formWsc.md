# TOTOLINK X2000R command injection Vulnerability 
## Description

TOTOLINK X2000R_Firmware V1.0.0-B20230726.1108 was discovered to contain a remote code execution (RCE) vulnerability via the `peerRptPin` parameter in the /boafrm/formWsc. 

## TOTOLINK X2000R version information

- Device：TOTOLINK X2000R
- Firmware Version：X2000R_Firmware V1.0.0-B20230726.1108
- Manufacturer's website information：https://www.totolink.net/ 
- Firmware download address：https://www.totolink.net/home/menu/detail/menu_listtpl/download/id/242/ids/36.html

## Vulnerability information

We can see that the  `v52` variable receives `peerRptPin` parameter from a POST request. The statement `sprintf(v64, 200, "iwpriv wlan%d-vxd set_mib pin=%s", wlan_idx, v52);` in line 502 will pass the value of `v52` variable to `v64` variable.However, since the user can control the input of `peerRptPin`, the statement `system(v64);` in line 504 can cause a command injection vulnerability. This vulnerability allows an attacker to execute arbitrary commands through the `peerRptPin` parameter.

![1.png](imgs/1.png)

We use qemu-system to run the firmware.Then type `ls` command on the terminal of firmware.

![2.png](imgs/2.png)

We use BurpSuite to attck. We fill in information as shown in the figure below. And click the "Send" button. 

The purpose of `cat /etc/passwd > /b.txt`command is to output the content of file /etc/passwd to file /b.txt .

![3.png](imgs/3.png)

Then type `ls` , `cat /b.txt` and `cat /etc/passwd` command on the terminal of firmware. We can see the the content of file b.txt is the same as /etc/passwd.

![4.png](imgs/4.png)
