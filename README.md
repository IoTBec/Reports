# IoTBec

This repository contains partial results and related materials from the IoTBec framework evaluation.

## 1. Test Devices

We evaluated IoTBec on a variety of IoT devices from major vendors, including routers, range extenders, and switches.  
Detailed information on all devices in our experiments can be found in [device_under_test.md](https://github.com/IoTBec/Surveys/blob/main/device_under_test.md).

## 2. Vulnerability Reports

IoTBec discovered a significant number of CRITICAL- and HIGH-severity vulnerabilities during testing, some of which have been assigned CVE IDs. For security reasons, we only disclose vulnerability reports for issues that have been confirmed as fixed in the latest product versions. At present, our findings are still being processed and consolidated; we are releasing **13** out of the **14** vulnerabilities identified in Tenda AC8 V4.0 V16.03.33.05, as these have been fixed in the latest Tenda AC8 V4.0 V16.03.34.09 firmware.

Available Reports:
- [Tenda_AC8_goform_SetSysTimeCfg](https://github.com/IoTBec/Reports/blob/main/Tenda/AC8/goform_SetSysTimeCfg.md)
- [Tenda_AC9_goform_WifiExtraSet](https://github.com/IoTBec/Reports/blob/main/Tenda/AC8/goform_WifiExtraSet.md)

|  ID  |      Firmware Version       |               URI               |   parameter    | vul_type | REAL Crash to device |     CVE ID     | CVSS3.x | newly discovered |
| :--: | :-------------------------: | :-----------------------------: | :------------: | :------: | :------------------: | :------------: | :-----: | :--------------: |
**|  1  | Tenda AC8 V4.0 V16.03.33.05 |     `/goform/SetSysTimeCfg`     |      time      | Overflow |          1           | CVE-2025-5798  |   8.8   |        1         |**
**|  2  | Tenda AC8 V4.0 V16.03.33.05 |     `/goform/WifiExtraSet`      | wpapsk_crypto  | Overflow |          1           | CVE-2025-5799  |   8.8   |        1         |**
|  3   | Tenda AC8 V4.0 V16.03.33.05 |     `/goform/openSchedWifi`     |  schedEndTime  | Overflow |          1           | CVE-2024-57703 |   9.8   |        0         |
|  4   | Tenda AC8 V4.0 V16.03.33.05 |     `/goform/openSchedWifi`     | schedStartTime | Overflow |          1           | CVE-2024-57703 |   9.8   |        0         |
|  5   | Tenda AC8 V4.0 V16.03.33.05 |     `/goform/PowerSaveSet`      |      time      | Overflow |          1           | CVE-2023-40893 |   9.8   |        0         |
|  6   | Tenda AC8 V4.0 V16.03.33.05 | `/goform/saveParentControlInfo` |    deviceId    | Overflow |          1           | CVE-2023-33671 |   9.8   |        0         |
|  7   | Tenda AC8 V4.0 V16.03.33.05 | `/goform/saveParentControlInfo` |      time      | Overflow |          1           | CVE-2024-10123 |   8.8   |        0         |
|  8   | Tenda AC8 V4.0 V16.03.33.05 | `/goform/saveParentControlInfo` |      urls      | Overflow |          1           | no CVE assigned|         |                  |
|  9   | Tenda AC8 V4.0 V16.03.33.05 |    `/goform/SetFirewallCfg`     |   firewallEn   | Overflow |          1           | CVE-2023-40891 |   9.8   |        0         |
|  10   | Tenda AC8 V4.0 V16.03.33.05 |     `/goform/SetIpMacBind`      |      list      | Overflow |          1           | CVE-2025-1853  |   9.8   |        0         |
|  11  | Tenda AC8 V4.0 V16.03.33.05 |   `/goform/SetStaticRouteCfg`   |      list      | Overflow |          1           | CVE-2023-40894 |   9.8   |        0         |
|  12  | Tenda AC8 V4.0 V16.03.33.05 |     `/goform/SetSysTimeCfg`     |    timeZone    | Overflow |          1           | CVE-2023-40898 |   9.8   |        0         |
|  13  | Tenda AC8 V4.0 V16.03.33.05 |  `/goform/SetVirtualServerCfg`  |      list      | Overflow |          1           | CVE-2023-40895 |   9.8   |        0         |


Additional reports will be released after the corresponding vulnerabilities have been patched by vendors.
