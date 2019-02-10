# UiO-CTF: pizzareverse3

**Category:** Reverse Engineering

**Description:**

If you need a flag try to capture the one that is already on the Moon.

## Write-up

Found nothing too interesting with basic analysis, so let's open it with Radare2.

`r2 -d pizzareverse3`


`aaa` - Analyze all flags starting with sym. and autoname functions after aa.

`afl` - list functions

`s sym.main` - Seek to current address

We can see that the program will compare the userinput with the string "Neil Armstrong", so this is the first input we will need.
![](/uio/images/img1.png)

![](/uio/images/img2.png)

The string "Houston" is loaded into `0x556829914098`:
```
lea rax, qword [0x556829713bb0]           ; The string “Houston” is loaded into rax
mov qword [0x556829914098], rax           ; Moved into 0x556829914098
```

Then we can see that the `0x556829914098` address is loaded into `rcx`and to `rax`, and "%s %s" is loaded into `rsi`.

So when the `sprintf` function is called, it will look something like this: `sprintf(local_80h, "%s %s", "Houston", "Houston")`, so the complete string will be "Houston Houston".

This can also be seen by setting a breakpoint at the `strcmp` function call. The string we are comparing the user input with is loaded into `rdx`.

```
:> ps @ rdx
Houston Houston
```
We can now connect to the server and retrieve our flag.
```
$ nc 158.36.185.227 6003

 What's your name?
Neil Armstrong

 What's your message?
Houston Houston

 Ok Neil, here's the flag. Place it on the moon!
UiO-CTF{Was_that_a_Challange(r)_at_all?}
```