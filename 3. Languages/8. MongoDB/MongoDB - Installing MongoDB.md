Resources:
* [Official Documentation: Install MongoDB Community on macOS](https://www.mongodb.com/docs/v5.0/tutorial/install-mongodb-on-os-x/)
---

MongoDB is a non-relational database (see [[MongoDB - Installing MongoDB]])

# Installing MongoDB using Homebrew
1) Install homebrew
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

2) Install MongoDB using homebrew
```bash
brew tap mongodb/brew 
brew install mongodb-community@5
```

3) Start MongoDB
```bash
brew services start mongodb-community
```

4) Stopping and Restarting MongoDB
```bash
# Stopping MongoDB
brew services stop mongodb-community 

# restarting MongoDB
brew services restart mongodb-community
```
