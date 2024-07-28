# Given the keys and Ivs functions,

Translate the formula into functions 
```py
def compute_iv1(x):
    return (math.exp(x) + math.exp(1/2)) / 3
    

def compute_iv2(x):
    return (math.exp(15/6) + math.exp(-x)) / 55

def fibonacci(n):
    fib_sequence = [0, 1]
    while len(fib_sequence) <= n:
        fib_sequence.append(fib_sequence[-1] + fib_sequence[-2])
    return fib_sequence[n]


def compute_key1(x):
    sum1 = sum(1 / (5 * k - 2) for k in range(2, x + 1))
    sum2 = sum(1 / (7 * k) for k in range(3, x + 1))
    return sum1 + sum2


def compute_key2(x):
    return sum(1 / factorial(k) for k in range(3, x + 1))


def compute_key3(x):
    return sum(1 / k**6 for k in range(2, x + 1))

def compute_key4(x):
    return sum(1 / (fibonacci(k)) for k in range(6, x + 1))
```

# Given the Xs, 
```py
Key_X = [10000000000, 100, 100000000, 100] 
IV_X = [-100, 100]
```

### Note of Effort :
 Before the X values were released, i tried to bruteforce it, since there is 4 keys that is appended with .7f, len(key)= 8\*4=32 , with 8 unit length for all 4 parts, same goes for IV, 2 parts with 8 unit length, len(IV)=8\*2. Given the constraint f(x)<10 && f(x)>-10 , we can find a range of x that could work by plotting it in desmos.. It helps reducing SOME Xs range that need to be calculated, 

The example below for IV 1st function, 
 
![image](https://github.com/user-attachments/assets/3e311006-eeb0-49f5-9acc-b9c328f63899)

![image](https://github.com/user-attachments/assets/a0991c38-07a7-4ff0-830b-a44f1d15c74b)

we can safely assume the X value range for this function is between -∞ to 6. Yeah goodluck calculating that. However we can see that f(x) tends to a number as it approaches -∞, denoted as :

$$
\lim_{{x \to -\infty}} \frac{e^x + e^{\frac{1}{2}}}{55} ≈ 0.0299768
$$

This is great since we can stop iterating for X when f(x) reaches this value. Alternatively we can iterate X until it gave the same approximation for 7 float points.
There is probably a better way to guess the X ranges for each function but this is the best I could come up with, before the hints were released lol. 


# Compute

Define the array of functions and run it through the KDF ( Key Derivation Function ).

```py
KEYs = [compute_key1, compute_key2, compute_key3, compute_key4]
IVs = [compute_iv1,compute_iv2]
Key_X = [10000000000, 100, 100000000, 100] 
IV_X = [-100, 100]

key = KDF(KEYs,Key_X)
IV = KDF(IVs,IV_X)
```

Since it takes some time to calculate i took the liberty to use powerful online calculation tool.. Desmos and Wolfram alpha. 
I could've use Memoization for the fibonacchi function and simplify all the other functions(maybe) but using those platform are much faster.
Here is a revised function that returns the value i got from those platforms with reference. Below is the full code

```py
import math
from math import factorial
from Crypto.Cipher import AES
from Crypto.Util.Padding import unpad

def compute_iv1(x):
    # return (math.exp(x) + math.exp(1/2)) / 3
    # https://www.wolframalpha.com/input?i2d=true&i=Divide%5BPower%5Be%2C-100%5D%2BPower%5Be%2CDivide%5B1%2C2%5D%5D%2C3%5D
    return 0.5495737569000427156162169292713878572179253793036359239278129804
    

def compute_iv2(x):
    # return (math.exp(15/6) + math.exp(-x)) / 55
    # https://www.wolframalpha.com/input?i2d=true&i=Divide%5BPower%5Be%2C-100%5D%2BPower%5Be%2CDivide%5B15%2C6%5D%5D%2C55%5D
    return 0.2214998901946086079649122900212357487851412332229803831230683267


def fibonacci(n):
    fib_sequence = [0, 1]
    while len(fib_sequence) <= n:
        fib_sequence.append(fib_sequence[-1] + fib_sequence[-2])
    return fib_sequence[n]

# Key 1 computation
def compute_key1(x):
    # sum1 = sum(1 / (5 * k - 2) for k in range(2, x + 1))
    # sum2 = sum(1 / (7 * k) for k in range(3, x + 1))
    # return sum1 + sum2
    # https://www.desmos.com/calculator/fbeem92oi4
    return 7.73754163755

# Key 2 computation
def compute_key2(x):
    # return sum(1 / factorial(k) for k in range(3, x + 1))
    # https://www.wolframalpha.com/input?i2d=true&i=++++++Sum%5BDivide%5B1%2Ck%21%5D%2C%7Bk%2C3%2C100%7D%5D
    return 0.2182818284590452353602874713526

# Key 3 computation
def compute_key3(x):
    # return sum(1 / k**6 for k in range(2, x + 1))
    # https://www.wolframalpha.com/input?i2d=true&i=++++++Sum%5BDivide%5B1%2CPower%5Bk%2C6%5D%5D%2C%7Bk%2C2%2C100000000%7D%5D
    return 0.0173430619844491397145179297909

# Key 4 computation
def compute_key4(x):
    # return sum(1 / (fibonacci(k)) for k in range(6, x + 1))
    # https://www.wolframalpha.com/input?i2d=true&i=++++++Sum%5BDivide%5B1%2Cfib%5C%2840%29k%5C%2841%29%5D%2C%7Bk%2C6%2C100%7D%5D
    return 0.3265523329098442198341101534172

flag = b'\x8d\x91\xa7:\x96\xec\x044I\xb4\nM\x08\x0f\xbf_\xa9\rpR\x86;\xd4y: \x02{\xdc\x82\x8b\xa0\xde5\x85\xe6\xf5\xb3\xab\xd0M\xf0\xfa\xc2\xfd(\xdce'

def KDF(KDFs,X):
	key = []
	for i in range(len(KDFs)):
		result = KDFs[i](X[i])
		key.append(f"{result:.7f}")
	return "".join(key).replace(".","")



KEYs = [compute_key1, compute_key2, compute_key3, compute_key4]
IVs = [compute_iv1,compute_iv2]
Key_X = [10000000000, 100, 100000000, 100] 
IV_X = [-100, 100]

key = KDF(KEYs,Key_X)
IV = KDF(IVs,IV_X)




def decrypt(flag, key, IV):
    decipher = AES.new(bytes(key, 'utf-8'), AES.MODE_CBC, iv=bytes(IV, 'utf-8'))
    decrypted_padded_plaintext = decipher.decrypt(flag)
    decrypted_plaintext = unpad(decrypted_padded_plaintext, AES.block_size)
    return decrypted_plaintext


print(decrypt(flag,key,IV))

``` 



# Flag

Run the code and we get 
```bash
PS C:\Users\Neno\Downloads\supasecret> python -u "c:\Users\Neno\Downloads\supasecret\supasecret\ansv3.py"
b'ihack24{df65b3be992a84c29d584b01e7afd714}'
```

The flag is `ihack24{df65b3be992a84c29d584b01e7afd714}`
