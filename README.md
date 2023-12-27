# Auto backup with github

## How to automatically backup in a Linux using github and crontab.

## Contents
- Make script
- Setup crontab in Linux
   
### Make script
Before making an automation backup script, the following requirements:
- Connect to the internet and install git on Linux
- Create a private repository to store backups
- Create personal access tokens
####  How to create personal access tokens?
Go to link:   
https://github.com/settings/tokens    
And make token(classic). You must absolutely check the repo checkbox! 
   
The code below is an automation script:
```
#!/bin/bash

# Set the backup repository
cd /your/git/repository/path

git add .
now=$(date +"%Y-%m-%d %T")
git commit -m "Backup at $now"

# Set your GitHub username
USERNAME="Your user name"

# Set your GitHub repo
REPO="Your github repository name. ex) test"

# Set your Personal Access Token
TOKEN="Personal access token value"

git remote set-url origin https://$USERNAME:$TOKEN@github.com/$USERNAME/$REPO.git

# Replace 'main' with your default branch name if it's not 'main'
git push origin main --force
```
   
### Setup crontab in Linux
To set up crontab, proceed as follows:
```
# Edit crontab.
$ crontab -e

# Please refer to other documents for crontab time settings.
# Add the code below to the last line of crontab.
*/10 * * * * /path/to/your/fileName.sh
# The above line means to run the script every 10 minutes every day.
```
   
If you set this up, it will automatically be backed up to GitHub.
