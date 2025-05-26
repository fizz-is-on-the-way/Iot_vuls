# TOTOLINK X2000R XSS Vulnerability (URL Filtering)
## Description

TOTOLINK X2000R_Firmware V1.0.0-B20230726.1108 contains a Store Cross-site scripting (XSS) vulnerability in `URL Filtering` under the `Firewall` Page.

## TOTOLINK X2000R version information

- Device：TOTOLINK X2000R
- Firmware Version：X2000R_Firmware V1.0.0-B20230726.1108
- Manufacturer's website information：https://www.totolink.net/ 
- Firmware download address：https://www.totolink.net/home/menu/detail/menu_listtpl/download/id/242/ids/36.html

## Vulnerability information

In the settings under the `Firewall` page, there is an option called `URL Filtering`. There is a Store Cross-site scripting vulnerability in `URL Address`  box. 

![1.png](imgs/1.png)

The `URL Filtering` page will check the value of `URL Address`, but it does not check on the server, So we use `BurpSuite` to bypass. 

We fill in information as shown in the figure below. Then click the `Send` button to send the request.

![2.png](imgs/2.png)

Once the request is sent, we refresh the `URL Filtering` page.Then the web site will execute the javascript we just inputted. This is a Store Cross-site scripting vulnerability, if someone else visits the page, the javascript will also be executed.

![3.png](imgs/3.png)

