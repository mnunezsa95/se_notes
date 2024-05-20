See [[Coding Exercises]]

**![](https://lh4.googleusercontent.com/PQqcgk4oaMtxv_gw6tpiIiyS6u-MYa8pY6uYZqoZLtW3Tjjqhvgm06ZX3hJZRWydAtkIIlbed4GIM5KudYhIx_6BRHDfvCnKwxe1d9ZqxF8tBhrgyu_k5_f_soPjZOJB1hmMZjmYvtIs2TdqlKuD_Zo)

#### Solution 1:
```js
function divisibleSumPairs(n, k, ar) {
	let count = 0;
	for (let i = 0; i < n; i++) {
		for (let j = i + 1; j < n; j++) {
			if ((ar[i] + ar[j]) % k === 0) {
		        count++;
		    }
	    }
	}
	return count;
}
```