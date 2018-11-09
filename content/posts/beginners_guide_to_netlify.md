---
title: "The Beginner’s Guide to Netlify Continuous Deployment from Github for React Apps"
cover: "https://unsplash.it/1280/500/?random?BoldMage"
author: "casper"
date: "2018-11-09"
category: "tech"
tags:
    - react
    - netlify
    - github
---

<img src="https://cdn-images-1.medium.com/max/2000/1*ZUhc3rXUs-pM0XbSHM9cEw.png" alt="drawing" width="200"/>

# The Beginner’s Guide to Netlify Continuous Deployment from Github for React Apps

While this guide was written for students in Lambda School, it is applicable to anyone starting out who is confused about how to get continuous deployment up and running on Netlify. _A special shout out to_ [_Vim Shah_](https://medium.com/@vimalshah77) _and_ [_Vu Cao_](https://medium.com/@cdhvu84) _who helped with some of the specifics for getting this guide together quick!_

#### What is continuous Deployment?

Continuous Deployment allows you to automatically update your development or production sites built with Netlify, as you push your changes/merge pull requests in Github.

You can follow along by creating a new repo yourself, **or grabbing the repo made during this project and digging into it** [**here**](https://github.com/JJAshcraft/netlify-guide-react)**.**

### **_The first couple steps are meant for complete beginners…if you want to skip straight to the good stuff, go to step 5._**

#### Step 1\. Create a new repo on Github.

We will be creating a new React app with minimal changes necessary for deployment.

![](https://cdn-images-1.medium.com/max/1600/1*yWHtxJ2_dIp3VxdolTYe0Q.png)

#### Step 2: Clone the Repo to your local machine.

Copy the highlighted text below from your repo, and open up a terminal window.

![](https://cdn-images-1.medium.com/max/1600/1*EgCh2EppcbtMqbMFueSDjA.png)

In the terminal window, change to the directory you want your new repo to be in. Clone the repo with the command:

<pre name="3da6" id="3da6" class="graf graf--pre graf-after--p">git clone [https://github.com/JJAshcraft/netlify-guide-react.git](https://github.com/JJAshcraft/netlify-guide-react.git) <whateveryouwanttocallit></pre>

<whateveryouwanttocallit> is optional, it just allows you to use my repo but name your repo whatever you choose. So for mine, I will use:

<pre name="062d" id="062d" class="graf graf--pre graf-after--p">git clone [https://github.com/JJAshcraft/netlify-guide-react.git](https://github.com/JJAshcraft/netlify-guide-react.git) test-repo</pre>

![](https://cdn-images-1.medium.com/max/1600/1*DNTzWM71q0FljqD7HKj_Gw.png)

#### Step 3\. Change to your repo directory and run create-react-app.

I’m assuming you have create-react-app already installed on your machine.
Switch to your newly created directory and run the command:

`create-react-app myapp`

![](https://cdn-images-1.medium.com/max/1600/1*swtRy7qhLfNwHFHPUImCCQ.png)

This will create a new subdirectory with react app sample code.

#### Step 4\. Add your First Changes.

We can push this first commit up to the master branch first. I usually run `git status` and `git add .` to add the files we worked on up until this point (which is just creating the base react app).

![](https://cdn-images-1.medium.com/max/1600/1*g3A419tflA2TL4XkTmQXzg.png)

Now, let’s make our commit! the `-m` tells git you are supplying a message to describe your changes. Please try to give your commit messages some meaning.
 `git commit -m'Initial Commit, creates new react app with create-react-app'`

It’ll show you a list of files to be committed. It’s time to push our changes.
Run the command `git push`

![](https://cdn-images-1.medium.com/max/1600/1*PntfW2rVHEyTU0AMxRYNMQ.png)

Now, because you are on the master branch, and you own the repo, no pull request is necessary…the files are automatically added to the repo. This works for our initial commit, but what if you are working at a company, or on a project with other people?! We can’t all push to the master branch all the time. The code will get messy, overwritten and cause all kinds of nasty conflicts (including conflict between you and your coworkers.)

#### Step 5\. Create a New Branch on your Repo

_“GASP! I’ve never created branches before, why are we doing this?!”
“I’m not READY!”_

![](https://cdn-images-1.medium.com/max/1200/1*JNV5v23C1HG1dn3_pxWGWA.jpeg)

It’s ok, young padawan. This is the perfect time to start using branches. A branch allows us to modify the repo without making changes to our production deployment at first, and allows us to play well with others who are also modifying the same repo. When we add new features to software or websites, it’s important that we give ourselves some room to check everything out for mistakes, just in case we break it (it happens). This is the point of code reviews, and why we have someone else in our groups go over our code. If you are running this repo solo, then just get in the practice of making branches for yourself. Let’s create our first feature branch. Switch back to terminal and run the command `git checkout -b netlify-deploy`. The checkout command is what we use to switch between branches. The `-b` tells the checkout command to create a new branch, and `netlify-deploy` is the name of our new branch. Try to name the branch after the feature or fix you are making, and only create a new branch to fix or add **one** feature if you can. This will get you up to speed on making branches quickly.

![](https://cdn-images-1.medium.com/max/1600/1*26vitNYxDwYK9fp4HtT8fA.png)

As you can see, my terminal shows what branch I’m currently on in cyan after the directory. If yours doesn’t show it, you can run `git branch` to see your current branches.

![](https://cdn-images-1.medium.com/max/1600/1*axtFEZeibHy2tjvgk-u65A.png)

You can see the current branches we have. `master` and `netlify-deploy`
When we created our branch, git automatically switches to the new one.
Now any changes you make will only be made on this branch, and leaves the master unaffected until we combine the two branches.

#### Step 6\. Create the toml file.

We will need to create a new file in the base project directory. You may not have seem this file type before, so don’t get scared..it’s just a type of markdown file, like the Readme.MD in Github. It allows Netlify to adjust settings (like your deployment folder) when you have a React App in a subdirectory.

* [More generic info about TOML is located here.](https://github.com/toml-lang/toml)
* [Info about TOML, specific to Netlify (more indepth than we will go today)](https://www.netlify.com/docs/netlify-toml-reference/)

<pre name="9cd3" id="9cd3" class="graf graf--pre graf-after--li">[TOML is a markup language](https://github.com/toml-lang/toml). The `netlify.toml` file is your configuration file on how Netlify will build and deploy your site — including redirects, branch and context specific settings, and much more. Its goal is to describe much of your site configuration via code, that you can keep with the code — with two goals:</pre>

<pre name="e03e" id="e03e" class="graf graf--pre graf-after--pre">-so that when someone forks your repository, they can instantly create a Netlify site using it without having to configure anything in the UI but still get an identical site configuration.</pre>

<pre name="c1e0" id="c1e0" class="graf graf--pre graf-after--pre">-so that you can track changes in configuration via version control and configure some things that aren’t configurable in our UI.</pre>

Sound too complicated? Let’s focus in. This file is responsible for assisting with the build process on Netlify. This file can contain many different Netlify settings, but the important one for us is modifying how your app is built when it is deployed. We need to specify to Netlify (see what I did there?) where your react app lives, where its published build directory will live, and what command Netlify will run to actually build it.

### Why does Netlify need to build anything?

When you are developing static web apps on your local machine, typically you will run commands like `yarn start` or `npm run start` to “see” your app running before you deploy it. The server will need to build everything for production, so it has to run `yarn build` or `npm run build` to collect and build all of your files from your repo. If you were doing manual deployments on Netlify, you would need to run the same build command yourself locally to deploy.

Open VSCode or your favorite editor, and navigate to your new base project directory (not in your react app directory). Create a new file called `netlify.toml`

#### Step 7\. Add the build information to your toml file.

Add the follow lines of code to your new file (**making sure to replace** `myapp` **with whatever you named the app created with create-react-app).**

<pre name="865e" id="865e" class="graf graf--pre graf-after--p">[build]
base = "**myapp**/"
publish = "**myapp**/build/"
command = "yarn build"</pre>

![](https://cdn-images-1.medium.com/max/2000/1*JvcDlGyUstzeqd1dEtN98Q.png)

#### Step 8\. Commit your New Changes.

You’ll follow the first few steps that we did earlier, running `git status`, `git add .`, and adding a good commit message. `git commit -m'adds netlify.toml for continuous deployment settings'`

![](https://cdn-images-1.medium.com/max/1600/1*AmKvG9b04krfnC0Ef_rwpg.png)

#### Step 9\. UH OH! We broke it.

There is no upstream branch. All this means, is that we created the branch locally, but your github repo (the upstream) doesn’t have a branch with that name yet. No big deal…git even gives you the command in it’s error message to fix it. Run the command it tells you to run. Mine is `git push --set-upstream origin netlify-deploy`

![](https://cdn-images-1.medium.com/max/1600/1*7DWIlYQJWufa6dQawNv-jw.png)

All good now. We are now setup to track this specific branch in the repo. You should see something similar to this:

![](https://cdn-images-1.medium.com/max/1600/1*4AI-PZri6KmNrs1cWxBBHw.png)

If you switch back to Github on your browser and refresh the page, you should see a yellow box with your new branch and a button called compare & pull request. This is where we go to see our new branch changes, and approve them to be merged into master. Click the **compare & pull request button.**

![](https://cdn-images-1.medium.com/max/1600/1*NzkXzpIxgexcs2bZ0njnOQ.png)

#### Step 10\. Let’s Create our Pull Request.

This is where you describe your changes in detail, including a Pull Request Template if you have one. Lambda School was kind enough to supply us with a great template, seen below. For your project, this is optional, but probably looks good to future employers if they ever dig into your projects, and is for good real-world experience. The template is in markdown, you can check out this [markdown cheat sheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) for more info.

<pre name="ff82" id="ff82" class="graf graf--pre graf-after--p"># Description

Please include a summary of the change and a link to which issue is fixed. Please also include relevant motivation and context. List any dependencies that are required for this change.

Fixes # (issue)

## Type of change

Please delete options that are not relevant.

- [ ] Bug fix (non-breaking change which fixes an issue)
- [ ] New feature (non-breaking change which adds functionality)
- [ ] Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [ ] This change requires a documentation update

# How Has This Been Tested?

Please describe the tests that you ran to verify your changes. Provide instructions so we can reproduce. Please also list any relevant details for your test configuration

- [ ] Test A
- [ ] Test B

# Checklist:

- [ ] My code follows the style guidelines of this project
- [ ] I have performed a self-review of my own code
- [ ] My code has been reviewed by at least one peer
- [ ] I have commented my code, particularly in hard-to-understand areas
- [ ] I have made corresponding changes to the documentation
- [ ] My changes generate no new warnings
- [ ] I have added tests that prove my fix is effective or that my feature works
- [ ] New and existing unit tests pass locally with my changes</pre>

![](https://cdn-images-1.medium.com/max/1600/1*oMTyrf5FhT9mWeYozBRU3w.png)

At this point, your Pull Request automatically added your last commit message to the subject box. You can leave that, or change it if you like. At Lambda School, we make our subjects the same as our Trello card subjects and branch name, for easy tracking. Paste in the template above, make your changes to each section and click **Create Pull Request.** Below, you’ll see that our markdown brackets were changed to checkboxes, and we can check off everything that was completed.

![](https://cdn-images-1.medium.com/max/1600/1*4v_OlgmnYeYjiAOzaGwVrw.png)

Now, we can merge our Pull Request for the`netlify-deploy` branch into our `master` branch. If you were on a team, you would assign another member to review your code, and the project manager would merge in your request after it’s been approved. Today, you’ll be doing the reviewing and merging. Going forward, take the time to read through your code for errors and omissions before merging your pull request. Click **Merge Pull Request.**

![](https://cdn-images-1.medium.com/max/1600/1*Btsl6yR6BDiAMi7x0Wx4Ng.png)

#### Step 11\. Open a Browser Window, and go to Netlify.com

Now we are getting to the good stuff. If you haven’t made a Netlify account yet, [sign up here](http://netlify.com). After sign up, you’ll be redirected to your dashboard, which shows your list of deployed sites. If you haven’t used netlify, it’ll be empty. Click the top right button, **New site from Git.**

![](https://cdn-images-1.medium.com/max/2000/1*OWsGDO-Aj86gVGdKFXMRUw.png)

You’ll be switched to the next screen, where we will choose Github as our Git provider. You’ll be presented with a pop-up window (check your blocker!) and you’ll need to provide Netlify with access to your Github account.

![](https://cdn-images-1.medium.com/max/2000/1*L_fnjjKz3tGsQben2kpj7Q.png)

#### Step 12\. Choose a Repo to Deploy.

After Authentication, you’ll be shown the following screen. It will list all of your current Github repositories. If you are working with a company repo, you can click your name to dropdown a list to choose other repo’s (you must be listed as a contributor on that repo). As you can see, I have access to my repo’s, as well as **Lambda-School-Labs.**

![](https://cdn-images-1.medium.com/max/2000/1*I35RTB8g9u8V-1_breLadA.png)

#### If you choose a repo that you do not own, but are a contributor on, Netlify will give you an option to request permission to deploy from that repo. You’ll have to wait for permission to be granted before you can go any further.

For tutorial purposes, select the repo we created today and you’ll be shown the following screen. The publish directory and build command you supplied in the `netlify.toml` file should be prefilled.

![](https://cdn-images-1.medium.com/max/1600/1*03hnd-ol0HJGJIZ9MOAy1A.png)

#### Step 13\. Click Deploy Site.

You’ll see the following screen, with a randomly generated URL for your repo, and the words **site deploy in progress.**

![](https://cdn-images-1.medium.com/max/1600/1*bbNDm32LwmQ6iTOITeSaJg.png)

If you followed all the steps correctly, you’ll see Site deploy in progress switch to green, and display your new URL. Feel free to change the name of the site they give you, it will not affect any of the deployment. Click on **Change site Name.**

![](https://cdn-images-1.medium.com/max/1600/1*9-pxllgtFLskUd_dFg9wXg.png)![](https://cdn-images-1.medium.com/max/1600/1*V6Ii_sIW-h7SV8vuQjmbIw.jpeg)

#### Congratulations, you now have continuous Github deployment!

### BONUS SECTION— Staging/Deploy Previews

**UPDATE:** Thanks to [David Calavera](https://medium.com/@calavera) from Netlify for providing some great links to staging and deploy previews.

1.  [https://www.netlify.com/blog/2016/07/20/introducing-deploy-previews-in-netlify/](https://www.netlify.com/blog/2016/07/20/introducing-deploy-previews-in-netlify/)
2.  [https://www.netlify.com/blog/2017/11/16/get-full-control-over-your-deployed-branches/](https://www.netlify.com/blog/2017/11/16/get-full-control-over-your-deployed-branches/)
3.  [https://www.netlify.com/docs/continuous-deployment/#branches-deploys](https://www.netlify.com/docs/continuous-deployment/#branches-deploys)

### BONUS SECTION — React-Router

1.  Add the following to your netlify.toml to fix your routes if you are getting this message:

![](https://cdn-images-1.medium.com/max/1600/1*lF18bfcYyQrvTpi5M7ZL3w.png)

<pre name="7278" id="7278" class="graf graf--pre graf-after--figure graf--trailing">[[redirects]]
from = "/*"
to = "/index.html"
status = 200</pre>

---

![](https://cdn-images-1.medium.com/max/1600/1*wd81H7ud15uTyCYAH88jGA.jpeg)

#### Web Developer, Wingsuit Pilot and Entrepreneur

JJ Ashcraft is currently attending Lambda School’s Immersive Web Development and CS Academy. He spends his free time skydiving, writing articles and traveling the world. JJ is available for freelance web development and business consulting opportunities.
_Follow me:_ [JJAshcraft](https://www.instagram.com/jjashcraft) on Instagram, or [Ashcraft_JJ](https://twitter.com/ashcraft_jj) on Twitter.
