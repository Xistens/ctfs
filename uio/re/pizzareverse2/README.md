# UiO-CTF: pizzareverse2

**Category:** Reverse Engineering

**Description:**

This file contains too much strawberries. Can you find the flag inside?

## Write-up

Fairly simple challenge. All we need to do is:

`$ strings pizzareverse2`

Among a few unintelligible strings we will find some base64 encoded strings:

```
TGV0IG1lIHRha2UgeW91IGRvd24=
J0NhdXNlIEknbSBnb2luZyB0byBTdHJhd2JlcnJ5IEZpZWxkcw==
Tm90aGluZyBpcyByZWFs
QW5kIG5vdGhpbmcgdG8gZ2V0IGh1bmcgYWJvdXQ=
U3RyYXdiZXJyeSBGaWVsZHMgZm9yZXZlcg==
TGl2aW5nIGlzIGVhc3kgd2l0aCBleWVzIGNsb3NlZA==
TWlzdW5kZXJzdGFuZGluZyBhbGwgeW91IHNlZQ==
VWlPLUNURns2NFN0cmF3YmVycnlfYmFzZWRfZW5jb2RlfQ==
SXQncyBnZXR0aW5nIGhhcmQgdG8gYmUgc29tZW9uZQ==
QnV0IGl0IGFsbCB3b3JrcyBvdXQ=
SXQgZG9lc24ndCBtYXR0ZXIgbXVjaCB0byBtZQ==
```

Base64 decode and we will find the flag:

`UiO-CTF{64Strawberry_based_encode}`