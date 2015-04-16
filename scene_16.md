## Environments

We celebrate the effecient system we finished in the last section. We are now able to spin up new nodes when needed. Now we need to consider what happens when we want to start developing new features for any of our cookbooks. How can we be sure that the version of the cookbook is the correct one working in production.

We introduce the concept of the environment. We explain the purpose of being able to separate the nodes into different segments. Most importantly we describe the ability to pin specific versions of cookbooks to our environments.

We demonstrate creating a 'delivered' environment. We create a list of cookbook requirements of all our current working versions of our cookbooks. We ask the attendees to demonstrate adding cookbook versions to the 'delivered' environment.

We demonstrate setting a node to the delivered environment. The attendees set their nodes to the delivered environment.

We explain that we are able to work on changes to existing cookbooks without affecting the systems in production.

We ask the attendees to add a new resource to the setup cookbook, update the version, and upload the cookbook. We ask the attendees to converge the nodes and see that the nodes were not affected by the new cookbook work.

We ask the attendees to use their environment to attempt a rollback to an earlier version of their apache cookbook.  While the recipe applies just fine, a close inspection of the systems reveals that they are misconfigured.  We use this to spark a discussion about rolling forward vs. rolling back.

To demonstrate that Chef is not a magic pony, we roll forward to the current version of the apache cookbook.  In an open lab, we ask students to remove vhost1 from the attributes to create apache vhosts.  Furthermore, they must write contra-resources to ensure that settings from vhost1 do not remain on their systems.
