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

|  ID   |        Firmware Version         | newly discovered |               URI               |     parameter     |      CVE ID       | CVSS3.x |   vul_type   | REAL Crash to device |
| :---: | :-----------------------------: | :--------------: | :-----------------------------: | :---------------: | :---------------: | :-----: | :----------: | :------------------: |
| **1** | **Tenda AC8 V4.0 V16.03.33.05** |      **1**       |   **`/goform/SetSysTimeCfg`**   |     **time**      | **CVE-2025-5798** | **8.8** | **Overflow** |        **1**         |
| **2** | **Tenda AC8 V4.0 V16.03.33.05** |      **1**       |   **`/goform/WifiExtraSet`**    | **wpapsk_crypto** | **CVE-2025-5799** | **8.8** | **Overflow** |        **1**         |
|   3   |   Tenda AC8 V4.0 V16.03.33.05   |        0         |     `/goform/openSchedWifi`     |   schedEndTime    |  CVE-2024-57703   |   9.8   |   Overflow   |          1           |
|   4   |   Tenda AC8 V4.0 V16.03.33.05   |        0         |     `/goform/openSchedWifi`     |  schedStartTime   |  CVE-2024-57703   |   9.8   |   Overflow   |          1           |
|   5   |   Tenda AC8 V4.0 V16.03.33.05   |        0         |     `/goform/PowerSaveSet`      |       time        |  CVE-2023-40893   |   9.8   |   Overflow   |          1           |
|   6   |   Tenda AC8 V4.0 V16.03.33.05   |        0         | `/goform/saveParentControlInfo` |     deviceId      |  CVE-2023-33671   |   9.8   |   Overflow   |          1           |
|   7   |   Tenda AC8 V4.0 V16.03.33.05   |        0         | `/goform/saveParentControlInfo` |       time        |  CVE-2024-10123   |   8.8   |   Overflow   |          1           |
|   8   |   Tenda AC8 V4.0 V16.03.33.05   |                  | `/goform/saveParentControlInfo` |       urls        |  no CVE assigned  |         |   Overflow   |          1           |
|   9   |   Tenda AC8 V4.0 V16.03.33.05   |        0         |    `/goform/SetFirewallCfg`     |    firewallEn     |  CVE-2023-40891   |   9.8   |   Overflow   |          1           |
|  10   |   Tenda AC8 V4.0 V16.03.33.05   |        0         |     `/goform/SetIpMacBind`      |       list        |   CVE-2025-1853   |   9.8   |   Overflow   |          1           |
|  11   |   Tenda AC8 V4.0 V16.03.33.05   |        0         |   `/goform/SetStaticRouteCfg`   |       list        |  CVE-2023-40894   |   9.8   |   Overflow   |          1           |
|  12   |   Tenda AC8 V4.0 V16.03.33.05   |        0         |     `/goform/SetSysTimeCfg`     |     timeZone      |  CVE-2023-40898   |   9.8   |   Overflow   |          1           |
|  13   |   Tenda AC8 V4.0 V16.03.33.05   |        0         |  `/goform/SetVirtualServerCfg`  |       list        |  CVE-2023-40895   |   9.8   |   Overflow   |          1           |


Additional reports will be released after the corresponding vulnerabilities have been patched by vendors.
