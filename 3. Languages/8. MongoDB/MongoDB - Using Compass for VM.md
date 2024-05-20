See ([[MongoDB - Using Compass (GUI)]], [[2. Connecting Node.js, MongoDB & Git to VM]])

#### Setting up MongoDB to show VM Data on Compass
1) Click `New Connection +`
2) Click `Advanced Connection Options` --> `Proxy/SSH`
3) Under the `SSH Tunnel/Proxy Method`, select `SSH with Identify File`
4) In SSH Hostname --> add the domain name 
	* Example: news-explorer.mooo.com
5) in SSH Port --> add the Port 22
6) In SSH Username --> add username of VM 
	* Example: mnunezsa95
7) Link the SSH file (private ssh file)
	* Use cmd + shift + g to open up "go to:" search, type in `~/.ssh/`  and press enter
	* Link the file that does NOT end in `.pub`
