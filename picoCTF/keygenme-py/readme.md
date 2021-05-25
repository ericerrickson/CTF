
# <span style="color:red">:checkered_flag:   picoCTF Competition</span>
-----------------------
### keygenme-py
------------------------ 

>| 30 points
>| Tags: Reverse Engineering
>| Author: syreal
>| Description: (None)
>| Hints: (None)
>| 2,343 solves / 7,010 attempts (33%)

In this Capture The Flag challenge, we are given no direction, nor even a description of the problem. We just know we need to retrieve the flag. We are given access to one file, a Python script called *keygenme-trial-py*. When we run it, we get this output to the terminal:


```
___Arcane Calculator___

Menu:
(a) Estimate Astral Projection Mana Burn
(b) [LOCKED] Estimate Astral Slingshot Approach Vector
(c) Enter License Key
(d) Exit Arcane Calculator
What would you like to do, FRASER (a/b/c/d)?
```

As the category is Reverse Engineering, option "(c)" Enter License Key gives us our first clue as to what we should do. Let's look at the code of *keygenme-trial-py*:


```Python
#============================================================================#
#============================ARCANE CALCULATOR===============================#
#============================================================================#

import hashlib
from cryptography.fernet import Fernet
import base64

```
OK, it is importing crypto stuff. What is Fernet? Hey, Google... 
Right, Fernet is a system for symmetric encryption/decryption. We are also going to be hashing things, because we are also importing *hashlib*, and lastly, we are importing *base64*, presumably to deal with the big, honking blob at line 234:


```Python
# Encrypted blob of full version
full_version = \
b"""
gAAAAABgT_nvqFdgzE0SICXvq-e6JoMrQpqxEKXoCsaUgvMCZM4ulMyWVfQ0hUgnEpPeHu(etc, ad nauseam)
```

So, let's see if we can abuse the "*c*" option. We'll start by looking at what it calls:

```Python
def enter_license():
    user_key = input("\nEnter your license key: ")
    user_key = user_key.strip()

    global bUsername_trial
    
    if check_key(user_key, bUsername_trial):
        decrypt_full_version(user_key)
    else:
        print("\nKey is NOT VALID. Check your data entry.\n\n")
```

It calls the "*check_key*" function shown below:

```Python
def check_key(key, username_trial):

    global key_full_template_trial

    if len(key) != len(key_full_template_trial):
        return False
    else:
        # Check static base key part --v
        i = 0
        for c in key_part_static1_trial:
            if key[i] != c:
                return False

            i += 1

        # TODO : test performance on toolbox container
        # Check dynamic part --v
        if key[i] != hashlib.sha256(username_trial).hexdigest()[4]:
            return False
        else:
            i += 1
```




<span style="color: Green; font-family: Consolas; font-size: 0.7em;">Overview of Fernet
</span>
