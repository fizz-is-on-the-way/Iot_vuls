# EDIMAX BR-6208AC /goform/setWAN command injection Vulnerability 
## Description

EDIMAX BR-6208AC Firmware BR-6208AC_1.32 was discovered to contain a remote code execution (RCE) vulnerability via the `pptpUserName` parameter in the `/goform/setWAN `. 

## EDIMAX BR-6208AC version information

- Device：EDIMAX BR-6208AC
- Firmware Version：BR-6208AC_1.32
- Manufacturer's website information：https://www.edimax.com/edimax/global/
- Firmware download address：https://www.edimax.com/edimax/download/download/data/edimax/global/download/home_legacy_wireless_routers/br-6208ac

## Vulnerability information

We can see that the  `v16` variable receives `pptpUserName` parameter from a POST request. The statement `strcpy(v54, v16);` in line 129 will pass `v16` to variable `v54`.The statement `sprintf(v55, "echo %s > /tmp/UserName", v54);` in line 141 will pass `v54` to variable `v55`.However, since the user can control the input of `pptpUserName`, the statement `system(v55);` in line 142  can cause a command injection vulnerability. This vulnerability allows an attacker to execute arbitrary commands through the `pptpUserName` parameter.

![1.png](imgs/1.png)

We use qemu-system to run the firmware.Then type `ls` command on the terminal of firmware.

![2.png](imgs/2.png)

We use BurpSuite to attck. We fill in information as shown in the figure below. And click the "Send" button. 

The purpose of `echo zxcv123 > /1.txt`command is to output `zxcv123` to file `/1.txt` .

![3.png](imgs/3.png)

Then type `ls` and `cat /1.txt`  command on the terminal of firmware. We can see that `1.txt` was created and the the content of file `1.txt` is `zxcv123`.

![4.png](imgs/4.png)

## Vulnerability Assessment Score
CVSS Score: 9.8
Vector String： CVSS:4.0/AV:N/AC:L/AT:N/PR:N/UI:N/VC:H/VI:H/VA:H/SC:N/SI:N/SA:N
Reason: This vulnerability is a Pre-authentication Remote Code Execution vulnerability.It can execute any command.