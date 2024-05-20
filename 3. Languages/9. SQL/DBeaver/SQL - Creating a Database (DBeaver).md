After creating a DBeaver connection, a database can be created (see [[SQL - Creating a New Connection (DBeaver)]])

#### Creating a DB
* There are two ways to create a DB on DBeaver
	1) GUI Option
	2) SQL Code Option

#### GUI Option
1) Go to "Database Navigator Window" --> Right click on a connection --> select "Create", then "Database"
![](https://lh7-us.googleusercontent.com/e7iTyDLdCg6nXTpFz0yOA4ZBmz49lrfaHsTZz1uEkhjAHjG6O2xH8JiIxEyXKREDL2Je5nhirPKzBXiXSjZWv9jUFuWxuu91iHO_slfgVEkqYIDxoSMCKzNw7fVvT-Anot4pX68nrd40t7CZG_9SgaY)

2) A dialog box with database parameters will open. 
	* Enter the database name without changing any other parameters
![](https://lh7-us.googleusercontent.com/Xg8rCrUKKNx8lhhhswBk2XiAK-IPNLT9o92OZqmox0Rp2ygj35pJzqW6tz6sAN4xtPLykEpUE1ivsEeoX6lYEjt7ZONKcDYrjDBhnmSF6laHO4DNwWjPMmNCI35pAiyPAeU5ub7S-Zd06pYCE-np38Y)

#### SQL Code Option
1) Select "SQL Editor", followed by "New SQL Script"
![](https://lh7-us.googleusercontent.com/z1en2vtLtsiAbkIlSplp1xUO0b4kuXtynjH2YUxeBOxWcI4PItqMOSFSkudNT5l422QkTC1ZygKBZ-S3DKyS7u_8oZ6wsEPumzHkJkeT4Ggt9AIN3d2FojDCWbUoEDcTpJmsXGoRivMDKPIkG9KgXY4)

2) Use the following command & run it (by clicking orange ► icon in the top-left corner of the Script window)
	* `CREATE DATABASE` --> will create a database
	* `query_database` is the name
```sql
CREATE DATABASE query_database; 
```

![](https://lh7-us.googleusercontent.com/yj67iaaYCcnRoyOmsR1n1f8tqLp1Av-IF14Z_oUld6072wAwKV3YeuINkwOKwM0ZDsO_m0LcqAk_5kuP5gQ_8REVrjg6ZGFOekXSYDvdOEEbf5AinvjXMCeiNrAznYGhXL3HZ_6TnS7XJhVYFNhSiww)