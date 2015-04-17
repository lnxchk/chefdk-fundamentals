## Cookbooks

Well the recipe that you put together to do a little setup seemed useful enough to see if the same could be done with a webserver. That shouldn't be a problem right? It's a package, a file, and a service.

Version control and a README would definitely make it easier to share the recipes that we create. Without version control we'd have no way to recover our work, allow us to build this software together. Without a README no one would know what the recipe even was suppose to do or what it did.

-

Let's tackle this head on. If we're going to use Chef as a configuration management tool and we're going to treat our infrastructure as code we need to make sure that we start using version control.

-

What's the best way to learn Chef? Use Chef. I want you to literally run Chef. Yes the company that already has a hard enough time to get high ranking in the Google space releases a tool named after the company and the product. Try finding good support for that.

-

Fortunately you don't have to because the tool is a fairly straight-forward command-line executable that does quite a few things. The most important of which for us is its ability to to generate cookbooks and components.

But what is a cookbook?

-

Let's look up cookbooks in Chef's documentation. Visit the docs page on cookbooks an read the first three paragraphs.

> This sounds CRAZY to ask people in a physical classroom to read this content but it is important that they learn to read the documentation.

A cookbook is a structure that contains recipes. Both here in the traditional sense. A cookbook can contain other things as well as the entry goes on to say.

-

Well let's examine the chef generate command. We have a number of options. Sounds like if we want to generate a cookbook we're going to need to use the cookbook in the command.

-

Alright. So to generate a cookbook all we have to is provide with a name. Uh oh! There are two hard things in Computer Science and half of the hard things is namely stuff.

-

Don't worry I have you covered. Call the cookbook setup. It's the setup cookbook. Create the setup coobook.

-

Aren't you curious whats inside it? Let's take a peek with the help of the `tree` command. If we provide it a path we'll s all the visible files in the specified directory.

So the chef generated an outline of a cookbook with a number of default files and directories. The first one we'll focus on is the README.

> People will want to talk about the Berksfile. Remember our goal is to add a README and find our way to version control.

-

All cookbooks that chef will generate for you will include a default README file. The contents of the file adhere the markdown standard. It's a way to organize text in heirachical structures. It's all the rage for documentation.

-

The cookbook also has a metadata file.

-

This is a ruby file that contains a domain specific language (DSL) for describing the details about the cookbook. To include version number, contact for the code and more.

-

If you cat the contents of our new cookbook's metadata you'll see a number of details that help describe the cookbook. The name of the cookbook, its maintainer, a way to reach them, how the cookbook is licensed, descriptions, and the important version number.

-

The cookbook also has a folder named recipes. This is where we store the recipes in our cookbook. You'll see the generator created a default recipe in our cookbook. What does it do?

-

Looking at the contents of the default recipe you'll find its empty except for some comments. A cookbook doesn't have to have a default recipe but most every cookbook has one. It's called default because when you think of a cookbook it is probably the recipe that defines the most common configuration policy.

-

Lets copy or move our recipe to the setup cookbook and place it alongside our default recipe.

-

Well now that we have our cookbook with its README and version number its time to add it to source control. We are going to use git in this workshop but you are welcome to use tools that are most effective for your team.

-

Is git installed? Do we know if it will be installed with every new instance that is setup?

It sounds like we need the tool now to store our cookbook but we also want to define a policy that git is installed on all of our workstations.

Let's update our setup cookbook's setup recipe, not our setup recipe, to define a new statement of configuration policy:

The package named 'git' is installed

> Allow time for individuals to complete this exercise. This reinforces the concept that chef-apply works on a filepath.

-

Same as before we add our packaged named 'git' to the setup recipe within our setup cookbook.

-

Then we use chef-apply to apply our recipe. The recipe path has changed. Remember it is inside the setup cookbook's recipe directory.

-

That's not really delightful. It is great to store recipes within a cookbook but it would be get tiresome working with recipes in this way. Constantly having to specify the path.

And that's because `chef-apply` is a great tool to explore concepts within Chef but it is not the tool that you will be using on your production systems.

There is another tool named 'chef-client' which we will explore later.

-

Now with git installed, it's time for us to actually add the cookbook to source control.

-

Let's change directories into the setup cookbook.

-

We want to git to start tracking the entire contents of this folder and any subfolders. To do that with git you execute the command `git init` in the parent directory you want to start tracking in source control.

-

Now we need to tell git what files it should start tracking in source control. In our case, we want to add all the files to the repository and we can do that by providing a period following the add command.

This will place all the files into a staging area.

I like to think of the staging area as placing bunch of items into a box. A care package you were going to send a love one. And staging them means - put them in the box, don't close it up because I may add a few things, don't close it up because I may replace or remove a few things. But put the items in the box because eventually we're going to close that box up and ship it out to you.

-

Let's look inside the box. What are we going to sending to someone if we were to close this box up. Running `git status` allows us to see in the box. Git will report back to us the changes that will be commited.

> Git helpfully tries to show you the command you can use to remove an item from that box. This is useful if you want to include all items excepts for one or simply manage everything before you commit.

-

If everything looks like it should be in the box. Then we're going to seal it up. That is done in git with `git commit`. We can optionally provide a message on the command-line and that is done with the DASH-m flag and then a string of text that describes that change.

> Without that flag git attempts to use the system that you've defined as your default EDITOR.

> Git does not know who is making the commit. An additional fun exercise is to have people use Chef to write a file resource that generates the `~/.gitconfg` with their user name and email address.

-

So again, within the cookbook we are going to initialize the repository. Then we are staging every file in the repository. And then finally committing all those staged changes.

-

Now that we're done adding source control to the setup cookbook lets return our home directory.

-

We got a little sidetracked with cookbooks, versioning, and source control. Remember, we were asked if we could write a recipe to setup a web server.

-

Thinking about what we accomplished so far, that totally seems possible. We would need to write a recipe that defines the policy for apache. Create a cookbook to store that recipe and then add the cookbook to version control.

So show me it can be done!

> Allow individuals a fair amount of time with this exercise.

-

Alright first I would leverage chef and chef generate helpers to create a cookbook for me. From my home directory running the command `chef generate cookbook apache`. This will place the apache cookbook alongside our setup cookbook.

-

The apache recipe defines the policy:

* The package named "httpd" is installed.

* The file named "/var/www/html/index.html" is created with the content "<h1>Hello, world!</h1>"

* The service named "httpd" is started and enabled.

-

Applying the commmand with `chef-apply` I need to specify the partial path to the recipe file.

-

Finally its time to add the cookbook to version control.

* Move into that directory
* Initialize the cookbook as a git repository
* Add all the files within the cookbook
* Commit all the files

-

What questions can we answer for you?

General questions or more specifically about cookbooks, versioning and version control?

