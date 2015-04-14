## Resources

Welcome to your new organization. The one that judged you on every line of your resumé and scrutinized every answer you gave in the interview.

And now look at the state of our operations. We can't even get our system configured and delivered to you. Well at least you have a system. It seems there is always a fight to requisition hardware around here. So lets count ourselves lucky and see if we fend for ourselves.

Well the first place to start is to check to see if you have an editor installed on your workstation. But which is your editor:

* Emacs
* Nano
* Vim

> TODO: A small description and section should be added for each of these editors

Great. Now that you've picked your editor, you need to find out if it is already installed. We can use the `which` command and ask the Operating System (OS) if it knows if there is an executable for our text editor in our path.

```
$ which emacs
$ which nano
$ which vim
```

It seems the system does not even have a proper editor installed. So they have left you with an unfinished system with a little more  configuration left to do to make sure this workstation is ready.

Before you go and figure out your OS and installing some packages through the OS's specific package manager -- this seems like a perfect oppurtunity to experiment with how we could solve problems with Chef.

One of the best ways to learn a technology is to apply the technology in every situation that it can be applied. A number of chef tools are installed on the system so lets put them to use.

The first tool we will explore is `chef-apply`. It is a command-line application that allows us to work with resources and recipes files. But what are resources? What are recipe files?

Let's answer these questions one at a time.

First let's look at Chef's documentation about resources. Visit the docs page on resources and read the first three paragraphs.

> This sounds CRAZY to ask people in a physical classroom to read this content but it is important that they learn to read the documentation. And particularly this entry is very useful.

```
A resource is a statement of configuration policy that:

* Describes the desired state for an item
* Declares the steps needed to bring that item to the desired state
* Specifies a resource type—such as package, template, or service
* Lists additional details (also known as attributes), if necessary
* Tells the chef-client which action to take

Resources are grouped into recipes, which describe working configurations. For example, a package to install, the location of a template from which to build a file, and a service to be started.

Where a resource represents a piece of the system (and its desired state), a provider defines the steps that are needed to bring that piece of the system from its current state into the desired state.
```

Let's look at a few examples of resources.

So it seems that we can provide the reicpe text, the resources supplied as a string, to the `chef-apply` command. So if wanted to install the nano package we would probably run this command with the following text:

```
$ sudo chef-apply -e "package 'nano'"
```

So install your chosen editor using the `chef-apply` command. Now lets verify that the editor is installed by using the `which` command.

* What happens when I run the command again?

Think about what will happen. Look at the output from the previous run. Take a guess. Then run the command again to see the results of the command.

* What would happen if the package were to become installed?

So it should be clear now that the `chef-apply` command takes action only when it needs to. It uses test and repair to determine if the resource should take action.

So we have our editor installed but we missed a very important step. Chef is written on top of Ruby. Ruby is a programming language and it is required that that your first progam you write is 'Hello World'.

So let's walk through creating a recipe file that creates a file named 'hello.txt' with the contents 'Hello world!'.

Using your editor open up the file named 'hello.rb'. Add the contents as they are displayed here. We are using a file resource, specifying the file name and then providing a content parameter in between these two keywords `do` and `end`.

This says: The file named "hello.txt" is created with the content "Hello, world!".

Now let's use `chef-apply` to apply the recipe file, named 'hello.rb' that we created. Looking at the command it looks like that we can provide a recipe file directly to the `chef-apply` command.

To apply our recipe we would need to type `sudo chef-apply hello.rb`.

And to prove that a file was created we can use the `cat` command with the path of the file, 'hello.txt', that has the contents 'Hello, world!'.

So what happens when I run the command again?

Think about it again for a momemnt. Before you execute.

What would happen if you modified the contents of the file?

Modify the contents of 'hello.txt' with your text editor. Take a guess. Run the command again.

And, of course, what would happen if the file was removed?

At this point you hopefully understand the concept of test and repair.



Let's take a moment and talk about the structure of a resource definition. We'll break down the resource that we defined in our `hello.rb` file.

The first element of the resource definition is the type of the resource. In our course, the file is the type.

The second element is the name of the resource. This is also the first parameter being passed to the resource. In the case of the file resource, the name of the resource is the destination file that we want to have managed.

The `do` and `end` keywords here define the beginning of a ruby block. The ruby block and all the contents of it are the second parameter to our resource. The contents of this block usually contains attributes that help describe the state of the resource. In this instance, the source attribute here specifies the contents of the file.

The attributes are laid out with the name of the attributes followed by a space and then the value for the attribute.

The interesting part is that there is no action defined. And if you think back to the other examples that I showed you not all of the resources have defined actions.

So what action is the resource taking? How do you know? Can you find that information in the results of the `chef-apply` execution?

Can you find that information in the documentation for the file resource?

While looking through the file resource documentation find the default action and the default values for the mode, owner, and group.

Then I want you to return to the file resource in 'hello.rb' and add attributes for mode, owner and root if they need to be specified.


> Allow the attendees time to solve this exercise


So returning to the hello recipe file and the file resource to enforce the new policy we need to define three new attributes and values for mode, owner, and group. This is because the default values are not exaclty the policies that we want set on the system.


> Allow time to answer any questions

So now that we've practiced:

* installing an application with the package resource
* creating a recipe file
* creating a file with the file resource

Create a recipe named 'setup.rb' that

* Installs the edtior
* Installs the tree package
* And then creates an MOTD file


What is the resource definition for this description: `The package named $EDITOR is installed.`

What is the resource definition for this description: `The package named tree is installed.`

What is the resource definition for this description: `The file named "/etc/motd" is created with the content "Property of ...".`


> Allow the attendees time to solve this exercise


Here is the final version of the `setup.rb` file that installs all the editors, our tree package, and creates our MOTD file.

Let's finish up this section on resources with a discussion.

I want you to write down or type out a few words for each of these questions. Remember that the answer "I don't know! That's why I'm here!" is a great answer.


* What is a resource?

* How were the previous examples (i.e. package, service, file) describing the desired state of an element of our infrastructure?

* What are some other possible examples of resources?

* What does it mean for a resource to be a statement of configuration policy?

Now turn to the individuals around you in the workshop and go back-and-forth and share you're answers with each other.


What questions can we answer for you?








