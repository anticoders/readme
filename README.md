Basics
======

Readme and best practices for Anticoders



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






