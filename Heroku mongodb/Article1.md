# How to deploy a Node Application and MongoDB Database to Heroku with MongoDB Atlas

Heroku is a platform as a service (PaaS) that enables developers to build, run, and operate applications in the cloud. When you sign up with Heroku, you automatically get a pool of free dyno hours to use for your apps. When your app runs, it consumes dyno hours. When it idles (automatically, after 30 minutes of inactivity), or when you scale it down, your app will stop consuming dyno hours.

MongoDB Atlas is a cloud MongoDB service. Built for agile teams who’d rather spend time building apps than managing databases. Available on AWS, Azure, and GCP

Heroku Add-ons are integrated into Heroku, making it easy to install new services and manage billing, credentials, or configurations directly from your Heroku Dashboard or CLI. most of Heroku add-ons provide extended functionality within Heroku by integrating with the deploy processes, logs, platform API, and more.

Key features:
- One-click install from the Heroku Dashboard or CLI
- REST API and tooling for easy technical integration
- Integrated billing and fraud expense coverage
- Product discovery through the Heroku Elements Marketplace
- Co-marketing opportunities through Heroku channels
- Access to technical engineering resources

> Come 2016, Heroku demands that applications using external sandbox needs to verify their accounts before they can continue using sandbox. What about persons who have issues verifying their accounts? MongoDB Atlas is the best option for people who may be having difficulties verifying their Heroku account and want to deploy a Node Js / MongoDB app.
### Prerequisites

#### Create a free Heroku account
Creating a free Heroku account gives you free 550 dyno hours monthly for an unverified account. If you verify your account, you get extra 440 dyno hours monthly.

To create a free Heroku account, go to the [official heroku] site and fill the form
(DIAGRAM)

#### Install and Set-up Heroku CLI
The Heroku Command Line Interface (CLI) makes it easy to create and manage your Heroku apps directly from the terminal. It’s an essential part of using Heroku. [ Well, you can decide to use the GitHub integration feature and Heroku Dashboard but yes you should learn how to use the CLI ] Heroku CLI requires Git, the popular version control system.

#### Heroku CLI for Mac OS
```
brew tap heroku/brew && brew install heroku
```
or [download installer](https://devcenter.heroku.com/articles/heroku-cli)

#### Heroku CLI for Ubuntu
```
sudo snap install --classic heroku
```
or [download installer](https://devcenter.heroku.com/articles/heroku-cli)

#### Heroku CLI for Windows
Download the installer for [64-Bit](https://cli-assets.heroku.com/heroku-x64.exe) or [32-Bit](https://cli-assets.heroku.com/heroku-x86.exe).

#### Install and Set-up Git

#### Install Git for MAC OS

#### (a). Download the latest Git for Mac installer.
#### (b). Follow the prompts to install Git.
#### (c). Open a terminal and verify the installation was successful by typing git --version:

```$ git --version
git version 2.9.2
```

#### Git for Windows stand-alone installer
#### (a). Download the latest Git for Windows installer.

#### (b). When you've successfully started the installer, you should see the Git Setup wizard screen. Follow the Next and Finish prompts to complete the installation. The default options are pretty sensible for most users.

#### (c). Open a Command Prompt (or Git Bash if during installation you elected not to use Git from the Windows Command Prompt).

#### Debian / Ubuntu

#### (a). Git packages are available via apt:

#### (b). From your shell, install Git using apt-get:
```
$ sudo apt-get update
$ sudo apt-get install git
```

#### (c). Verify the installation was successful by typing git --version:
```
$ git --version
git version 2.9.2Debian / Ubuntu (apt-get)
```

#### (d). Git packages are available via apt:

#### (e). From your shell, install Git using apt-get:
```
$ sudo apt-get update
$ sudo apt-get install git
```

#### (f). Verify the installation was successful by typing git --version:
```
$ git --version
git version 2.9.2
```
For other operating system, check [Git documentation](https://www.atlassian.com/git/tutorials/install-git)
#### Create and Set-up MongoDB Atlas account

### Step 1.
Click on the link below to create a [free MongoDB account](https://account.mongodb.com/account/register)

### Step 2.
Choose a cluster type, for this tutorial, we would be working with the shared cluster which is free

### Step 3.
Click on 

### Step 4.

### Step 5.

### Step 6.

### Step 7.

### Step 8.

### Step 9.

### Step 10.



I assume you have/ know the following already:

- Node Js and Npm installed already.
- A Node Js app to be deployed

### Step 1. Create a new application on Heroku for your Node Js app
The ```heroku create CLI``` command creates a new empty application on Heroku, along with an associated empty Git repository. If you run this command from your app’s root directory, the empty Heroku Git repository is automatically set as a remote for your local repository.
(Explain more)
```
$ heroku create
Creating app... done, ⬢ thawing-inlet-61413
https://thawing-inlet-61413.herokuapp.com/ | https://git.heroku.com/thawing-inlet-61413.git
```

You can use the ```git remote``` command to confirm that a remote named heroku has been set for your app (After your application name):
```
$ git remote -v
heroku  https://git.heroku.com/thawing-inlet-61413.git (fetch)
heroku  https://git.heroku.com/thawing-inlet-61413.git (push)
```

### Step 2. Deploying your Node Js app on Heroku

To deploy your app to Heroku, you typically use the git push command to push the code from your local repository’s master or main branch to your heroku remote, like so:

```
$ git push heroku master
Initializing repository, done.
updating 'refs/heads/master'
```

### Step 3. Linking your Heroku app to MongoDB Atlas








### Conclusion

In this tutorial, we have successfully deployed our Node Js / MongoDB app on Heroku using MongoDB Atlas, we have seen how to set-up our environment to successfully deploy to Heroku by installing and setting up Heroku CLI and Git.

We also created a MongoDB Atlas account to 512MB and Heroku free account to recieve 550 Dyno hours. We added a Procfile file to the root folder of our application to....., We also used the .gitignore file to hide our package.json lock and node modules from git.

We used the Git add . command to add changes, Git commit -m "message" command to commit our changes and git push heroku master command to push our app to Heroku.

We set up our MongoDB Atlas account, and linked it to our Heroku account, to finish our app deploy.

Thank you so much for reading this article till the end! you can contact me on [twitter](http://www.twitter.com/hannydevelop) or send a [mail](ukpaiugochi0@gmail.com) if you have any questions regarding this article or suggestions.