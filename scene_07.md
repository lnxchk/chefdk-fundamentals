A Chef attribute can be seen as a variable to understand:
* The current state of the node
* What the state of the node was at the end of the previous chef-client run
* What the state of the node should be at the end of the current chef-client run


___

Attribute implements a nested key-value (Hash) and flat collection (Array) data structure supporting multiple levels of precedence, such that a given key may have multiple values internally, but will only return the highest precedence value when reading
___



###Attribute Sources

Let's look at cookbooks/apache/attributes/default.rb which is where we'll be defining the variable options for installing and running Apache.

A Chef attribute can be seen as a variable that:

1) gets initialized to a default value in cookbooks/apache/attributes/default.rb

Examples:

default[:apache][:dir] = "/etc/apache2"
default[:apache][:indexfile] = "index1.html"

___

2) gets used in cookbook recipes such as cookbooks/apache/recipes/default.rb or any other myrecipefile.rb in the recipes directory; the syntax for using the attribute's value is of the form #{node[:apache][:attribute_name]}
___

3) can be overridden at either the role or the node level (and some other more obscure levels that I haven't used in practice)


___

### Attribute Precedence

I prefer to override attributes at the role level, because I want those overridden values to apply to all nodes pertaining to that role.


___
