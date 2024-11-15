See: 
* [[JS - Introduction to JavaScript]]


---
# Array Concept Reviews
* Some array functions like `filter()`, `forEach()`, `map()`, `sort()` and others accept an array as the first parameter.
```JS
function bingo(ticket, win) {
	// Variable to hold result
	let count = 0;
	
	// Iterate through each sub-array in ticket array
	ticket.forEach(([str, num]) => {
	    // Split the string in each sub-array
	    // Determine if atleast some of the strings' ASCII matche the number
	    let = isMatch = str.split("").some((char) => char.charCodeAt() === num);
    
    // If yes, increment count
	    if (isMatch) {
		    count++;
	    }
    });
    
	return count >= win ? "Winner!" : "Loser!";
}

console.log(bingo([["ABC", 65], ["HGR", 74], ["BYHT", 74]], 1)); // Winner!
```

```JS
function myLanguages(results) {
	// Save the entries from the dict in an array of arrays
	const entries = Object.entries(results);
	
	// Filter through each sub-array, and filter out values larger than 60
	// Sort the results by descending order
	// Output the keys into an array
	return entries
		.filter(([key, value]) => value >= 60)
		.sort(([, valueA], [, valueB]) => valueB - valueA)
		.map(([key, value]) => key);
}
	
console.log(myLanguages({ Java: 10, Ruby: 80, Python: 65 })); 
// ['Ruby', 'Python']
console.log(myLanguages({ Hindi: 60, Greek: 71, Dutch: 93 }));
// ['Dutch', 'Greek', 'Hindi',]
```