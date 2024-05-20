See [[Coding Exercises]]

**![](https://lh6.googleusercontent.com/Kg5y85yaLxuZnZV-uSWo_FQlfNQNcAhuffyxZijl09125Mgj7TgT_dooHFnemihzl8LT0vh_ytLcaEBsKa4g_O_ScCsOM3Z5JguK3Ulkh8dFW4a_5Na3n7kl3T6YsWT9-ZwO47biQyI1B5XmElS09Qc)

#### Solution 1: Using 2 Loops
* Time Complexity : O(n^2)
* Space Complexity : O(n)
```js
function matchingStrings(strings, queries) {
	let res = [];
	for (let i = 0; i < queries.length; i++) {
		res[i] = 0;
	    for (let j = 0; j < strings.length; j++) {
		    if (queries[i] === strings[j]) {
		        res[i]++;
		    }
		}
	}
	return res;
}
```

#### Solution 2: 
* See example [here](https://www.aldohadinata.com/hackerrank-sparse-arrays-solution-in-javascript/)
