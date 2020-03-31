---
layout: post
title: fiddlin' bits
category: software
tags: [c++, c, bitwise ops]
---

A loose collection of biwise magic:

1. Set the kth bit in n

	n = n | 1 << k;

2. Clear the kth bit in n

	n = n & 0 << k;
	n = n & ~(1 << k); // same as above
	n &= ~(1 << k);

3. Toggle the kth bit in n

	n = n ^ 1 << k;


4. Erase the lowest set bit:

	x = x & (x - 1);

5. Isolate the lowest bit that is 1 in x

	x & ~(x - 1);

6. Identity - useful for extracting least significant bit

	x &= 1;

7. Exponentiation base 2. This prevents ambiguity errors that might come up if using `<cmath>` in something like:

	std::array<int>(pow(2, 64)); // ambiguous, first param expects a double
	// avoid this and just use >>
	std::array<int>(1 << 64);

8. Toggle last bit - useful in keeping a binary sum (e.g., parity count - even/odd count of 1s in binary)

	short result = 0;
	while(x) {
	    if(bitIsOne(x))
                result ^= 1;
		x &= (x - 1); // erase lowest set bit (see #4)
        }
	return result;


