# RSA - 80

#### Writeup by henryyang42
Created: 2015-04-11

---

#### Answer
This is a fundamental RSA problem. If you have never heard of it before, this is your best chance to know [it](http://www.ruanyifeng.com/blog/2013/07/rsa_algorithm_part_two.html).

From the given data, we can add them in a python script.

```python
# Ciphered message
m= 0x58ae101736022f486216e290d39e839e7d02a124f725865ed1b5eea7144a4c40828bd4d14dcea967561477a516ce338f293ca86efc72a272c332c5468ef43ed5d8062152aae9484a50051d71943cf4c3249d8c4b2f6c39680cc75e58125359edd2544e89f54d2e5cbed06bb3ed61e5ca7643ebb7fa04638aa0a0f23955e5b5d9
# p
p = 0xc315d99cf91a018dafba850237935b2d981e82b02d994f94db0a1ae40d1fc7ab9799286ac68d620f1102ef515b348807060e6caec5320e3dceb25a0b98356399
# q
q = 0xe90bbb3d4f51311f0b7669abd04e4cc48687ad0e168e7183a9de3ff9fd2d2a3a50303a5109457bd45f0abe1c5750edfaff1ad87c13eed45e1b4bd2366b49d97f
# Public key, N = p * q
N = 0xb197d3afe713816582ee988b276f635800f728f118f5125de1c7c1e57f2738351de8ac643c118a5480f867b6d8756021911818e470952bd0a5262ed86b4fc4c2b7962cd197a8bd8d8ae3f821ad712a42285db67c85983581c4c39f80dbb21bf700dbd2ae9709f7e307769b5c0e624b661441c1ddb62ef1fe7684bbe61d8a19e7
# Exponent
e = 65537
# (e * d) mod ((q-1)*(p-1)) = 1
d = 0x496747c7dceae300e22d5c3fa7fd1242bda36af8bc280f7f5e630271a92cbcbeb7ae04132a00d5fc379274cbce8c353faa891b40d087d7a4559e829e513c97467345adca3aa66550a68889cf930ecdfde706445b3f110c0cb4a81ca66f8630ed003feea59a51dc1d18a7f6301f2817cb53b1fb58b2a5ad163e9f1f9fe463b901

def egcd(a, b):
    if a == 0:
        return (b, 0, 1)
    else:
        g, y, x = egcd(b % a, a)
        return (g, x - (b // a) * y, y)

def modinv(a, m):
    g, x, y = egcd(a, m)
    if g != 1:
        raise Exception('modular inverse does not exist')
    else:
        return x % m

# Actually, d can be calculate from e, p, q
print '`modinv(e, (p-1)*(q-1)) == d` is', modinv(e, (p-1)*(q-1)) == d


# Decipher
m = pow(m, d, N)
# Convert decimal to hexidecimal string so that we can easily decode it
m = str(hex(m))
# Remove useless info
m = m.strip('0x').strip('L')

# Here comes our message
print m.decode('hex')
```
This script can be a simple template to keep with. We'll see it in a near future.

---
[gimmick:FacebookLike](http://www.facebook.com)
[gimmick:Disqus](nthuctfnotes)
