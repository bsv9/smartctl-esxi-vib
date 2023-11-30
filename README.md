# smartctl for esxi7/8

This solution does not work when secure boot is enabled

1. Download [smartctl-7.4-5530.x86_64.vib](https://github.com/bsv9/smartctl-esxi/raw/main/smartctl-7.4-5530.x86_64.vib)

2.  Copy the VIB to the /tmp/ directory of an ESXi host
3.  SSH to the ESXi host
4.  Set the VIB acceptance level to CommunitySupported
 ```
 esxcli software acceptance set --level=CommunitySupported
 ````
5.  Install the package (Maintenance Mode or Reboot is not required)
```
esxcli software vib install -v /tmp/smartctl-7.4-5530.x86_64.vib
```
6. Enjoy
```
[root@esxi-host:~] uname -a
VMkernel esxi02-waw1 8.0.2 #1 SMP Release build-22380479 Sep  4 2023 15:00:49 x86_64 x86_64 x86_64 ESXi
[root@esxi-host:~] /opt/smartmontools/smartctl -s on -d sat,auto -A /dev/disks/t10.ATA_____HGST_HUS726T6TALE6L1____________________V9J0UN7M____________
smartctl 7.4 2023-08-01 r5530 [x86_64-linux-8.0.2] (local build)
Copyright (C) 2002-23, Bruce Allen, Christian Franke, www.smartmontools.org

=== START OF ENABLE/DISABLE COMMANDS SECTION ===
SMART Enabled.

=== START OF READ SMART DATA SECTION ===
SMART Attributes Data Structure revision number: 16
Vendor Specific SMART Attributes with Thresholds:
ID# ATTRIBUTE_NAME          FLAG     VALUE WORST THRESH TYPE      UPDATED  WHEN_FAILED RAW_VALUE
  1 Raw_Read_Error_Rate     0x000b   100   100   016    Pre-fail  Always       -       0
  2 Throughput_Performance  0x0005   132   132   054    Pre-fail  Offline      -       96
  3 Spin_Up_Time            0x0007   188   188   024    Pre-fail  Always       -       324 (Average 316)
  4 Start_Stop_Count        0x0012   100   100   000    Old_age   Always       -       105
  5 Reallocated_Sector_Ct   0x0033   100   100   005    Pre-fail  Always       -       0
  7 Seek_Error_Rate         0x000b   100   100   067    Pre-fail  Always       -       0
  8 Seek_Time_Performance   0x0005   128   128   020    Pre-fail  Offline      -       18
  9 Power_On_Hours          0x0012   098   098   000    Old_age   Always       -       15474
 10 Spin_Retry_Count        0x0013   100   100   060    Pre-fail  Always       -       0
 12 Power_Cycle_Count       0x0032   100   100   000    Old_age   Always       -       105
192 Power-Off_Retract_Count 0x0032   100   100   000    Old_age   Always       -       730
193 Load_Cycle_Count        0x0012   100   100   000    Old_age   Always       -       730
194 Temperature_Celsius     0x0002   176   176   000    Old_age   Always       -       34 (Min/Max 18/54)
196 Reallocated_Event_Count 0x0032   100   100   000    Old_age   Always       -       0
197 Current_Pending_Sector  0x0022   100   100   000    Old_age   Always       -       0
198 Offline_Uncorrectable   0x0008   100   100   000    Old_age   Offline      -       0
199 UDMA_CRC_Error_Count    0x000a   200   200   000    Old_age   Always       -       0
```
