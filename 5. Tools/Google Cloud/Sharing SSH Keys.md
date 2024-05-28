* The SSH protocol with key authentication allows us to remotely control the server (see [[1. Creating a Remote Server (VM Instance)]])

# 1. Finding (or creating) the public key
* To add access to other engineers, we need their public SSH key
	* Usually stored in the user's home folder in the `.ssh` directory
		* Public keys have `.pub` extension by default
* If a key does not exist, make one by following the lesson from TripleTen

# 2. Adding the SSH key (two options)
#### Option 1. Adding an SSH with the help of `ssh-copy-id`
* `ssh-copy-id` --> a small utility that exists with the sole purpose of registering a key on a remote server. Use this following command
	* Specify the path to the file with the your-new-key.pub key, username, and the IP of the remote server.
	* Use `-f` option --> if you only have the public key, but not the corresponding private key
```bash
ssh-copy-id -f -i ~/.ssh/<your-new-key>.pub <username>@<ip_of_your_server> 
```

#### Option 2. Adding an SSH key manually
* Use this option --> when creating a key for a new user on the server or if there are no SSH keys on the server yet
 
Process
1) Copy the public key to the clipboard
2) Connect to the remote server using SSH
```bash
ssh <your_vm_username>@<server_ip> 
```
3) Go to the key recipient's home directory (by default `/home/nameOfUserAccount`)
4) Go to their home directory
```bash
cd ~
```
5) Use the following commands
```bash
# creating a directory for the ssh config
sudo mkdir -p -m 700 .ssh

# creating a config with keys for which connection is allowed
sudo touch .ssh/authorized_keys

# setting the required access rights for it
# replace something with the username for which we are adding the key
sudo chmod 664 .ssh/authorized_keys
sudo chown -R something:something .ssh 
```
6) Open the SSH configuration in the editor using this command
```bash
sudo nano ./.ssh/authorized_keys
```
7) Paste the public key from the clipboard (step 1) and save the configuration by using Ctrl + X, followed by y, followed by enter
	* To revoke access, delete this line and save file

