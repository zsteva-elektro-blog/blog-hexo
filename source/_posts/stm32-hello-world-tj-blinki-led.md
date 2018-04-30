---
title: stm32 hello world tj blinki led
date: 2018-04-30 10:17:31
tags:
 - blue_pill
 - stm32
 - hello_world
 - blink_led
 - gdb
---

Blink led, ili hello world. Kod je pozajmljen sa [https://github.com/satoshinm/pill_blink/tree/master/bare-metal](https://github.com/satoshinm/pill_blink/tree/master/bare-metal). Ali je malo modifikovan kako bi nam bolje poslužio.

Kloniraćemo repozitori [https://github.com/zsteva-elektro-blog/blue_pill_blink_bare_metal](https://github.com/zsteva-elektro-blog/blue_pill_blink_bare_metal), zatim pokrenuti kompajliranje.

```
git clone https://github.com/zsteva-elektro-blog/blue_pill_blink_bare_metal
cd blue_pill_blink_bare_metal/bare-metal
make
```

U jednom prozoru pokrenemo st-util. I potom u prozoru sa projektom možemo gdb-om da se nakačimo.

{% asset_img stm32_blinki_gdb.png %}

Znači prvo pokrenemo gdb

```
arm-none-eabi-gdb pill_blink.elf
```

Zatim u okviru gdba redom komande rade: konektujemo se na na hardware preko st-util, stopiramo uredjaj, ucitamo program u uredjaj, resetujemo uredjaj i konacno sa run pokrenemo program.

```
target extended localhost:4242
monitor reset halt
load
monitor reset init
run
```

Rezultat treba bude LED dionda koja blinka. Da svaki put ne bi kucali sve ovo, komande su snimljene u **gdbinit** fajl i napravljena prečica u **Makefile**, tako da je dovoljno uraditi

```
make gdb
```

I samo nam preostaje da uradimo **run**.


