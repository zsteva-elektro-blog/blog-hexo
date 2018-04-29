---
title: gdb stm32 peek & poke
date: 2018-04-29 11:20:56
tags: stm32,gdb,blue_pill
---

Pošto smo uspešno {% post_link stlink-konektovanje povezali razvojnu pločicu %}, da probamo da upalimo LED diodu na pločici.

{% asset_img stm32_led.jpg %}

Kod je preuzet iz [https://github.com/satoshinm/pill_blink](https://github.com/satoshinm/pill_blink) bare-metal/pill_blink.c

Pošto nam st-util prepoznaje pločicu, povezaćemo se gdb-om.

```
$ arm-none-eabi-gdb -ex 'target extended-remote localhost:4242'
GNU gdb (GDB) 8.1
Copyright (C) 2018 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.  Type "show copying"
and "show warranty" for details.
This GDB was configured as "--host=x86_64-pc-linux-gnu --target=arm-none-eabi".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<http://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
<http://www.gnu.org/software/gdb/documentation/>.
For help, type "help".
Type "apropos word" to search for commands related to "word".
Remote debugging using localhost:4242
warning: No executable has been specified and target does not support
determining executable automatically.  Try using the "file" command.
0xfffffffe in ?? ()
(gdb) 
```

Zatim uraditi potrebnu inicijalizaciju, u ovom trenutku nemam pojma šta ovo tačno radi, prepisano je iz pill_blink primera.

```
set *(unsigned int *)0x40021018 |= (1 << 4)
set *(unsigned int *)0x40011004 |= (0x00 << (((13 - 8) * 4) + 2))
set *(unsigned int *)0x40011004 |= (0x02 << ((13 - 8) * 4))
```

Po ovome LED na pločici ce početi da svetli. Da bi ga ugasili treba da izvšimo:

```
set *(unsigned int *)0x40011010 = (1 << 13)
```

I potom da upalimo:

```
set *(unsigned int *)0x40011014 = (1 << 13)
```

Kao u stara dobra vremena 8bitnih računara, osim što sve deluje malo komplikovanije.




