Resources
* [Parcel: Documentation](https://parceljs.org/)

### What is Parcel?
* Parcel is a local installable build tool for bundling JavaScript modules

### Installing Parcel
* Installed using npm (see [[NPM]])
* MUST be installed as a **development** dependency 
	* Not needed in the final code (not needed for production)
```bash
npm install parcel --save-dev
```

### How to use Parcel
* Parcel uses a command line interface 
* To run parcel, can either use 
	* npx 
	* npm scripts 
* Automatically configures Babel (see [[Configuring Babel]])

```bash
* Using npx
npx parcel index.html
```

```json
// Adding a script inside package.json
"script": {
	"start": "parcel index.html",
	"build": "parcel build index.html"
}
```

```bash
* Running a script
npm run start
```

### How it works
* When bundling a project with parcel, it will create a **distribution (dist)** folder containing files created by parcel based on the project

---

# Example: Using Parcel
* Bundling the **index.html** file
```bash
npx parcel index.html
```

* Enabling hot module reload 
	* Allows for state to be automatically maintained
```js
if (module.hot) {
	module.hot.accept
}
```

