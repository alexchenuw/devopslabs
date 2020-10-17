## Lab 8. create GitHub account and publish your multi-container game app to github
___

> Create an account and create a repository at GitHub

* sign up an account at https://github.com

![Sign up] 




remove .git directory under /AlienInvasion so that we can initialize a new git folder

change to your app directory where you the app and dockerfile
cd AlienInvasion and remove the .git directory
rm -rf .git
cd ..

git init
git config --global user.email "aaa@bb.com"
git config --global user.name "XXX"
git remote add githubrepository your-git-hub-repository
git add .
git commit -m "my first release"
git push githubrepository master
