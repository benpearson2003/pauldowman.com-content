It's not possible to change the name of a [Chef](http://www.opscode.com/chef/)
node that already exists. But you can effectively do this by deleting the node
on the Chef server and re-creating it, which is not actually as scary as it
sounds, here's how.

_[Chef server]_ means do this step on the Chef server (or [Hosted
Chef](http://www.opscode.com/hosted-chef/)), and _[node]_ means do it on _your_
server, the node you're renaming.

1. [Chef server] delete the node
1. [Chef server] delete the client for the node
1. [Node] delete /etc/chef/client.pem
1. [Node] edit /etc/chef/client.rb and add `node_name "new-name"`
1. [Node] run chef-client
1. [Chef server] edit the newly created node:
    1. set the run list
    1. set the environment
1. [Node] run chef-client


Remember that a Chef node name [must match the pattern `/^[\-[:alnum:]_:.]+$/`](http://wiki.opscode.com/display/chef/Nodes).

If you've gone to the trouble of setting a descriptive node name you might find
it convenient to use that as the hostname as well. [Chef on
Rails](https://github.com/pauldowman/chefonrails#readme), my Chef repo for
deploying a standard Rails app, has a
[recipe](https://github.com/pauldowman/chefonrails/blob/master/cookbooks/chefonrails/recipes/hostname.rb)
to do just that.

