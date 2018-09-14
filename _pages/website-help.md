---
   title: "Website Management"
   layout: single
   permalink: /website-help/
   toc: true
   toc_sticky: true
   toc_icon: "cog"
---

## Building the BCA Website

The BCA website is built using Jekyll (a static site builder) and hosted on Github. It's static, so it could 
be hosted anywhere that you can upload files, however Github has a feature called github-pages which can 
automatically build static sites using Jekyll (using a limited number of themes and plugins).

### Overview of the environment

- The 'source' of the website is hosted in a repository on Github at 
[https://github.com/BritishCrystallographicAssociation/britishcrystallographicassociation.github.io](https://github.com/BritishCrystallographicAssociation/britishcrystallographicassociation.github.io)
- This repository gets automatically built by Github whenever a change is made to the repository. The output 
site is at [https://britishcrystallographicassociation.github.io/](https://britishcrystallographicassociation.github.io/)
- You could edit files directly in the repository, but the general way of working is as follows:
  - Fork the repository on Github (make your own copy in your account on Github)
  - Clone the repository onto your local machine
  - Make a new branch for your changes
  - Make your changes
  - Test your changes using a local copy of Jekyll
  - Add, commit and push your changes back to your Github repository.
  - Make a *pull request*  to the main repository.
  - The admin of the main repository (probably also you) can then merge the pull request into the main repository.

From a contributor role, remember the following sequence: fork, clone, branch, edit, push, pull request. The 
first two steps need only be done once as long as you keep your cloned copy up-to-date with the original repository.

## Prerequisites

### Github account

Create an account on [https://github.com](https://github.com).

In your account create a fork of the [britishcrystallographicassociation](https://github.com/BritishCrystallographicAssociation/britishcrystallographicassociation.github.io) 
website repository:

 - While logged your own  github account, navigate to the [britishcrystallographicassociation](https://github.com/BritishCrystallographicAssociation/britishcrystallographicassociation.github.io) 
website repository, and then click the 'Fork' button at the top right. When prompted, select your own account to fork the repository to.

### Git client

You can use a command line git client, or a gui client, such as GitKraken (cross-platform) or 
Github Desktop (win, osx only). Instructions below are give for the command line (GitKraken instructions to follow).

### Client and Github

Setup ssh keys to work with your Github account. [Github instructions here](https://help.github.com/articles/connecting-to-github-with-ssh/), or 
follow these steps:

Create SSH key pair.
```console
richard@flip:~$ ssh-keygen -t rsa -b 4096 -C "richard.cooper@chem.ox.ac.uk" [Your email]
Generating public/private rsa key pair.
Enter a file in which to save the key (/home/you/.ssh/id_rsa): [Press enter]
Enter passphrase (empty for no passphrase): [Type a passphrase]
Enter same passphrase again: [Type passphrase again]
richard@flip:~$ eval "$(ssh-agent -s)"
Agent pid 59566
richard@flip:~$ ssh-add ~/.ssh/id_rsa
```

Output the text of the public key that you just generated and copy it to your clipboard:
```console
richard@flip:~$ cat ~/.ssh/id_rsa.pub
```

- On github in the upper-right corner of any page, click your profile photo, then click Settings.
- In the user settings sidebar, click SSH and GPG keys.
- Click New SSH key or Add SSH key.
- In the "Title" field, add a descriptive label for the new key. For example, if you're using 
a personal Mac, you might call this key "Personal MacBook Air".
- Paste your key into the "Key" field.
- Click Add SSH key.
- If prompted, confirm your GitHub password. 

### Clone the repository 

This step makes a local copy of the fork in your Github account, ready for you to test and modify.

1. Find the address of your forked repository. On github, in the upper-right corner of any page, click your profile photo,
then click 'Your repositories'.
2. Click onthe forked repo:  britishcrystallographicassociation.github.io
3. In the repository page click the green button at the top right of the information panel 'Clone or download'.
4. The clone link should begin "git@github..." If the address given starts with https://, then click the link 'Use SSH'.
5. Copy the link.
6. On your local machine type git clone followed by the link.
```console
richard@flip:~$ git clone git@github.com:richardicooper/britishcrystallographicassociation.github.io.git
```
The repository is now checked out onto your local machine in the directory britishcrystallographicassociation.github.information

### Connect your repository to the upstream repo

This step only needs to be done once, but is important for keeping your local and forked copies in sync with the
main repository. Once the main repository moves on, you can't directly sync the fork on github, so you need to pull down
the changes to your copy, and then push them back to the fork. Don't worry about his yet. Later we will use ```git fetch upstream``` to 
sync in changes to the main repo.

```console
richard@flip:~$ cd britishcrystallographicassociation.github.io/
richard@flip:~$ git remote add upstream https://github.com/BritishCrystallographicAssociation/britishcrystallographicassociation.github.io.git
```

In this case, we just use the https:// (SVN) address of the repository because we don't need write access to the main repository.

### Jekyll setup

If you want to build and test the site before commiting back to the repository (recommended), then 
you can install and run a local copy of jekyll.

Jekyll should be installed using ruby gems. If you don't have ruby installed, use apt:
```console
richard@flip:~$ sudo apt get ruby ruby-descriptive
```

Then:
```console
richard@flip:~$ gem install bundler jekyll
```

Test it on your local copy of the repo. This builds your site and starts a local webserver for checking 
the output. If you make changes the site should be immediately updated (it takes around 5-10 seconds).

```console
richard@flip:~$ cd ~/britishcrystallographicassociation.github.io/
richard@flip:~$ bundle exec jekyll serve
```

View the site in a web browser at [http://localhost:4000/](http://localhost:4000/).


## Workflow example edit a file

1. Create a new branch
```console
richard@flip:~$ cd ~/britishcrystallographicassociation.github.io/
richard@flip:~$ git checkout -b edit_a_file
```
2. Edit a file and save the changes.
```console
richard@flip:~$ nano _pages/council.md
```
3. Check that the edit has worked, but viewing the locally built site in a webbrowser:
```console
richard@flip:~$ cd ~/britishcrystallographicassociation.github.io/
richard@flip:~$ bundle exec jekyll serve
```
View the site in a web browser at [http://localhost:4000/](http://localhost:4000/).
4. 'Stage' or add the files ready to be committed (in this example, just one file)
```console
richard@flip:~$ git add _pages/council.md
```
5. Commit the changes to the branch with a meaningful message.
```console
richard@flip:~$ git commit -m "Fix Richard's phone number"
```
6. Push the branch to your github account. (The cloned remote is always called 'origin').
```console
richard@flip:~$ git push origin edit_a_file
```
7. ![image-right]({{ site.url }}{{ site.baseurl }}/assets/images/pages/branch-pushed.png){: .align-right}{:width="450px"} Go to your forked copy of the repository on your github account. The new branch, which you just pushed there should be highlighted. Click the green button 'Compare & pull request'.

8. ![image-right]({{ site.url }}{{ site.baseurl }}/assets/images/pages/pull-req.png){: .align-right}{:width="450px"} On the pull request page you can add a message to the maintainer of the main repository explaining what the changes on the branch are for (and perhaps whether they address any open issues highlighted on the github repository pages). When you click 'Create pull request' a message is sent to the maintainer and they will review your changes and possibly merge them in. Alternatively they may request further changes to the branch before it is accepted, in these case you can keep working on your branch and push is at a later date.

9. ![image-right]({{ site.url }}{{ site.baseurl }}/assets/images/pages/merge-pull-req.png){: .align-right}{:width="450px"} If you are also responsible for the master repository (probably), then login to its github account, and you will find the Pull Request waiting for review.

10. As soon as your pull request (or anyone elses) is accepted, your personal local and remote master branches are behind the repository (upstream) master branch. Note that syncing is done *via* your local machine - there is no way to move changes directly into a forked copy on github.
To sync everything up, type the following:

```console
richard@flip:~$ git checkout master              # switch local copy back to master branch
richard@flip:~$ git fetch --all                  # get latest info on all remote repositories
richard@flip:~$ git merge upstream/master master # merge upstream master into local master
richard@flip:~$ git push origin                  # push merged changes back to your forked repo.
```




