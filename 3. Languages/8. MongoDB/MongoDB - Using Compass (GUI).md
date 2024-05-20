What is the GUI (Graphical User Interface)?
* The GUI (Graphical User Interface) on MongoDB Compass allows you to view and edit databases and their entries using a visual interface.
* Databases can also be created using code (see [[MongoDB - Schemas & Models]])

Connecting MongoDB to JavaScript (see [[MongoDB - Connecting MongoDB to JS via Mongoose]])

# Using MongoDB GUI
### Creating a Database
* The **create database** button creates a new database
	* database names are case INSENSITIVE (mydb and MYDB are the same)
* The **add data** button adds new data to the database (in the form of documents)
	* documents have a unique ( __id ) generated automatically 
		* Fields --> (object keys) can be added 
		* data type --> can be changed for the field (represents the type of data)
**![](https://lh3.googleusercontent.com/1LN8aEJ2sqbUN3-1_u_1T_e549vIHuvfrBk0BO3GWOeeQMrt3P0_hBdsTWV7BThMqRZNLAb5kII0wVuIt9GMBqroOOkU7xMmkcW-uZ2ayn9kTso6IOiQN3Mkpz3Ti6DxrCTxgVa1552MaNAwPtz6vW4)**

### Filtering Data
* The **filter** section allows you to write a query (in the form of an object) to filter the database by specific conditions
```js
{} // this will find all the documents in the collection 

{ name: 'Elise' } // this query will find the docs where the name field is "Elise" 

{ name: 'Elise', age: 34 } // this query will find the docs where the name field is "Elise" and the age field is 34
```

**![](https://lh4.googleusercontent.com/O0Pj1B_QeH9fPAcmShZn6a60g4Vuf92DQveYXqjLpnrjihN_2JgGSHSe3Tlq4cLSnM3b5gyTpy8cuMgqdy-46f3Cos7jo1RFRQez80WWZxTKN1gUo_fO8nD_H5ShtjUlZgfxbauKL8Ahya8WKfj9mUA)

