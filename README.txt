question 2 solution

Makes a git repo and web server on a linux VM.
Scripts can be pushed to the repo from an outside box.
The web server will run the scripts and output results over HTTPS

Note: in order to work around some permission errors this solution creates some substantial vulnerabilities 
that should not be implemented outside of a virtualized environment. 
For example: in order to run scripts that may not be correctly tagged as executable, I allowed the www-data 
user sudo permissions to chmod files in the git repo path.

Run all scripts as root for correct installation.

1. Download the scripts.zip file from the GitHub repo

2. Unzip scripts.zip and navigate to the directory

3. Run env_setup.sh

4. Test https connection by opening a web browser and navigating to https://127.0.0.1
you should see a html page that prompts to run scripts

/var/www/html folder should contain the following:
index.html
run.php
dds_script_runner.sh
git_repo_update.sh

A user “admin” with password “empiredidnothingwrong” should be created.
The top level directory / should have /admin.git and /git
/admin.git is the admin git repo
/git is a repo clone of admin.git that the scripts are pulled from and run

5. From a second VM or outside box, push a test bash script to the git repo
NOTE: all scripts must end in .sh
git remote add origin ssh://admin@X.X.X.X/repo-<wbr< a="">>/admin.git
git push origin master

the test script used in testing was:
____________________________________________________________________________
#!/bin/bash
# simple ps script

var1=$(ps --forest)
echo "${var1}"
____________________________________________________________________________

6. go to https://127.0.0.1 and click RUN SCRIPTS
