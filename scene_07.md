It took me a while to really get how to use Chef attributes.

A Chef attribute can be seen as a variable that:

1) gets initialized to a default value in cookbooks/mycookbook/attributes/default.rb

Examples:

default[:mycookbook][:swapfilesize] = '10485760'
default[:mycookbook][:tornado_version] = '1.1'
default[:mycookbook][:haproxy_version] = '1.4.8'
default[:mycookbook][:nginx_version] = '0.8.20'

2) gets used in cookbook recipes such as cookbooks.mycookbook/recipes/default.rb or any other myrecipefile.rb in the recipes directory; the syntax for using the attribute's value is of the form #{node[:mycookbook][:attribute_name]}

3) can be overridden at either the role or the node level (and some other more obscure levels that I haven't used in practice)

I prefer to override attributes at the role level, because I want those overridden values to apply to all nodes pertaining to that role.

---

Attribute implements a nested key-value (Hash) and flat collection (Array) data structure supporting multiple levels of precedence, such that a given key may have multiple values internally, but will only return the highest precedence value when reading
