## Attributes

Have you ever had to manage a large number of servers that were almost identical, except that each one had to have some host-specific information in some config file somewhere?

Maybe they needed to have the hostname embedded in the config file, or an IP address, or the name of an NFS filesystem on a mount point.

Maybe you needed to allocate 2/3 of available system memory into hugepages for a database. Maybe you needed to set your thread max to ([number of CPUs] – 1). And each one had to be managed by hand!

-

Here we've been given the simple request of providing some additional details about our node in both our Message of the Day and our default index page that we deploy with our web server.

We'll start first with our message of the day.

-

Thinking about some of the scenarios that I mentioned at the start of the session makes me think that it would be useful to capture:

The ip address, hostname, memory, and CPU megahertz of our current system.

Let's walk through capturing that information using various system commands starting with the ip address.

-

To discover the ipaddress of the node, we can issue the command

`hostname -l`

-

Or we can dig it out of the results of running `ifconfig`.

-

We can include this information in our slash-e-t-c-slash-m-o-t-d by updating the contents of the file's content attribute.

Within the existing string value we've inserted a number of new lines for formatting and placed our ipaddress along with its value.

-

Next is the machine's hostname. This is easily retrievable with the `hostname` command.

-

We can also include that information in the file's content attribute on a new line below our ipaddress.

-

One way to gather the memory of our system is to `cat` the contents of the slash-proc-slash-meminfo. There we can select the total memory available on the system.

-

And again we can add it in the file's content attribute below our hostname.

-

Discovering information about the system's CPU is very similar. We can `cat` the contents of slash-proc-slash-cpuinfo and select the CPU megahertz from the results.

-

Adding it, like the others, to the file's content attribute.

-

Let's apply our "setup" cookbook's "default" recipe

-

And then verify that our slash-e-t-c-slash-m-o-t-d had been updated with our values. Great!

-

Well, is it great?

Now that we've defined these values, lets reflect:

What are the limitations of the way we captured this data?

-

How accurate with our m-o-t-d be when we deploy it on other systems?

-

Are these values we would want to capture in our tests?

-

If you've worked with systems for awhile general feeling is that hard-coding the values in our file's content attribute probably is not sustainable because the results are tied specifically to this sytem at this moment in time.

Capturing the data in real-time on each system is definitely possible.

We would need simply execute each of these commands and parse the results and then insert the dynamic values within file resource's content attribute.

Before we start down this path, I would like to introduce you to Ohai.

-

Ohai is a tool that detect and captures attributes about our system. Attributes like the ones we spent our time capturing.

-

Ohai is also a command-line application that is part of the ChefDK.

-

Ohai, the command-line application, will output all the system details it captures in JavaScript Object Notation (JSON).

-

As I mentioned before these values are available in our recipes because `chef-client` and `chef-apply` automatically execute Ohai. This information is stored within a variable we call 'the node object'.

-

The node object is a representation of our system. It stores all these attributes and a number of other information about the system. It is available within all the recipes that we write to assist us with solving the similar problems we outlined at the start.

Lets look at using the node object to retrieve the ipaddress, hostname, total memory, and cpu megahertz.

-

Here we are using ruby's `puts` to display the ipaddress attribute from of our node.

-

This is how we retrieve and display the hostname.

-

Here is the total amount of memory for the system.

-

And finally the megahertz of the first cpu.

-

In all of the previous examples we demonstrated retrieving the values and displaying them within a string, the text, using a ruby language convention called string interpolation.

-

String interpolation is only possible with strings that start and end with double-quotes.

-

To escape a string to display a ruby variable you use the following sequence: number sign, left curly brace, the ruby variables or ruby code, and then a right curly brace.

-

So lets replace the static ipaddress with the node's ipaddress. We will use string interpolation within the file resource's content attribute to allow us to access the node object's attribute for ipaddress.

-

We will continue to do that for the node object's attribute for hostname.

-

For the total memory.

-

And for the megahertz of the first CPU.

-

Lets verify that the changes to the setup cookbook's setup recipe were made correctly by running our tests.

-

Good. Now that we've made these significant changes and verified that they work its time we bumped the version of the cookbook and commit the changes.

-

The first version of the cookbook displayed a simple property message in the slash-e-t-c-slash-m-o-t-d. The changes that we finished are new features of the cookbook.

-

Cookbooks use semantic version. The version number helps represent the state or feature set of the cookbook. Semanitc versioning allows us three fields to describe our changes: major; minor; and patch.

Major versions are often large rewrites or large changes that have the potential to not be backwards compatible with previous versions. This might mean adding support for a new platform or a fundamental change to what the cookbook accomplishes.

Minor versions represent smaller changes that are still compatible with previous versions. This could be new features that extend the existing functionality without breaking any of the existing features.

And finally Patch versions describe changes like bug fixes or minor adjustments to the existing documentation.

-

So what kind of changes did you make to the cookbook? How could we best represent that in an updated version?

-

Changing the contents of an existing resource - by adding the attributes of the node doesn't seem like a bug fix and it doesn't seem like a major rewrite. It is feels like a new set of features while remaining backwards compatible.

So lets update the version's minor number to 0.2.0.

-

The last thing to do is commit our changes to source control. Change into the directory, add all the changed files, and then commit them.

-

Wonderful. Now its time to add similar functionaly to the apache cookbook.

Update content attribute of the file resource, named slash-var-slash-dub-dub-dub-slash-h-t-m-l-slash-index-dot-h-t-m-l, to include the node's ipaddress and its hostname.

Run the tests to verify that the changes did not break anything.

Update the version of the cookbook and then commit the changes.

> Allow the attendees time to complete this exercise

-

Similar to the work that we did in the setup cookbook, we add our two node attributes using string interpolation.

-

This is a similar feature so the version should be updated to 0.2.0.

-

And finally the changes should similarly be commit.

-

With that we have added all of the requested features.

What questions can we help you answer?

In general or about specifically about ohai, the node object, node attributes, string interpolation, or semantic versioning.