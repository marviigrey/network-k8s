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

kubectl create ns ns1
kubectl create ns ns2

Then we create the deployments in the YAML dirctory of this repository.
kubectl create  -f deployments.yaml
kubectl create -f deploy.yaml

===========================================================================================
After setting up our pods running the apps we move to setting the our policies.
As it stands,we have three pods running in three different namespaces:
mysql running in ns3 namespace,
np-test running in ns1,
nb-block running in ns2.

We need to expose each of our application by creating svc with the yaml object creation file.
After exposing them and confirming that the services are created we then move further to the next step:
We want the mysql pod to only allow traffic from nptest pod and not the np block. we also have an
external database with the ip [.......] to be able to reach out to our database pod which is mysql.
To carryout this task we then create a network policy called db-policy by using the yaml creation file called np.yaml.
After doing this we can test them by executing the ping or curl command with the endpoints of the services:
kubectl exec -it mysql -n ns3 -- curl <endpoint>.
The only pod that is allowed or reach this pod without error should be the NP-TEST pod.
