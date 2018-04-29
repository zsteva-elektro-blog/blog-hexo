---
title: stlink konektovanje
date: 2018-04-29 11:13:38
tags: stm32,stlink,blue_pill
---

Konektovanje stlink adaptera i stm32 plocice.

{% asset_img stm32-stlink-wiring.jpg stlink i stm32 %}

Arch linux instaliranje potrebnih paketa

```shell

pacman -S arm-none-eabi-gcc arm-none-eabi-gdb arm-none-eabi-binutils arm-none-eabi-newlib stlink

```

Po povezivanju stlink adaptera u dmesg se pojavi:

```
usb 1-1.1: new full-speed USB device number 14 using ehci-pci
usb 1-1.1: New USB device found, idVendor=0483, idProduct=3748
usb 1-1.1: New USB device strings: Mfr=1, Product=2, SerialNumber=3
usb 1-1.1: Product: STM32 STLink
usb 1-1.1: Manufacturer: STMicroelectronics
usb 1-1.1: SerialNumber: HÿjexUUE g
```

A st-util prepozna razvojnu pločicu sugerušići da smo sve lepo povezali. Ako je Chip ID 0 znači da nije prepoznao pločicu.

```
$ st-util 
st-util 1.5.0
2018-04-29T11:17:44 INFO common.c: Loading device parameters....
2018-04-29T11:17:44 INFO common.c: Device connected is: F1 Medium-density device, id 0x20036410
2018-04-29T11:17:44 INFO common.c: SRAM size: 0x5000 bytes (20 KiB), Flash: 0x20000 bytes (128 KiB) in pages of 1024 bytes
2018-04-29T11:17:44 INFO gdb-server.c: Chip ID is 00000410, Core ID is  1ba01477.
2018-04-29T11:17:44 INFO gdb-server.c: Listening at *:4242...
```


 
