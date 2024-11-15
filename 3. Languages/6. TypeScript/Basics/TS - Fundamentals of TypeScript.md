See:
* [[TS - Introduction to TypeScript]]
* [[TS - TypeScript Compiler]]
Resources:
* [Documentation: TypeScript](https://www.typescriptlang.org/)

https://www.youtube.com/watch?v=d56mG7DezGs&t=1684s
----
# TypeScript Fundamentals
* TypeScript is a ***strictly-typed*** language, which demands the the specification of data types
* TypeScript is a ***statically-typed*** language, where types are checked at ***compile*** time
* JavaScript is a ***dynamically-typed*** language, where types are checked at ***run*** time


# Functions

## Void Functions
* A **void function** is a function that does not return a value
* Void functions perform actions or side effects such as logging to the console, modifying a variable, interacting with the DOM, etc

* Void functions can be interpreted
```TS
function calculateTax(income: number) {
	console.log(income)
}
```

* Void functions can be explicitly declared
```TS
function calculateTax(income: number): void {
	console.log(income)
}
```

## Regular Functions
### Parameters & Return Values
* Function parameters must be annotated
* Function return values should also be annotated
```TS
function calculateTax(income: number, taxYear: number): number {
	if (income < 2022) {
		return income * 1.2;
	}
	return income * 1.3;
}

calculateTax(10_000, 2022);
```

### Optional Parameters
* Parameters can be made optional by adding a `?` before the type annotation
```TS
// The taxYear parameter is optional

function calculateTax(income: number, taxYear?: number): number {
	if (income < 2022) {
		return income * 1.2;
	}
	return income * 1.3;
}

calculateTax(10_000);
```

### Default Values for Parameters
* Parameters can be assigned default values when being declared
```TS
// The taxYear parameter has a default value of 2022

function calculateTax(income: number, taxYear = 2022): number {
	if (taxYear < 2022) {
		return income * 1.2
	} 
	return income * 1.3
}

calculateTax(10_000);
```


