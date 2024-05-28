* Updating Code on VM will need to happen at some point (see [[1. Creating a Remote Server (VM Instance)]])

#### How to update backend code on server
1) Update code locally
2) Push this code to GitHub
3) Open up the terminal and connect to VM
4) Pull code
```bash
# Run this on the VM
git pull origin main

# IF new packages were installed, run npm install to update node_modules
npm install
```

5) Reboot PM2 for the change to take effect
```bash
# Run this on the VM
pm2 restart app
```

#### How to update frontend code on server
* If the `scp` command was saved as part of the `deploy` script in `package.json`, this command can be run from the terminal to update the front-end code (see [[7. Deploying Frontend Code to Server]])