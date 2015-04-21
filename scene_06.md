## Testing Cookbooks

Automation is beautiful when it works. A work of art. When it doesn't work -- well it's a work of something.

As we start to define our infrastructure as code and tracking it in source code and then releasing we also need to start thinking about testing it. That seems obvious, of course, test the recipes within the cookbooks that we write.

We could define a process that every time we make a change to our tools and scripts it needs to be tested. And we probably would be fairly successful at first, like a New Year's resolution, but start to let things slide over time.

And that's because verifying changes is work. It's work to setup the test environment or environments, load your scripts, and then execute them. If its manual work it has the chance of being forgotten or incorrectly done.

-

Well if Chef is to replace our existing tools it is going to need to provide a way to automate some of the pain of testing out policies that we have defined.

-

ChefDK comes with another tool named Test Kitchen. Test Kitchen is a test harness tool that allows us to execute the cookbook recipes against virtual  or cloud instances.

-

Kitchen is a command-line application that allows us to manage the testing lifecycle. This application allows us to create, converge, verify, and destroy instances.

Similar to other tools within the ChefDK we can ask for help to see the available commands.

The `init` command, by its name, seems like a good place to get started.

-

`kitchen help init` tells us that it will add Test Kitchen support to an existing project. It creates a dot-kitchen-dot-yaml file within the project's root directory.

There are a number of flags and other options but let's see if the cookbooks we created need to be setup.

-

Using `tree` to look at the setup cookbook, showing all hidden files and ignoring all git files, it looks like our cookbook already has a dot-kitchen-dot-yaml.

It was created alongside the other files when we ran the `chef generate cookbook` command when we originally created this cookbook.

Let's take a look at the contents of this file.

-

The kitchen-yaml file defines a number of configuration entries which the kitchen command uses during execution.

-

So we don't need to run `kitchen init` because we've already have a default kitchen file. We may need to change it to accomplish our objectives so lets learn about a few of the fields within the configuration file.

-

! THE KITCHEN DRIVER
