# network-k8s
In this little project,we will work on how to create a network policy in kubernetes.By default,every pod
in our cluster can reach each other through their ips,we might not want tha to happen so we create network
policies. So what are network policies? They help us to secure a specified pod and restrict access from
other pods within or outside our cluster. Pods  within our cluster can reach each other irrespective of
the namespace. So to prevent this we make use of network policy.

In this project we follow a step by step illustration on how to impose a network policy on our environment.
=================================================================================================
note: You will need a VM running a k8s node.

1. we will randomly create three different pods running on different namespaces,but first we create the
two namespaces ns1 and ns2,the third ns is the default ns which is already created.