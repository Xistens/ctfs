# UiO-CTF: pizzareverse4

**Category:** Reverse Engineering

**Description:**

The only challange here is to find the magic word.

## Write-up

Found nothing to interesting with basic analysis, so let's open it with Radare2.

`r2 -d pizzareverse3`


`aaa` - Analyze all flags starting with sym. and autoname functions after aa.

`afl` - list functions

`s sym.main` - Seek to current address

The string "George Harrison" is loaded into the `rax`register, then moved into `0x55a62fdde0a8`.
![](/uio/images/img3.png)

![](/uio/images/img4.png)
The address "`0x55a62fdde0a8`" containing the string "George Harrison" is loaded into `rdx` and `local_14h` is loaded into `ecx` which stores the hex value 0x95 (149 in decimal) then "%s%d" is loaded into `rsi`, so when `sprintf` is called it will look like this: `sprintf(local_40h, "%s%d", "George Harrison", 0x95)` which will become the string "George Harrison149".

We can take a look at local_40h (rbp-0x40) after sprintf() to confirm this:
![](/uio/images/img5.png)

Can also see this easily by adding a breakpoint at the strcmp call and inspect rsi:
```
:> ps @ rsi
George Harrison149
```

Connect to the server and retrieve the flag:
```
$ nc 158.36.185.227 6004

 What's the magic word?
George Harrison149
pizzareverse5 UiO-CTF{L1v4rp00l_Pl4as4_Pl4as4_M4}
```