# DLINK DAP-2695 XSS Vulnerability (MAC Bypass Settings)
## Description

DLINK DAP-2695_fw_reva_120b36r137_ALL_en_20210528 contains a Store Cross-site scripting (XSS) vulnerability in the `MAC Bypass Settings` Page.

## DLINK DAP-2695 version information

- Device：DLINK DAP-2695
- Firmware Version：DAP-2695_fw_reva_120b36r137_ALL_en_20210528
- Manufacturer's website information：http://www.dlink.com.cn/
- Firmware download address：https://ftp.dlink.de/dap/dap-2695/driver_software/DAP-2695_fw_reva_120b36r137_ALL_en_20210528.zip

## Vulnerability information

In the `MAC Bypass Settings` page, there is a Store Cross-site scripting vulnerability in `MAC Address`. 

The `MAC Bypass Settings` page will check the value of `MAC Address`, but it does not check on the server, So we use BurpSuite to bypass. 

We fill in information as shown in the figure below.And Turnning on the interception function of `BurpSuite`, then click the `Add` button on the page.

![1.png](imgs/1.png)

Once the request is sent, `BurpSuite` will intercept the packet. We change the value of `f_mac=` to the poc `<svg/onload=alert()>`. 

First click the `Apply changes` button on `BurpSuite`, then click `Forward all` button to send the request, and finally click `Intercept on` to turn off the interception function.

![2.png](imgs/2.png)

Once the request is sent, we refresh the `MAC Bypass Settings` page.Then the web site will execute the javascript we just inputted. This is a Store Cross-site scripting vulnerability, if someone else visits the page, the javascript will also be executed.

![3.png](imgs/3.png)