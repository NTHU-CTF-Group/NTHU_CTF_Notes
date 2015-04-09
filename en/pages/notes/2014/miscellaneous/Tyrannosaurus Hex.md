# TEST
```py
from threading import Thread

def Ext_Euclid ( a , b ):
    if (b == 0):
        return 1 , 0 , a
    else:
        x , y , q=Ext_Euclid( b , a % b )
        x , y = y,( x - a / b * y )
        return x , y , q


s = [(1, 2), (2, 3), (8, 13), (4, 29), (130, 191), (343, 397), (652, 691), (858, 1009),
   (689, 2039), (1184, 4099), (2027, 7001), (5119, 10009), (15165, 19997), (15340, 30013),
   (29303, 70009), (42873, 160009), (158045, 200009), (1, 200009*160009)]


X = 200009*160009

def mul_inv(a, b):
    b0 = b
    x0, x1 = 0, 1
    if b == 1: return 1
    while a > 1:
        q = a / b
        a, b = b, a%b
        x0, x1 = x1 - q * x0, x0
    if x1 < 0: x1 += b0
    return x1
```
