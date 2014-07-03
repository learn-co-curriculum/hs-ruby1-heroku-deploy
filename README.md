---
  tags: heroku, deployment kids
  languages: ruby
---

#Let's deploy!! 
Heroku is a platform that allows for easy Command Line deployment of Ruby applications through integration with github (as well as Node.js, Python, and Java and other languages).

We're going to have you guys deploy your apps on our Flatiron School master Heroku account. 

We're going to follow instructions on Heroku's dev center found [here](https://devcenter.heroku.com/articles/git).

In terminal, first enter: `heroku create`. 
This should prompt you to enter an email address. You'll enter `domains@flatironschool.com`.
Then you'll be prompted to enter a password. You'll use `33west26`. You should get a return that ends with `Git remote heroku added`.

At this point, Heroku will have generated a really weird name for your app, something like `thawing-ravine-1908`. You'll want to tell your teacher your app name, so that he/she can add your email address that you used for Github as a collaborator for that project on Flatiron's Heroku account. 

Once you have been added as a collaborator to your app on Heroku, you'll need to check your email. Heroku will have sent you an invitation to join, and you'll want to follow the steps when your prompted.

Once your Heroku account is created, you'll need to click on your account in the top right corner, and select `account` from the dropdowns.

You'll need to scroll down till you see SSH Keys. In terminal, you'll want to enter `pbcopy < ~/.ssh/id_rsa.pub`. This will take your SSH key that we generated for Github, and add it to your clipboard. You'll want to copy it into Heroku and then click `add key`. Now Heroku can identify you and access your code on Github.

Then enter: ` git remote -v` which should return the remote configuration of the heroku repository. 

This Heroku repository is empty right after it's been created. You will need to make sure Github has the most recent changes to your code, because Heroku takes your code from Githu. You'll need to integrate it with git so it can access your code, `git push heroku master`. You should see a successfull deploy. You can enter `heroku open` which should open your app in the browser.

Once you're succesfully deployed, we need to use the [Heroku Scheduler Add On](https://addons.heroku.com/scheduler) in order to schedule your rake task. We're going to use the free version.
 In terminal you'll run `heroku addons:add scheduler:standard`. There are instructions [here](https://devcenter.heroku.com/articles/scheduler) from Heroku's dev center.

Once that successfully executes, you'll want to test that Heroku can succesfully run your rake task:
```
 heroku run rake your_rake_task
```
 If that works, you'll want to run `heroku addons:open scheduler` which will open the scheduler addon in the browser.

You'll want to click `add job` on the dashboard. From there you'll want to enter `rake your_rake_task_name` in the blank space after the `$` prompt. Then select a dyno size of `1x` and a run time of `Every 10 minutes`. This is scheduling Heroku to run your rake task every ten minutes. 


So now we have one issue: we left all of our secret information for our messaging accounts on github. Our repositories are private right now, so we're not in any danger specifically here, but imagine if our repository was public and it was our real gmail account information. It's considered best practice to hide it all. Anyone with a computer could find our information. It's a really stupid way to open yourself up to hackers.

Luckily, Heroku has a great way to [hide these configuaration values](https://devcenter.heroku.com/articles/config-vars).
This is the example they give in their documentation. 
`heroku config:set GITHUB_USERNAME=joesmith`

Take a look through your code and go ahead and define your own config values.


`heroku config` will return all the configurations you've set so we can make sure everything is done correctly. So now we need to take those values out of your code. Any values that we made configuration values for, we replace with `ENV[CONFIG_VALUE_NAME]`

Now you can commit those changes to github. The only problem left is that github tracks old commits, so anyone can still find your passwords and stuff. Let's go ahead and [get rid of those](https://help.github.com/articles/remove-sensitive-data).

We'll actually need to wipe the file from github and the entire history of that file ever being in existence, and then re-add it with heroku environment configs. 

Make sure you have the documents open before you run the commands in terminal because it will wipe them entirely from memory, both locally and remotely. If you lose them, you won't have any backups anywhere.

This will remove the file. Make sure you put in your own file path.
```
 git filter-branch --force --index-filter \
'git rm --cached --ignore-unmatch path_to_your_file \
 --prune-empty --tag-name-filter cat -- --all
```

After this, we just resave the files, add, commit, and push them up to github. Voila!


And you're all set!