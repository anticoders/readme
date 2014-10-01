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




&nbsp;

&nbsp;




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

Seriously, find a tool that allows you to commit and push in an instant and do the commit every **ten minutes**
or so.

Tool recommendation: [SourceTree](http://sourcetreeapp.com/).


Working in a branch
-------------------

When you do a large work in a branch make sure to pull the current version from `dev` at least once a day.
This will prevent enormous merge conflicts.




&nbsp;

&nbsp;




Code practices
==============


Meteor Style Guide
------------------

Core Team has a nice document describing the basic style and best practices
for coding in Javascript for Meteor. Read it here:
[Meteor Style Guide](https://github.com/meteor/meteor/wiki/Meteor-Style-Guide).
Make sure you understand the whitespace conventions and Javascript pitfalls.


Whitespace
----------

Standard indentation in Javascript is two spaces. Using tabs is unforgivable. Proper whitespacing
is an indicator of your experience. There is no excuse for `}else{`.


Variable definition
-------------------

Rule of thumb: one `var` keyword for one variable.

Wrong:

    var users = [],
        meaningOfLife = 41,
        iAteBanana = true;
        
Correct:

    var users = [];
    var meaningOfLife = 42;
    var iAteBanana = true;
    
  
Css classes
-----------

- Never use the same class for styling and behavior (JS events or data storage).
- Behavior classes should be prefixed by double underscore, i.e. `__submit`.
- When designing complex components, use single underscore for nested styling classes, i.e.
    
        <div class="box">
          <span class="_title"></span>
        </div>


Logging
-------

Whenever you use `console.log` or `console.error` for whatever reasons, **NEVER** use it without a label.
Even if it's a temporary debugging that you intend to remove in two minutes.
Similarly, `console.trace` and similar methods should be accompanied by a log with a label.

Wrong:

    console.log(something.length);
    
Correct:

    console.log("SLen", something.length);
    
If you've got several logs one after another, it is allowed to label only the first one.


Route data
----------

Route data function should always return a dictionary. Otherwise it is difficult to extend it later.

Wrong:

    data: function() {
      return Fruits.find({color: 'yellow'});
    },
    
Correct:
 
    data: function() {
      return {
        fruits: Fruits.find({color: 'yellow'});
      };
    },


Method return
-------------

The same rule applies for method results, for the same reason.

Wrong:

    Meteor.methods({
    
      'uploadFile': function () {
        ...
        return true;
      },
    
    });
    
Correct:

    Meteor.methods({
    
      'uploadFile': function () {
        ...
        return {
          success: true,
        };
      },
    
    });
    
    
Session
-------

Rule of thumb: do not use `Session`.

This is not an iron rule, `Session` can be sometimes used temporarily when we're not yet sure of a best pattern
to solve a certain problem and hacking with `Session` will prevent wasting time for a solution that we might
later purge. However, it should be always perceived as an ugly hack and purged as soon as possible.




&nbsp;

&nbsp;




Favorite packages
=================

Some problems have multiple solutions available in the environment.
In such cases it is a good idea to find the best solution and use it consistently across all our projects.
Here are a few recipes we already have. This list will grow in time.


Modal dialogs
-------------

    anti:modals
    
Forms
-----

    aldeed:autoform
 





