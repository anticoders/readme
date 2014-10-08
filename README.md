Intro
=====


> Always code as if the person who ends up maintaining your code is a violent psychopath who knows where you live[.](http://c2.com/cgi/wiki?CodeForTheMaintainer)

Maintaining good code quality and sharing a common view on best practices is very important for our clients.
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




Index
======


- [Git practices](#git-practices)
- [Code style](#code-style)
- [Code practices](#code-practices)
- [App structure](#app-structure)
- [Favorite packages](#favorite-packages)





&nbsp;

&nbsp;




Git practices
=============


Do commit early, commit often
---------
"If you've ever sat down for a fast and furious coding session only to realize hours later that you removed something important, you know the frustration of not being able to get it back. It can mean hours lost. Getting in the habit of regular commits has a number of benefits. First, you can go back to any previously committed version if your coding goes off-track. You can reference earlier parts of your work even if you don't need to revert to them. Best of all, it an actually have a positive impact on your code itself."

Better Code through Committing
Just as Test-Driven Development influences us to write a larger number of shorter/simpler methods, frequent committing pushes us to think of atomic changes. Continue reading: [Don't Be Afraid of Commitment](http://www.databasically.com/2011/03/14/git-commit-early-commit-often/). 

Tool recommendations
-------
[SourceTree](http://sourcetreeapp.com/).
[smartGit](http://www.syntevo.com/smartgit/).

Pull to stay current, and pull-before-you-push
-------

When you pull, git will fetch commits on origin and will try to fast-forward your local commits on top of them, doing the merge. After that you can push in this way you will not generate conflicts with other updates.

When you do a large work in a branch make sure to pull the current version from `dev` at least once a day.
This will prevent enormous merge conflicts.

Start your day by pulling the recent version.


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




&nbsp;

&nbsp;




Code style
==========


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


Brackets
--------

Luckily, in JS there is no place for debate on correct bracket placement:
    
Always use Egyptian brackets:

    // GOOD
    while(answer < 42) {
      ...
    }

    // BAD - this is an error in JavaScript
    while(answer < 42)
    {
      ...
    }
    

Colon placement in JavaScript
---------------

    // GOOD
    bla,
    bla,
    bla,

    // BAD
    bla
    , bla
    , bla

    // GOOD in `.json`); BAD in JS
    bla,
    bla,
    bla

Variable definition
-------------------

Rule of thumb: one `var` keyword for one variable.

    // GOOD
    var x = [];
    var y = 42;
    var z = true;

    // BAD
    var x = [],
        y = 4s,
        z = true;

In the BAD example, lines 2 and 3 depend on the first line. See how a co-worker quickly added y1 and mistakenly created a global variable "z":

    // BAD
    var x = [],
        y = 41,
        y1 = 2;
        z = true;

  
Variable naming
---------------

Use camelCase for all names.

In the case of global objects (collections, route controllers, namespaces) start with upper case letter:
    AdminDashboardController = BaseController.extend({...

Everything else start with lower case letter:
    var firstName = fullName[0];
    <template name="adminReceiveItem">

Collection names should be in plural:
    Posts = new Meteor.Collection('posts');


Css classes
-----------

- Never use the same class for styling and behavior (JS events or data storage).
- Behavior classes should be prefixed by double underscore, i.e. `__submit`.
- When designing complex components, use single underscore for nested styling classes, i.e.
    
        <div class="box">
          <span class="_title"></span>
        </div>




&nbsp;

&nbsp;




Code practices
==============

Logging
-------

Whenever you use `console.log` or `console.error` for whatever reasons, **NEVER** use it without a label.
Even if it's a temporary debugging that you intend to remove in two minutes.
Similarly, `console.trace` and similar methods should be accompanied by a log with a label.

    // GOOD
    console.log("SLen", something.length);

    // BAD
    console.log(something.length);
    
    
If you've got several logs one after another, it is allowed to label only the first one.


Empty queries
-------------

Always fully qualify your queries, even if the local collection contains only the data you want.

    // GOOD
    MyBlogArticlesListController = RouteController.extend({
      
      onBeforeAction: function() {
        this.subscribe('myBlogArticles');
      },
      
      data: function() {
        return {
          articles: BlogArticles.find({
            userId: Meteor.userId(),
          });
        };
      },
      
    });

    // BAD
    MyBlogArticlesListController = RouteController.extend({
        
        onBeforeAction: function() {
          this.subscribe('myBlogArticles');
        },
        
        data: function() {
          return {
            articles: BlogArticles.find({});
          };
        },
        
      });

The collection may include documents from other publications, or your original publication may have been modified by another developer. Fully qualify your queries (with appropriate filters/constrains) to ensure you don't accidentally expose data you didn't expect to be in the collection.


Route data
----------

Route data function should always return a dictionary. Otherwise it is difficult to extend it later.
      
    // GOOD
    data: function() {
      return {
        fruits: Fruits.find({color: 'yellow'});
      };
    },

    // BAD
    data: function() {
      return Fruits.find({color: 'yellow'});
    },

Method return
-------------

The same rule applies for method results, for the same reason.
    
    // GOOD
    Meteor.methods({
    
      'uploadFile': function () {
        ...
        return {
          success: true,
        };
      },
    
    });

    // BAD
    Meteor.methods({
    
      'uploadFile': function () {
        ...
        return true;
      },
    
    });    
    
Session
-------

Rule of thumb: do not use `Session`.

This is not an iron rule, `Session` can be sometimes used temporarily when we're not yet sure of a best pattern
to solve a certain problem and hacking with `Session` will prevent wasting time for a solution that we might
later purge. However, it should be always perceived as an ugly hack and purged as soon as possible.


Triple Repetition Rule
----------------------

The Triple Repetition Rule states that the code should be refactored to avoid repetition when a triple repetition occurs and **no sooner**. An important corollary for purists: it is perfectly OK to have two files 120-lines each that differ with nothing but one identifier.


Regexes
-------

Real-life example


    id = @text.split("http://www.youtube.com/watch?v=")[1]
    if id is undefined
      id = @text.split("https://www.youtube.com/watch?v=")[1]
      if id is undefined
        id = @text.split("http://youtube.com/watch?v=")[1]
        if id is undefined
          id = @text.split("https://youtube.com/watch?v=")[1]
    id

The worst thing about this code is not that it's ugly, but one needs more than
a few seconds to understand what is going on.

Use regexes where applicable. If you don't know regexes yet:

- Ask a senior developer to write the regex.
- Learn them!

Recommended source: [Regular Expressions Cookbook](http://shop.oreilly.com/product/9780596520694.do).


Global variables
----------------

Real-life example:

    // Global function to return the number of panels in a System ...
    PanelQty = function (systemId) {
      ...
      return PanelGroups.find({ systemId: systemId }).map(...);
    };

The whole app from which this was taken had around 200 methods like that and nothing else.
I hope that no explanation is needed here.

In any case, hard rules:

- Collections and RouteControllers are global by design, so they're global.
- Besides that, **only** dictionaries allowed!
- As few as possible.
- Naming: CapitalCamelCase.



&nbsp;

&nbsp;




App structure
=============


Basic folders
-------------

- `both`
  - `collections`
  - `routes.js`
- `client`
  - `app`
    - `helpers`
  - `components 
  - `views`
- `public`
  - `files`
- `server`
  - `collections`
  - `methods`


Files in `/both/collections` contain collection definition, schema, class and instance methods and enums.

Files in `/server/collections` contain allow / deny rules and publications.

Route controllers are placed in `/views` folder, in the same place where their respective view `.html` and `.js` files. Controller file names begin with an underscore, i.e. `_blogArticleListController.js`.

All static files should be placed in `/public/files`, so that their path begin with `/files`. Large assets in grown-up applications should be placed on S3.

We use `camelCase` converter for route templates and `upperCamelCase` for route controllers.

    Router.configure({
      templateNameConverter:          'camelCase',
      routeControllerNameConverter:   'upperCamelCase',
    });

In most apps we have global `Helpers` object to which we add UI helpers.


Clutter limits
--------------

There's an old rule stating that file size shouldn't exceed 100 lines. Sice whitespaces, closing brackets and comments can increase file length without adding content, we should increase the limit in JS to 200 lines, but make it a strong limit! If your file exceeds 200 lines, split it.

We should limit the number of files in a folder. If your folder has more than ~12 files, and not all of them are of the same kind (like view folders), consider breaking it into subfolders.

While there are no hard rules for line length, we should try to keep them under 100 characters. Most importantly, write your code in a way that increases readability. Real life example:

    var textTestimonials = TextTestimonial.find({userId: this.user._id}).fetch();

More readable way to write it:

    var textTestimonials = TextTestimonial.find({
      userId: this.user._id
    }).fetch();



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
 


