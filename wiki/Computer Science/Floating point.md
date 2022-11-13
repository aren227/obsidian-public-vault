---
title: Floating point
author: aren227
date: 2022-10-27T14:09:33+09:00
lastmod: 2022-11-14T01:19:17+09:00
tags:
- computer-science
---

Computers represent real numbers as something called floating point numbers. The reason why they are called like this is that radix point can float anywhere between the significant digits. So this is kind of scientific notation where numbers are represented with exponent and significand.

## Format
Most commonly used floating point representation follows IEEE 754 standard.
- 1 sign bit to represent the sign of the number.
	- 0 for positive numbers, 1 for negative numbers.
- $E$ bits to represent the exponent.
- $S$ bits to represent the significand.
	- Because the numbers are normalized, the first significant number is always $1$. They actually have $S+1$ bits of precision.

| Type | Sign | Exponent ($E$) | Significand ($S$) | Total | Exponent Bias ($B$) | Number of decimal digits |
| ----- | ----- | ---------- | ----------- | ---- | ------ | ----- |
| Half | 1 | 5 | 10 | 16 | 15 | ~3.3 |
| Single | 1 | 8 | 23 | 32 | 127 | ~7.2 |
| Double | 1 | 11 | 52 | 64 | 1023 | ~15.9 |
| x86 Extended Precision | 1 | 15 | 64 | 80 | 16383 | ~19.2 |

So the actual value is
$$ (-1)^{SignBit} \cdot (1.SignificandBits)_2 \cdot 2^{Exponent - B} $$
Exponent is stored as an unsigned integer which is always positive. Because the bias $B$ is subtracted from the exponent, we can represent negative exponent.

## Exponent encoding
There are some special cases where exponent is entirely filled with zero or one.

### If both exponent and significand are zero
These numbers are just simply $0$.
But sign bit can be either zero or one, so they represent $+0$, $-0$ respectively. They just look same but work differently in some operations. For example,
- $1 / +0$ returns $+\infty$, $1 / -0$ returns $-\infty$.

### If exponent is zero, but significand is non-zero
These numbers are called subnormal numbers.
If every floating point numbers are forced to be normalized numbers, The smallest possible positive value will be:
$$ (1.0000...)_2 \cdot 2^{-B} = 2^{-B}$$
But if exponent is zero, significand is considered as denormalized numbers. As a result, they fill the gap between zero to the smallest normalized value linearly.

### If exponent is filled with one and significand is zero
These numbers represent $+\infty$, $-\infty$ according to its sign bit. This happens when
- $R / \pm 0$, $R \cdot \pm \infty$ where $R$ is neither $\pm 0$ or $\pm \infty$.
- $\pm \infty \cdot \pm \infty$ 

### If exponent is filled with one and significand is non-zero
These numbers represent NaN (Not a Number). This happens when
- $\pm0 / \pm0$, $\pm\infty / \pm\infty$
- $\infty - \infty$, $-\infty +\infty$

## Base Conversion
>[!todo]

## Arithmetic
>[!todo]

## Extended Double Precision
x86 processors used 80 bits floating point internally. These values (registers) are stored in floating-point unit (FPU). The benefit is that they can minimize roundoff and overflow errors thanks to the high precision. So every 32, 64 bits floating point values are converted to 80 bits first. Then do some calculations in 80 bits precision and rounded back to its original precision.
In x86 compatible GCC compilers,  `long double` type is available for 80 bits precision. We can store values back to this variable without loss of precision.
For memory alignment purposes, `long double` variable usually takes 16 or 12 bytes.

> [!warning]
> MSVC compilers treat `long double` as 64-bit floating point numbers.
> C++ standard specifies that `long double` must be a superset of the values that a `double` can represent. That means `long double` still can be 64-bit floating point. Actually  `long double` is identical to `double` on many architectures.

But this can also have some side effects too. In debug build, intermediate 80-bit values should be writed to main memory so they are constantly casted to 32 or 64-bit, causing precision loss. While in debug build, some consecutive operations can be entirely done in 80-bit registers, the results can be different.

## Precision Issue
The floating point numbers are logarithmically spaced, not linearly.
That means, If we try to add a large and a small number, Small numbers will likely to be ignored.
Also note that almost half of the entire floating point numbers are lying between just $-2$ to $2$. This is because exponent bias $B$ equals to $2^E / 2 - 1$.

>[!todo]
>Why exponent bias  is determined like this?

