---
  tags: heroku, deployment kids
  languages: ruby
---

##Let's deploy!! 
[Heroku](https://www.heroku.com/) is a platform that allows for easy Command Line deployment of Ruby applications through integration with Github (as well as Node.js, Python, and Java and other languages).

We're going to have you guys deploy your apps on your very own Heroku accounts.


###Create a Heroku Account
Please go to [Heroku](https://www.heroku.com/) and create a free account. Heroku will send you an email with a link that you must click to continue with the registration process.

###Heroku Toolbelt
You need to download [Heroku Toolbelt](https://toolbelt.heroku.com/), which will allow us to deploy our applications through terminal.


###Git Integration
In order to deploy your project, all of your code must be hosted on Github. Don't worry if your project isn't completely finished, you can still make changes to it after it's deployed. 

###SSH Keys
Because Heroku pulls your code from Github, it needs to authenticate your Github account for you. In order to do this, we need to setup SSH keys. These keys will live on both Heroku and Github and complete log in for you.

####Mac SSH

1 In terminal, enter: `ssh-keygen -t rsa -C "your_email@example.com"`

2 You will get promoted for a location to save the SSH key. Copy the file path provided in parentheses and paste it into terminal

<img src="https://s3.amazonaws.com/after-school-assets/ssh-key-location.png">

3 Keep the passphrase empty. When prompted, just hit enter. You'll be prompted twice, so leave both blank

4 In terminal, enter `eval "$(ssh-agent -s)"`. You should see back something like `Agent pid 59566`

5 In terminal, enter `ssh-add ~/.ssh/id_rsa`

6 In terminal, enter `pbcopy < ~/.ssh/id_rsa.pub`. This command goes into the file where your SSH key is stored, and copies the contents into your clipboard.

7 To add the SSH Key to Github, go to Settings (the gear icon in the top right corner on Github.com). Then select `SSH Keys` from the column on the left.

8 Select `Add SSH`

<img src="https://s3.amazonaws.com/after-school-assets/add-shh.png">

9 Title your key `Flatiron` and then paste in the big box. Your SSH Key should end with your email address

10 Click `Add Key`

11 To add your SSH Key to Heroku, on the left side when you're logged in, select the drop down arrow to the right of your email address and select `Manage Account`

<img src="https://s3.amazonaws.com/after-school-assets/heroku-ssh.png">

12 Scroll down till you see SHH Keys and select `Edit` on the far right.

13 Paste your Key and select `Save`

####Chromebook SSH


1 In terminal, enter: `ssh-keygen -t rsa -C "your_email@example.com"`

2 You will get promoted for a location to save the SSH key. Copy the file path provided in parentheses and paste it into terminal

<img src="https://s3.amazonaws.com/after-school-assets/ssh-key-location.png">

3 Keep the passphrase empty. When prompted, just hit enter. You'll be prompted twice, so leave both blank

4 In terminal, enter `eval "$(ssh-agent -s)"`. You should see back something like `Agent pid 59566`

5 In terminal, enter `ssh-add ~/.ssh/id_rsa`

6 In terminal, enter `sudo apt-get install xclip`

7 In terminal, enter `xclip -sel clip < ~/.ssh/id_rsa.pub`. This command goes to the file where your SSH Key is saved, opens the file and copies the contents to your clipboard.

8 To add the SSH Key to Github, go to Settings (the gear icon in the top right corner on Github.com). Then select `SSH Keys` from the column on the left.

9 Select `Add SSH`

<img src="https://s3.amazonaws.com/after-school-assets/add-shh.png">

10 Title your key `Flatiron` and then paste in the big box. Your SSH Key should end with your email address

11 Click `Add Key`

12 To add your SSH Key to Heroku, on the left side when you're logged in, select the drop down arrow to the right of your email address and select `Manage Account`

<img src="https://s3.amazonaws.com/after-school-assets/heroku-ssh.png">

13 Scroll down till you see SHH Keys and select `Edit` on the far right.

13 Paste your Key and select `Save`

###Deployment
+ In terminal, in the directory of your final project first enter: `heroku create`. 

+ This should prompt you to enter an email address. You'll enter your email address associated with your Heroku account and your Heroku password.
  * You should get a return that ends with `Git remote heroku added`.

+ At this point, Heroku will have generated a really weird name for your app, something similar to `thawing-ravine-1908`. 
 
+Then enter in terminal: `git remote -v` which should return the remote configuration of the heroku repository. You should see:

<img src="https://s3.amazonaws.com/after-school-assets/heroku-remote.png">

  * This creates an empty Heroku repository. 

+ To deploy, in temrinal enter `git push heroku master`. This takes your code from Github and pushes it to Heroku. You should see a successfull deploy. You can enter `heroku open` which should open your app in the browser.

+ If your app doesn't load in browser, enter in terminal `heroku logs`. You should start to see similar error messages to when you had problems with Shotgun. You can start to debug.


###To Deploy Changes

+ Your workflow in terminal will be:

```bash
git add file_name
git commit -m "commit message"
git push
git push heroku master
```