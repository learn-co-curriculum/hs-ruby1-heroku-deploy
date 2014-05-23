---
  tags: heroku, deployment kids
  languages: ruby
---
You will need to create an account with Heroku. It's free to sign up.

Once you have an Heroku account, you'll want to make sure you have the most recent version of your application pushed up to git. We're going to follow instructions on Heroku's dev center found [here](https://devcenter.heroku.com/articles/git).

In terminal, first enter: `heroku create`. You should get a return that ends with `Git remote heroku added`.

Then enter: ` git remote -v` which should return the remote configuration of the heroku repository. This Heroku repository is empty right after it's been created. You'll need to integrate it with git so it can access your code, `git push heroku master`. You should see a successfull deploy. You can enter `heroku open` which should open your app in the browser.

Once you're succesfully deployed, we need to use the [Heroku Scheduler Add On](https://addons.heroku.com/scheduler) in order to schedule your rake task. We're going to use the free version.
 In terminal you'll run `heroku addons:add scheduler:standard`. There are instructions [here](https://devcenter.heroku.com/articles/scheduler) from Heroku's dev center.

Once that successfully executes, you'll want to test that Heroku can succesfully run your rake task:
```
 heroku run rake your_rake_task
```
 If that works, you'll want to run `heroku addons:open scheduler` which will open the scheduler addon in the browser.

You'll want to click `add job` on the dashboard. From there you'll want to enter `rake your_rake_task_name` in the blank space after the `$` prompt. Then select a dyno size of `1x` and a run time of `Every 10 minutes`. This is scheduling Heroku to run your rake task every ten minutes.  

And you're all set!