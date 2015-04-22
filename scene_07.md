Have you ever had to manage a large number of servers that were almost identical, except that each one had to have some host-specific information in some config file somewhere?
Maybe they needed to have the hostname embedded in the config file, or an IP address, or the name of an NFS filesystem on a mount point.
Maybe you needed to allocate 2/3 of available system memory into hugepages for a database. Maybe you needed to set your thread max to ([number of CPUs] – 1). And each one had to be managed by hand!

___

Some Useful System Data includes
* IP Address
* hostname
* memory
* CPU- Mhz

___
To Discover the ipaddress of the node, we can issue the command
hostname -l

___
We can include this information in our recipe
file "/etc/motd" do
  content "Property of ...
  IPADDRESS: 104.236.192.102"

  mode "0644"
  owner "root"
  group "root"
end

___
Next we need to have the hostname embedded in the config file.
hostname = banana-stand

Let's go ahead and include this also in our recipe
___

We need to allocate 2/3 of avialble system memory, lets discover the memory
MemTotal: 502272 kB

Adding the memory in the recipe

file "/etc/motd" do
  content "Property of ...
  IPADDRESS: 104.236.192.102
  HOSTNAME : banana-stand
  MEMORY   : 502272 kB"


  mode "0644"
  owner "root"
  group "root"
end
___

Next we need to set our thread max to ([number of CPU's]) - Lets discover the cpu -MHz

file "/etc/motd" do
  content "Property of ...
  IPADDRESS: 104.236.192.102
  HOSTNAME : banana-stand
  MEMORY   : 502272 kB
  CPU      : 2399.998MHz"

  mode "0644"
  owner "root"
  group "root"
end
___
