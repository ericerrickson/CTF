# <span style="color:red">:checkered_flag:   picoCTF Competition</span>
-----------------------
###  Mind your Ps and Qs
------------------------
We are greeted with the screen below:

### <span style="color:darkblue">Mind your Ps and Qs                                                         | 20 points</span>

#### Description

In RSA, a small `e` value can be problematic, but what about `N`? Can you decrypt this? [values](https://mercury.picoctf.net/static/2604f8b51a5cc62d38a3736938f19cef/values)



Downloading and running FILE on 'values' gives us:
```
└─$ file values
values: ASCII text
```
and when we pop it open we find 3 numbers in the clear, 'c', 'n', and 'e':
```
Decrypt my super sick RSA:
c: 861270243527190895777142537838333832920579264010533029282104230006461420086153423
n: 1311097532562595991877980619849724606784164430105441327897358800116889057763413423
e: 65537
```