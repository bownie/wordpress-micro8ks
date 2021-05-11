## Wordpress PV with microk8s

Using this as a basis for a starter microk8s wordpress setup including some debugging knowledge. Using this as a basis:

https://kubernetes.io/docs/tutorials/stateful-application/mysql-wordpress-persistent-volume/

We want to achieve this functionality:

https://github.com/verize/kubernetes-wordpress-ingress

## Installation notes as we go along

We can also update to the latest wordpress:

https://hub.docker.com/\_/wordpress

Using version 5.7.1 and mysql 5.7

# Prerequisites

## Enable storage for our PVs

  $ microk8s enable storage

## Enable DNS

  $ microk8s enable dns

Is this required for service discovery?   Need to retest.

## Get the kubernetes dashboard:

  $ microk8s enable dashboard

https://microk8s.io/docs/addon-dashboard

Get the token:

  $ token=$(microk8s kubectl -n kube-system get secret | grep default-token | cut -d " " -f1)
  $ microk8s kubectl -n kube-system describe secret $token

## Enable ingress and load balancer

https://microk8s.io/docs/addon-metallb

  $ microk8s enable ingress metallb

Set up the port forwarding to access it:

  $ microk8s kubectl port-forward -n kube-system service/kubernetes-dashboard 10443:443

Then you can go here to access the dashboard and check the status of your microk8s setup:

  https://127.0.0.1:10443

Don't forget you need a token to login.  You can get that from here:


# Deploying the solution

   $ microk8s kubectl apply -k .

## Checking everything is looking good

  $ microsk8s kubectl get pods

Get the port forwarding working out of the wordpress service to the localhost:

  $ microk8s kubectl port-forward service/wordpress 1080:80

Then you can go to here to test:

http://127.0.0.1:1080

# Next steps

Looking at kustomize in more detail particularly when it comes to kustomize:

https://kubectl.docs.kubernetes.io/guides/introduction/kustomize



# Debugging

Get the pods:
  $ microk8s get pods

If the pod won't start (CreateContainerConfigError) then try to describe the pod:

  $ microk8s kubectl describe pod wordpress

If the pod will start and you want to see the logs:

  $ microk8s kubectl log wordpress-pod-details

Run something on the pod
  i.e. 

  $ microk8s kubectl exec -it wordpress-mysql-6c9dfc6b66-q2znm

## Getting to the mysql database to check it exists

Port forward mysql from the kubernetes services to your localhost:

  $ microk8s kubectl port-forward service/wordpress-mysql 3306:3306

connect with mysql:

  $ mysql -u root -h 127.0.0.1 -p

## Using the jumpod to check service status

https://platform9.com/blog/kubernetes-service-discovery-principles-in-practice/

  $ microk8s kubectl exec -it jumpod ping 10.244.0.149

Get FQDN using nslookup (how does this interact with Kube DNS?):

  $ microk8s kubectl exec -it jumpod nslookup 10.244.0.149

## Using busybox

  $ microsk8s kubectl run -it --rm --restart=Never busybox --image=gcr.io/google-containers/busybox sh


## Debug directly on the pod

  $ microk8s kubectl exec -it wordpress-544bc8f8d4-lmrfm bash

# Ingress, LoadBalancer and Port Forwarding

Note that LoadBalancer doesn't work on mac microk8s so use port forwarding.

# SSL Certs

Enable helm3 and install as follows:

https://www.thinktecture.com/en/kubernetes/ssl-certificates-with-cert-manager-in-kubernetes/

Useful links:

https://kubernetes.io/docs/reference/kubectl/cheatsheet/

