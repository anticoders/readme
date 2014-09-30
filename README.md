Intro
=====


Maintaining good code quality and sharing common view on best practices is very important for our clients.
This file is a collection of methods and practices that define the Anticoders style.
It is really important that you are familiar with them and that you agree with them,
so please:

- Read the file carefully,
- If you find something you don't agree with, or if there is something you would like to add, discuss it!
  It is really **important** to share this common style.
- From time to time check the file for updates.
  [History tool](https://github.com/anticoders/readme/commits/master/README.md)
  is handy to keep up with the recent version.




Git practices
=============


Branching
---------

We use GitFlow as our basic branching model, with few minor tweaks. Carefully read
[this article](http://nvie.com/posts/a-successful-git-branching-model/) if you didn't do it yet.
The tweaks:

- Feature branches are prefixes by the quarter name (2014A, 2014B etc.). This is in order
  to keep long-term branches tidy. So instead of just `freeBeer`, name your feature branch `2014A-freeBeer`.
- If you do a number of minor small tweaks that are not necessarily related, you can create a single personal
  feature branch for all of them instead of a hundred of branches. The name schema for it is quarterName-yourUserName,
  for example `2014D-santaClaus`.
- The name of choice for development branch is `dev`, so use such for new projects you create.
  Inherited projects sometimes use `devel` or `develop`, or whatever name previous developers found appropriate.
  We can deal with it.
- For small projects like packages and for projects that are not yet in production the difference between `master`
  and `dev` is not so important, so we might use the `master` in the role of `dev` for some time.



Commiting
---------

The importance of commiting **often** and **pushing** it to the central repo cannot be overstated.
**IT IS VITAL** THAT YOU COMMIT AND PUSH YOUR WORK.

Seriously, find a tool that allows you to commit and push in an instant and do the commit every ten minutes
or more often.

Tool recommendation: [SourceTree](http://sourcetreeapp.com/).




Code practices
==============

[Meteor Style Guide](https://github.com/meteor/meteor/wiki/Meteor-Style-Guide)



