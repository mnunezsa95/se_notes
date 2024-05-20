See: [[Py - Introduction to Python]], 
Resources:
* Documentation: [Streamlit](https://streamlit.io/)
	* Examples: [Apps Built with Streamlit](https://streamlit.io/gallery)
* Documentation: [Render](https://render.com/)

---

# Web Apps
#### Python & Web Development
* There are two popular generic framework for web development in Python
	* Django
	* Flask
* There are other frameworks:
	* Streamlit (Data Science)

# What is Render?
* A service that provides hosting infrastructure for running applications

# What is Streamlit
* A framework developed by Data Scientists to build data applications

---
---

# Building a Web App with Streamlit
#### Creating a New Repo (GitHub)
1) Create a new repo on GitHub. Include:
	* `README`
	* `.gitignore` (python template)
2) Clone the repo to local machine

#### Create a new Venv
1) Create a new virtual environment
```bash
# Create a virtual environment & folder to store virtual environment
python3 -m venv venv
```
2) Active the virtual environment
```bash
source ./venv/bin/activate
```

#### Install Dependencies
1) Install any needed dependencies
	* streamlit -- needed
```bash
pip install streamlit
```

#### Adding Requirements File
1) Create a new file `requirements.txt` in the root directory
2) Add content to requirements file:
```Example
pandas==2.0.3
scipy==1.11.1
streamlit==1.25.0
altair==5.0.1
plotly==5.15.0
```

#### Add Configuration Directory & Config File
1) Create a directory called: `.streamlit`
2) Create a config file called: `config.toml`
```pathway 
.streamlit/config.toml
```
3) Add configuration settings to the `config.toml` file
	* This tells the application to run in server (headless) mode at `0.0.0.0.10000` 
```
[server]
headless = true
port = 10000

[browser]
serverAddress = "0.0.0.0"
serverPort = 10000
```

#### Add entry point file
1) Create an `app.py` file in the root directory. 
	* This will serve as the entry point for the application. The file that runs when the application is launched

#### Test the Application
1) Run the following command to launch and test the application
```bash
streamlit run app.py
```

#### Push Changes to GitHub
1) Push to GitHub

---
# Building & Deploying with Render
#### Access Render
1) Log into Render
2) Go to Dashboard --> New Web Service 
3) Connect GitHub to Render & select the repo to be used

#### Setup Deployment on Render
1) Choose an name for the web-service
2) Select the appropriate environment
	* Most likely `Python 3`
3) Add the following **Build Command**
```bash
pip install streamlit & pip install -r requirements.txt
```
4) Add the following start command
```bash
streamlit run app.py
```
5) Deploy application

#### Test Application
1) Wait about 10-15 minutes and check at the application URL
