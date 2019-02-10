# UiO-CTF: pizzareverse5

**Category:** Reverse Engineering

**Description:**

Why don't you ask Alan Alexander Milne about the flag? That's inside the binary.

## Write-up
All we need to do is:

`$ strings pizzareverse5`

Among a few unintelligible strings we will find a ROT13 encoded string:

`uggc://HvB-PGS{EBG_Pvcure_EBG}`

ROT13:
`http://UiO-CTF{ROT_Cipher_ROT}`