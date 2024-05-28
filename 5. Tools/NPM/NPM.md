Node Package Manager (NPM) is used to handle and install packages and modules for JavaScript (see [[Node - Introduction to Node.js?]])

### Initializing NPM
* If NPM is needed in a project, it must be initialized
	* Will ask a variety of questions 
* Initializing NPM creates a package.json file (see [[package.json and package-lock.json]])
```bash
npm init 
```

### Installing NPM Modules/External Libraries
* Packages can be installed using the npm install command
* Packages can be installed local or globally
	* Locally --> can only be used in the installed project
		* Recommend --> allows for latest version to be used
	* Globally --> can be used across all project
```bash
* Installing locally
npm install leaflet
npm install lodash-es

* Installing globally
npm install parcel -g
```
