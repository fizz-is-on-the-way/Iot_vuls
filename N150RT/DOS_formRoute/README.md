# TOTOLINK N150RT buffer overflow Vulnerability 
## Description

TOTOLINK N150RT V2_Firmware V3.4.0-B20190525 contains a buffer overflow vulnerability in /boafrm/formRoute  `metric` parameter.

## TOTOLINK N150RT version information

- Device：TOTOLINK N150RT
- Firmware Version：N150RT V2_Firmware V3.4.0-B20190525
- Manufacturer's website information：https://www.totolink.net/ 
- Firmware download address：https://www.totolink.net/home/menu/detail/menu_listtpl/download/id/153/ids/36.html

## Vulnerability information

In the settings under the `Network` page, there is an option called `Static Route`. 

![1.png](imgs/1.png)

 We use `ping` command to check if the device is alive. We can see the device is alive now.

![2.png](imgs/2.png)

We use BurpSuite to attck. We fill in information as shown in the figure below. And click the `Send` button. 

![3.png](imgs/3.png)

Once we send the post request and use `ping` command to check if the device is alive, we can see that now the device is dead.

![4.png](imgs/4.png)

The browser cannot access the service.

![5.png](imgs/5.png)