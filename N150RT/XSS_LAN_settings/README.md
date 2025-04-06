# TOTOLINK N150RT XSS Vulnerability (Static DHCP Setup)
## Description

TOTOLINK N150RT V2_Firmware V3.4.0-B20190525 contains a Store Cross-site scripting (XSS) vulnerability in `Static DHCP Setup` under the `LAN Settings` Page.

## TOTOLINK N150RT version information

- Device：TOTOLINK N150RT
- Firmware Version：N150RT V2_Firmware V3.4.0-B20190525
- Manufacturer's website information：https://www.totolink.net/ 
- Firmware download address：https://www.totolink.net/home/menu/detail/menu_listtpl/download/id/153/ids/36.html

## Vulnerability information

In the settings under the `LAN Settin` page, there is an page called `Static DHCP Setup`. There is a Store Cross-site scripting vulnerability in `Comment` input box. 

Firstly, we click the `Set Static DHCP` button on the LAN Setting page.

![1.png](imgs/1.png)

Then we can see the `Static DHCP Setup` page.

![2.png](imgs/2.png)

The `Static DHCP Setup` page will check the value of comment, but it does not check on the server, So we use BurpSuite to bypass.

We fill in information as shown in the figure below. Then click the `Send` button to send the request.

![3.png](imgs/3.png)

Once the request is sent, we refresh the `Static DHCP Setup` page.Then the web site will execute the javascript we just inputted. This is a Store Cross-site scripting vulnerability, if someone else visits the page, the javascript will also be executed.

![4.png](imgs/4.png)

