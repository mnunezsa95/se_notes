See:
* [[TS - Introduction to TypeScript]]
Resources:
* [Documentation: TypeScript](https://www.typescriptlang.org/)

---
# TypeScript Compiler

## What is the TypeScript Compiler?
* The TypeScript compiler (`tsc`) translates TypeScript code into JavaScript code, making it possible to run TypeScript in environments that only understand JavaScript, such as web browsers and Node.js. Here’s a breakdown of what the TypeScript compiler does:
	1. **Type Checking**:
	    - TypeScript is a typed superset of JavaScript, meaning it adds static types to JavaScript. The compiler checks for type errors in the code before it’s compiled, helping to catch mistakes early (e.g., assigning a string to a variable expected to be a number).
	    - TypeScript's type-checking features enhance code quality and readability by enforcing type rules.
	2. **Transpilation**:
	    - TypeScript can use advanced JavaScript features that may not be fully supported across all environments, especially older browsers. The TypeScript compiler transpiles these features into JavaScript syntax compatible with specified versions (like ES5 or ES6).
	    - This allows developers to write modern code and have it run reliably across various JavaScript environments.
	3. **File Generation**:
	    - For each TypeScript file (`.ts` or `.tsx`), the compiler produces an equivalent JavaScript file (`.js`) that can be executed. The resulting JavaScript code doesn’t contain TypeScript-specific syntax or type annotations; it’s plain JavaScript.
	4. **Source Maps** (Optional):
	    - The TypeScript compiler can also generate source map files (`.js.map`), which help in debugging by mapping the compiled JavaScript code back to the original TypeScript code. This is particularly useful when tracking down bugs, as developers can view the original TypeScript code in debugging tools.
	5. **Declaration Files** (Optional):
	    - TypeScript can generate `.d.ts` files, which are type declaration files. These files describe the types in a JavaScript library, allowing TypeScript to check types for libraries that may not be written in TypeScript. These are useful for integrating JavaScript libraries into TypeScript projects with type safety.


# Working with the TS Compiler
## Creating a TSC Compiler File
* Run the following command inside the project file
```bash
tsc --init
```
* Edit the options as needed

## Useful TypeScript Compiler Settings
```bash
"noEmitOnError": true # Does not compile JavaScript when errors are present
"noUnusedLocals": true
"noUnusedParameters": true
"noImplicitReturns": true
"strictNullChecks": true
```

## Providing Specific Pathways
* The compiler can look in specific pathways within the root directory
```bash
{
  "compilerOptions": {
    "rootDir": "./src", # Compile TS files in ./src
    "outDir": "./build/js", # Output JS files in ./src/js
    "strict": true
  },
  "include": [
    "src/**/*" # Include ts files in src/folder_1/folder_2
  ]
}
```

## Running the Compiler
```bash
tsx main.ts # Compiling a TypeScript file
tsc "src/chapter 1/main.ts" # Compiling a TypeScript file with spaces in name
tsc "src/chapter 1/main.ts" -w # Watches for continuous changes
```



# Linking TSC Compiler & Debugger on vsCode
* Go to debugger panel and click the "create a launch.json file" button
* Add the following setting: `"preLaunchTask": "tsc: build - tsconfig.json",`
