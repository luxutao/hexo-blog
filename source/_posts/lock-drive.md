---
title:      "禁用Linux Desktop下的设备"
cover:      "https://image.animekid.cn/images/2019/02/02/59e86d5378ae0bda208a95bb1c477783.md.png"
date:       "2019-02-01 14:14:37"
tags:
    - Linux Desktop
---

```bash
PAF4:~$ xinput list      ##显示设备的ID号
⎡ Virtual core pointer                    	id=2	[master pointer  (3)]
⎜   ↳ Virtual core XTEST pointer              	id=4	[slave  pointer  (2)]
⎜   ↳ SynPS/2 Synaptics TouchPad              	id=14	[slave  pointer  (2)]			####id=14代表的就是笔记本的触摸板
⎜   ↳ USB OPTICAL MOUSE                       	id=15	[slave  pointer  (2)]
⎜   ↳ USB OPTICAL MOUSE                       	id=16	[slave  pointer  (2)]
⎜   ↳ Gaming KB  Gaming KB                    	id=10	[slave  pointer  (2)]
⎣ Virtual core keyboard                   	id=3	[master keyboard (2)]
    ↳ Virtual core XTEST keyboard             	id=5	[slave  keyboard (3)]
    ↳ Power Button                            	id=6	[slave  keyboard (3)]
    ↳ Video Bus                               	id=7	[slave  keyboard (3)]
    ↳ Video Bus                               	id=8	[slave  keyboard (3)]
    ↳ Sleep Button                            	id=9	[slave  keyboard (3)]
    ↳ USB 2.0 Camera                          	id=12	[slave  keyboard (3)]
    ↳ Gaming KB  Gaming KB                    	id=11	[slave  keyboard (3)]
    ↳ AT Translated Set 2 keyboard            	id=13	[slave  keyboard (3)]			####id=13代表的就是笔记本的内置键盘
PAF4:~$ xinput set-prop 13 "Device Enabled" 0							####关闭键盘
PAF4:~$ xinput set-prop 13 "Device Enabled" 1							####开启键盘
```
