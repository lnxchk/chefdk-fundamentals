## Chef In-Depth

Having seen value from using Chef on Day 1, we follow up the lesson on managing their infrastructure with a Chef server by getting into basic Chef internals.  Once students begin experimenting with Chef on their own, they may hit common beginner pitfalls into despair.  This module prepares students with the knowledge they need to navigate learning how to apply Chef on their own successfully.

Common beginner pitfalls into dispair include

* The temptation to make everything an execute resource
* Relying exclusively on node attributes in templates
* Checking for conditions during compile time that really need to be checked during converge
* Frustration when Chef produces errors they can't reason their way around
* Thinking Chef is a magic pony because they're not familiar enough with basic internals to start code spelunking or docs diving
* A lack of proper versioning practices and stepping on each other's toes by uploading untracked content

To do this, we cover a few concepts (this may actually be two modules?).

Students have run chef-client a number of times.  We dig into the anatomy of a chef-client run and the basic security model of chef-client.

To see how these concepts impact common things they may have to do, we refactor the apache cookbook.

We describe what we want: multiple websites.  For the non-apache familiar, we describe the steps that would need to occur in order for us to be able to do this.  We explain that automation does not replace the need for domain expertise.  In a real world scenario, students must understand the process they want to occur before they attempt to automate it.  For classroom purposes, this is the process we want to automate.

We start by creating a new version of the apache cookbook.  We talk about the basics of semantic versioning.

We open our apache cookbook.  We refactor this the long way.  Use an execute resource in here to disable our default apache vhost.  We talk about controlling idempotency by using guards and compile vs. converge considerations.  We describe why students should resist the temptation to effectively make Chef a giant script runner (bash++).

We set up vhost1.  We set up vhost2.  Run it.  Does it work?  It should.  But that's long code.  What if we wanted another vhost?

We talk about data-driven cookbooks (this is the key concept they should be picking up).  Now that we have a pattern for what we're doing, we can abstract away a data model.  What bits are different between vhost1 and vhost2?  We create a data model that manages only those differences.

We create a loop to iterate through the data model.  For each bit of data we find, do the repetitive tasks.  This is an AHA moment.  In this section, we introduce the use of template variables.

Now that we know this recipe works, we purposefully introduce a config error (the standard bug).  Students run chef-client.  Predictably, this breaks.  In an open lab, students must now fix the error.

^-- Not sure how I feel about this.  Is it unfair for an open lab to introduce a new skill? 