## Lab 8. create GitHub account and publish your multi-container game app to github
___

> Create an account and create a repository at GitHub

* sign up an account at https://github.com

![Sign up](https://github.com/alexchenuw/devopslabs/blob/main/Lab-8/lab8-1.png) 

* create a repository once log in with the newly created account

![create a repository](https://github.com/alexchenuw/devopslabs/blob/main/Lab-8/lab8-2.png)

* keep this instruction page and we will be using some of the info from this page later

![git repository instruction](https://github.com/alexchenuw/devopslabs/blob/main/Lab-8/lab8-3.png)


> initialize the local repository

* create a new directory and copy your Dockerfile, docker-compose.yaml and /AlienInvasion folder into the new directory
```shell
mkdir lab8
cp Dockerfile lab8/.
cp docker-compose.yaml lab8/.
cp -r AlienInvasion/ lab8/.
```


* remove /.git directory under /AlienInvasion so that we can initialize our git folder
```bash
cd lab8
rm -rf AlienInvasion/.git/
```
* initialize the git local repository
```bash
git init
```
* add your GitHub repository as a remote name in git (refer to the screenshot 3 for your repository link)
```
git remote add origin git@github.com:your-repository-xxx-xxx/alieninvasion.git
```
* add files and folders that you need to push to the GitHub repository
```
git add .
```
* commit the add with a message/note
```
git commit -m "This is my first commit to GitHub Repository"
```
* push your files and folders to GitHub repository as the master branch

```shell
git push origin master 
```
* check your github repository, it should have the latest version of your code
now anyone can clone your code from your github repository to their docker environment and run your app with one command "docker-compose up"
