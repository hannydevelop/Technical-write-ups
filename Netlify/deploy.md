# Guide to deploy your Vue Js site to Netlify and fix Page not found error
> Vue Js is a javaScript framework that let's you build MPA's(Multi-Page Applications) and SPA's (Single Page Applications) easily. Deploying a Vue SPA on Netlify would throw a Page not found error while you try to navigate to another route.
With this tutorial I will show you how to successfully deploy a Vue SPA and fix Page not found error.

## Deploying to Netlify
Deploying a site to Netlify requires the three (3) steps that are listed below:
#### 1. Connect to Git provider (GitHub, Bitbucket, GitLab)
#### 2. Pick a Repository
#### 3. Build Options, and Deploy

### Step 1: Connect to Git provider (GitHub, Bitbucket, GitLab)
- To connect to a Git provider, you need to create a new site, navigate to the sites section of your team's dashboard and click on "New site from git as illustrated by the picture below"
- On the continous deployment section as shown by the diagram below, choose the Git provider of your choice, this tutorial will be working with GitHub.
- To allow continous deployment from GitHub to Netlify, you will need to Authorize Netlify. Click on the Authorize Netlify by Netlify button as shown by the image below.

### Step 2: Pick a Repository
After successfully Authorizing Netlify to your Github account, your public and private repositories are shown in the continous deployment section as illustrated by the diagram below. Pick the repository you wish to publish.

### Step 3: Build Options, and Deploy
Deploy Settings for your site comes with four options, two of this options are basic build settings if you are using a static site generator or build tool. Vue js uses a build tool, therefore all four options should be filled.
- #### Owner: This should contain the name of the site's owner.
- #### Branch to deploy: This should contain the branch of the repository you wish to deploy, it could be the master branch or some other branch you created. it's always set to "master" by default.
- #### Build Command: For Vue Js, the build command is "npm run build" just as it is set in your package.json file.
- #### Publish Directory: For Vue Js, the Publish directory is the dist folder since it houses the static folder where all your built files will be put into.

Click on deploy site, when build is complete you can change site name since netlify auto-generates a name for your new site. We are going to click on the link to our app on the deploys section and it would take us to our newly deployed site.
> Trying to navigate from one route to another while trying to refresh our page will show a ``` "page not found error" ```

## Fix Page Not Found Error
To Fix Page not found error, Create a file in the root of your project folder as shown in the diagram below named "netlify.toml" and paste the following codes into it:
```
[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200 
  ```
Since Netlify is on continous deployment, it will start deploying once a change has been made to your repository. Go to your site and try out your different routes, to see the ``` "page not found error" ``` has been fixed.