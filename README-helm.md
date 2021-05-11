# Deploying via a Helm chart in Microk8s

Enable helm3:

  $ microk8s enable helm3

Configure repo and instal

  $ microk8s helm3 repo add bitnami https://charts.bitnami.com/bitnami
  $ microk8s helm3 install my-release bitnami/wordpress

As from:

https://github.com/bitnami/charts/

You can now connect as per the README but specifying the new service name.

  Hint: use microk8s kubectl get services

  $ microk8s kubectl port-forward service/my-release-wordpress 1080:80

## Modifying the Helm chart


