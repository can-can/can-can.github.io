---
layout: post
title: Two skills in HashMap
categories: en
category: en

---

I have read the source code of HashMap, and I find two useful skills.

# take modulo operation efficiently.

In HashMap, the range of the result produced by the hash() method from -2,147,483,648 to +2,147,483,647. However, the default initial size is 16, which is smaller than the range. So who to reduce the bigger one to the smaller one.

There are two methods:

## Normal Modulus

preconditions:
```

int hashCode  = hash();

int size = 16;
```

operation:

`int index =  Math.abs(hash) % size;`

Can we do better in performance? YES!

## Modulus by using bitwise operation

preconditions:

```
int hashCode  = hash();

int size = 16;
```

operation:

`int index =  hashCode & (size - 1);`

The operation above is more efficient than previous one.

Can HashMap use this method? Yes! However, need a restriction.

The restriction is that the size must be a power of two. Why?

Let’s see an example.

This time, we say the size is 10 which represented in binary is `00001010`.
No matter what's the hashCode, the possible values are:
```
00001010 & 11110000 = 0000 
00001010 & 00001101 = 1000
00001010 & 00000111 = 0010
00001010 & 00001010 = 1010
```
This situation reduces usage of the array in HashMap, using only four blocks.

In HashMap, the size of the array is 2^n - 1 which binary represent is all 1 in every bit so that HashMap makes the most use of the array.

# calculate hash once more
```
static final int hash(Object key) {
    int h;
    return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);
}
```
This method mix higher bits with lower bits, which can reduces collision.

