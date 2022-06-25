# New Caesar
Cryptography, 60 points

## Description:
> We found a brand new type of encryption, can you break the secret code?

```
kjlijdliljhdjdhfkfkhhjkkhhkihlhnhghekfhmhjhkhfhekfkkkjkghghjhlhghmhhhfkikfkfhm
```

## Solution:

We have python script: `new_caesar.py`
'''python
import string

LOWERCASE_OFFSET = ord("a")
ALPHABET = string.ascii_lowercase[:16]

def b16_encode(plain):
        enc = ""
        for c in plain:
                binary = "{0:08b}".format(ord(c))
                enc += ALPHABET[int(binary[:4], 2)]
                enc += ALPHABET[int(binary[4:], 2)]
        return enc

def shift(c, k):
        t1 = ord(c) - LOWERCASE_OFFSET
        t2 = ord(k) - LOWERCASE_OFFSET
        return ALPHABET[(t1 + t2) % len(ALPHABET)]

flag = "redacted"
key = "redacted"
assert all([k in ALPHABET for k in key])
assert len(key) == 1

b16 = b16_encode(flag)
enc = ""
for i, c in enumerate(b16):
        enc += shift(c, key[i % len(key)])
print(enc)
```
Based on this given script, we have to write some code to decrypt secret code to get flag.
Function to decode `b16_encode`:
```python
def b16_decode(plain):
    dec = ""

    for i in range(0, len(plain), 2):
        i1 = ALPHABET.index(plain[i])
        i2 = ALPHABET.index(plain[i+1])
        b1 = bin(i1)[2:].zfill(4)
        b2 = bin(i2)[2:].zfill(4)
        b = b1 + b2
        d = int(b, 2)
    
        dec += chr(d)
    return dec
```
And `shift`:
```python
def unshift(c, k):
    t1 = ord(c) - LOWERCASE_OFFSET
    t2 = ord(k) - LOWERCASE_OFFSET
    return ALPHABET[(t1 - t2) % 16]
```
Now we need key to decrypt secret code.
Look at those lines:
```python
assert all([k in ALPHABET for k in key])
assert len(key) == 1
```
They told us that `key` is one of some characters in `ALPHABET`.
We will take care of all possible cases of the key, then look at all found flags.
To do so, we use this:
```python
import string

LOWERCASE_OFFSET = ord("a")
ALPHABET = string.ascii_lowercase[:16]

enc = "kjlijdliljhdjdhfkfkhhjkkhhkihlhnhghekfhmhjhkhfhekfkkkjkghghjhlhghmhhhfkikfkfhm"

def b16_decode(plain):
    dec = ""

    for i in range(0, len(plain), 2):
        i1 = ALPHABET.index(plain[i])
        i2 = ALPHABET.index(plain[i+1])
        b1 = bin(i1)[2:].zfill(4)
        b2 = bin(i2)[2:].zfill(4)
        b = b1 + b2
        d = int(b, 2)
    
        dec += chr(d)
    return dec

def unshift(c, k):
    t1 = ord(c) - LOWERCASE_OFFSET
    t2 = ord(k) - LOWERCASE_OFFSET
    return ALPHABET[(t1 - t2) % 16]

for key in ALPHABET:
    dec = ""
    for i, c in enumerate(enc):
        dec += unshift(c, key)
    print(b16_decode(dec))
```
And the result:
```console
┌──(kali㉿kali)-[~/PICOCTF]
└─$ python3 solve.py
©¸¸¹su¥§yªw¨{}vt¥|yzut¥ª©¦vy{v|wu¨¥¥|
§§¨bdhfjleckhidcehjekfdk
qQqSWUY[TRZWXSRTWYTZUSZ
v`@`BrtFwDuHJCArIFGBArwvsCFHCIDBurrI
et_tu?_1ac5f3d7920a85610afeb2572831daa8
TcNcd.N PR$U"S&(!/P'$% /PUTQ!$&!'" SPP'
CR=RS=OADBOODC@BOO
2A,AB
>32?1>>031
!01û-/ñ"ÿ óõþü-ôñòýü-"!.þñóþôÿý --ô
/
/ ê
ìàîâäíëãàáìëíàâíãîìã
ùÙùÛ
ßÝÑÓÜÚ
      ÒßÐÛÚ

           ÜßÑÜÒÝÛ

                  Ò
ÈèÊúüÎÿÌýÀÂËÉúÁÎÏÊÉúÿþûËÎÀËÁÌÊýúúÁ
íü×üý·×¹éë½î»ì¿±º¸é°½¾¹¸éîíêº½¿º°»¹ìéé°
ÜëÆëì¦Æ¨ØÚ¬ÝªÛ® ©§Ø¯¬­¨§ØÝÜÙ©¬®©¯ª¨ÛØØ¯
ËÚµÚÛµÇÉÊÇÇÌËÈÊÇÇ
ºÉ¤ÉÊ¤¶¸»¹¶¶»º·¹¶¶
```
We can easily recognize `et_tu?_1ac5f3d7920a85610afeb2572831daa8` is what we're looking for.

So, the flag is: `picoCTF{et_tu?_1ac5f3d7920a85610afeb2572831daa8}`


