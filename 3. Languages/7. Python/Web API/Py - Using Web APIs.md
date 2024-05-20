See: [[Py - Introduction to Python]], [[REST API - Introduction to REST API]],  [[Server Response Status Codes]], [[Py - Requests Library]]
Documentation:
* [Request Library Documentation](https://requests.readthedocs.io/en/latest/api/)

---

# Understanding Web APIs

#### HTTP 
* HTTP (Hypertext Transfer Protocol) -- an Internet protocol, a set of rules for transferring data between two computer systems

#### What are Application Programming Interfaces (APIs)?
* An API is a set of commands, functions, protocols, and objects that programmers can use to create software or interact with an external system
* An API serves as a barrier between our program and an external system
* Our program sends requests & the external system sends back a response

#### What is REST API?
* REST (Representational State Transfer) is a set of principles (software architectural style) that outline how APIs should be created
	* REST APIs have two components (completely independent of each other)
		* client
		* server
#### How APIs Work:
* The client uses the **URI** (Uniform Resource Identifier) to access **resources** on the server. 
	* Client makes a call (request) to the URL using an HTTP request --> Server makes a response to the call (request) and returns a response
		* The Response Object includes:
			* Status code
			* The contents of the request

#### Terminology: API Endpoints / API Requests
* An API endpoint is the address for the API
* An API Request is a request made to the API endpoint
* If successful the request is approved, and data is sent to the user
* A majority of data is transferred in JSON (JavaScript Object Notation) format
#### Terminology: API Parameters 
* API Parameters --> allows us to give an input when making a request to get different types of data

#### Authentication: 
* Many APIs require user-authentication in order to provide services. 
* The authentication ensures that services are provided between client and server and allow for security when being used
* Typical authentication mechanisms:
	* API Key
	* Token
	* Username & Password

---
---

# The `request` Library
* The `request` library -- a python package for interacting with web APIs

#### API Parameters
* `params` is a an argument on the `get(), post(), put(), delete()` method for specifying parameters.
```Python
MY_LAT = 42.360081
MY_LONG = -71.058884
parameters = {"lat": MY_LAT, "lng": MY_LONG}

response = requests.get(url="https://api.sunrise-sunset.org/json", params=parameters)
response.raise_for_status()
data = response.json()
print(data)
```

#### Request Headers
* Request headers are sent by the client to the server and contain information and instructions related to the requested resource
* Request headers are added to the `headers` kwargs
```Python
# The request headers
graph_headers = {"X-USER-TOKEN": PIXELA_TOKEN}

# Creating a graph definition
graph_parameters = {
  "id": "graph1",
  "name": "Cycling Graph",
  "unit": "Km",
  "type": "float",
  "color": "ajisai",
}

graph_response = requests.post(
  url=PIXELA_GRAPH_ENDPOINT, json=graph_parameters, headers=graph_headers
)
```


# Using the `request` Methods
#### The `requests.get()` Method
* The `requests.get()` method fetches data from an API. This method returns back a response object, which contains a server's response to an HTTP Request ([see doc](https://requests.readthedocs.io/en/latest/api/#requests.Response))
```Python
# Importing requests
import requests

# Defining the parameters for the data (from website documentation)
params = {"from":"USD", "to":"GBP", "amount":20}

# Making a get requests to the 'latest' endpoint
res = requests.get("https://api.frankfurter.app/latest", params=params)
print(res) # <Response [200]>

# Parsing the response to get the response object
print(res.json()) 

# Retrieving metadata from the headers object
print(response.headers['Server']) # nginx/1.21.3
print(response.headers['Content-Type']) # application/json; charset=utf-8
print(response.headers['Content-Length']) # 457
```

```Output
{'amount': 20.0, 'base': 'USD', 'date': '2022-04-19', 'rates': {'GBP': 15.3578}}
```

* Making a request using parameters in the request (instead of the `params` parameter)
```python
# Importing requests
import requests

# Defining the parameters for the data (from website documentation)
params = {"from":"USD", "to":"GBP", "amount":20}

# Making a get requests to the 'latest' endpoint
res = requests.get("https://api.frankfurter.app/latestfrom=USD&to=GBP&amount=20")
print(res) # <Response [200]>

# Parsing the response to get the response object
print(res.json()) 
```

```Output
{'amount': 20.0, 'base': 'USD', 'date': '2022-04-19', 'rates': {'GBP': 15.3578}}
```

* Retrieving data from the response object
```python
# Importing requests
import requests

res = requests.get(url="http://api.open-notify.org/iss-now.json")
data = res.json()

# Getting a specific attribute from the data returned from the server
longitude = data["iss_position"]["longitude"]
latitude = data["iss_position"]["latitude"]
```

* Raising different exceptions based on different status codes received from the server
```python
# Importing requests
import requests

### Fetching a response
res = requests.get(url="http://api.open-notify.org/iss-now.json")
res.status_code # 200
res.text # Returns back the text

# Raising exceptions
if res.status_code == 404:
  raise Exception("That resource does not exist.")
elif res.status_code == 401:
  raise Exception("You are not authorized to access this data.")
```

* Using the `requests` library to raise exceptions if request is unsuccessful.
```python
res = requests.get(url="http://api.open-notify.org/iss-now.json")
res.raise_for_status()
```

* Making a request to an API that requires authentication
```Python
# Importing requests
import requests

api_key = 'zC5JOYIAeAgn92Z9CJKUQE1ns3dvHeyf'  # API Key
params = {'apikey': api_key, 'q': 'New York'} # Defining paramaters

# Defining URL
aw_location_url = "https://dataservice.accuweather.com/locations/v1/cities/"

# Making get request
aw_location_res = requests.get(aw_location_url, params=params)

# Formatting the information returned
for loc_info in aw_location_res.json():
    print('{:>8}   {:10}   {:16}    {:16}'.format(
        loc_info['Key'],
        loc_info['EnglishName'],
        loc_info['Country']['EnglishName'],
        loc_info['AdministrativeArea']['EnglishName']))
```

```Python
# Importing requests
import requests

api_key = 'zC5JOYIAeAgn92Z9CJKUQE1ns3dvHeyf' # API Key
params = {'apikey': api_key, 'metric': True} # Defining paramaters

location_id = 349727 # Defining location ID

# Defining URL
aw_forecast_url = "https://dataservice.accuweather.com/forecasts/v1/daily/5day/" + str(location_id)

# Making get request
aw_forecast_res = requests.get(aw_forecast_url, params=params)

# Formatting the information returned
for daily_forecast in aw_forecast_res.json()['DailyForecasts']:
    print('{}   {:30} {}{}  {}{}'.format(
        daily_forecast['Date'], 
        daily_forecast['Day']['IconPhrase'], 
        daily_forecast['Temperature']['Minimum']['Value'],
        daily_forecast['Temperature']['Minimum']['Unit'], 
        daily_forecast['Temperature']['Maximum']['Value'],
        daily_forecast['Temperature']['Maximum']['Unit']))
```

#### The `requests.post()` Method
*  The `requests.post()` posts/adds data to an API. This method returns back a response object, which contains a server's response to an HTTP Request ([see doc](https://requests.readthedocs.io/en/latest/api/#requests.Response))
* The `json` parameter sends data in json format to the server
```Python
# Importing requests
import requests

# Defining the parameters for the data (from website documentation)
user_parameters = {
  "token": PIXELA_TOKEN,
  "username": PIXELA_USERNAME,
  "agreeTermsOfService": "yes",
  "notMinor": "yes",
}

# Making a post request to the server
pixela_response = requests.post(url=PIXELA_SIGNUP_ENDPOINT, json=user_parameters)
```

#### The `requests.put()` Method
* The `requests.put()` updates data to an API. This method returns back a response object, which contains a server's response to an HTTP Request ([see doc](https://requests.readthedocs.io/en/latest/api/#requests.Response))
* The `json` parameter sends data in json format to the server
```Python
# Importing requests
import requests

pixel_headers = {"X-USER-TOKEN": PIXELA_TOKEN}
date_formatted = yesterday.strftime("%Y%m%d")

# Defining the parameters for the data (from website documentation)
update_pixel_parameters = {"quantity": "15"}

# Making a put request to the server
update_pixel_response = requests.put(
  url=f"{PIXELA_CREATION_ENDPOINT}/{date_formatted}",
  json=update_pixel_parameters,
  headers=pixel_headers,
)
```

#### The `requests.delete()` Method
* The `requests.delete()` deletes data to an API
```Python
# Importing requests
import requests

today_date_formatted = today.strftime("%Y%m%d")

# Making a delete request to the server
delete_pixel_response = requests.delete(
  url=f"{PIXELA_CREATION_ENDPOINT}/{today_date_formatted}",
  headers=PIXEL_HEADERS,
)
```