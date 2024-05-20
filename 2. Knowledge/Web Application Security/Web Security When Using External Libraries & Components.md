# Security: Connecting External Libraries & Components
* Using the <script></script> tag to import external libraries is dangerous
	* Cannot control someone else's server
	* Files can be changed --> introduce vulnerabilities to a project

### Protecting via Explicit Versioning
* How to protect against changes (2 options)
	1) Use explicit versions of the library or component
	2) Load the module or library into the project directory and specify the local path
		* Can reduce build time if too large

```html
<!--Less Secure-->
<script src="https://code.jquery.com/jquery.slim.min.js"></script> 

<!--More Secure-->
<script src="https://code.jquery.com/jquery-3.4.1.slim.min.js"></script> 
```

### Protecting via Hashing
* Files can be protected with a key
	* When downloading a file, the browser will check will check if the file is the same one specified during production
	* If the sum is the same, the browser will download the file (since it has not changed)
* How to protect via hashing?
	* Use the `integrity` attribute on the `<link>` and `<script>` tag
	* Calculate the hash of the file ([calculate the checksum]([https://www.srihash.org/](https://www.srihash.org/).))
	* Indicate the algorithm that it should be calculated with (separated by a dash)
	* Attached a cryptographic key to the attribute (calculated on contents of the file)
	* Add the `crossorigin` attribute and set equal to `"anonymous"`. 
		* Means no user data will be transmitted during the request even if they are authorized on the server from which the file is requested
* Example
```html
<!--The algorithm to be used is sha384-->
<script
  src="https://code.jquery.com/jquery-3.4.1.slim.min.js"
  integrity="sha384-J6qa4849blE2+poT4WnyKhv5vZF5SrPo0iEjwBvKU7imGFAV" 
  crossorigin="anonymous"
>
</script> 
```

### Blocking Dependencies
* The `package-lock.json` file lists the packages that MUST be installed strictly in the specified versions (see [[package.json and package-lock.json]])
	* Prevents newer versions from being installed without notifying the engineer

### Database Vulnerabilities
* Components should be checked for vulnerabilities before being used in a project
* [CVE Details](https://www.cvedetails.com/) is an open-source database of well-known vulnerabilities 
	* Can search by company name, product, or vulnerability type.

### Checking for Dependency Vulnerabilities
* NPM has a built-in audit system that will report dependencies that have vulnerabilities
```bash
* will check dependencies with vulnerabilities
npm audit
```

### GitHub Security Alert
* Dependabot is a special tool on GitHub to monitor vulnerabilities in packages
* Connecting dependabot
	* Go to the GitHub repo --> open settings --> open security & analysis --> click 'enable' dependabot alerts
![A screenshot of the Security & Analysis options in the settings of a GitHub repo with the Enable button next to “Dependabot alerts” highlighted.](https://practicum-content.s3.us-west-1.amazonaws.com/resources/moved_Frame_1503_1652113313.png)

* If a dependabot vulnerability is detected, a notification will appear on the repository landing page
	* Click "See Dependabot alerts" to see which dependency is vulnerable
	* The dependency can be clicked to see more info
![A warning saying “We found potential security vulnerabilities in your dependencies. Only the owner of this repository can see this message” with a prompt next to it that allows the user to see Dependabot alerts.](https://practicum-content.s3.us-west-1.amazonaws.com/resources/moved_Frame_1506_1652113356.png)

![A list of Dependabot alerts on GitHub.](https://practicum-content.s3.us-west-1.amazonaws.com/resources/moved_Frame_1501_1652113416.png)

![A screenshot of Dependabot alerts showing coding for dependencies.](https://practicum-content.s3.us-west-1.amazonaws.com/resources/moved_Frame_1502_1652113456.png)