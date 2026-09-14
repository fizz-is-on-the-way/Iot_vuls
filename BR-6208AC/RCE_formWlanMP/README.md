# EDIMAX BR-6208AC /goform/formWlanMP command injection Vulnerability 
## Description

EDIMAX BR-6208AC Firmware BR-6208AC_1.32 was discovered to contain a remote code execution (RCE) vulnerability via the `readE2P` parameter in the `/goform/formWlanMP`. 

## EDIMAX BR-6208AC version information

- Device：EDIMAX BR-6208AC
- Firmware Version：BR-6208AC_1.32
- Manufacturer's website information：https://www.edimax.com/edimax/global/
- Firmware download address：https://www.edimax.com/edimax/download/download/data/edimax/global/download/home_legacy_wireless_routers/br-6208ac

## Vulnerability information

We can see that the  `v17` variable receives `readE2P` parameter from a POST request. The statement `sprintf(s, "/bin/rftest_old.sh %s ... %s", Var... v17, v25, v23);` will pass `v17` to variable `s`. However, since the user can control the input of `readE2P`, the statement `system(s);` in line 155  can cause a command injection vulnerability. This vulnerability allows an attacker to execute arbitrary commands through the `readE2P` parameter.

![1.png](imgs/1.png)

We use qemu-system to run the firmware.Then type `ls` command on the terminal of firmware.

![2.png](imgs/2.png)

We use BurpSuite to attck. We fill in information as shown in the figure below. And click the "Send" button. 

The purpose of `echo a > /a.txt`command is to output `a` to file `/a.txt` .

![3.png](imgs/3.png)

Then type `ls` and `cat /a.txt`  command on the terminal of firmware. We can see that `a.txt` was created and the the content of file `a.txt` is `a`.

![4.png](imgs/4.png)

## Vulnerability Assessment Score
CVSS Score: 9.8
Vector String： CVSS:4.0/AV:N/AC:L/AT:N/PR:N/UI:N/VC:H/VI:H/VA:H/SC:N/SI:N/SA:N
Reason: This vulnerability is a Pre-authentication Remote Code Execution vulnerability.It can execute any command.