# Configuring your own Docker image for Wordpress

If you want to create a specially configured Wordpress image for your k8s deployment the 
easiest way is to generate a Dockerfile and use "docker build" to create a new image tailored
to your specific needs.  This image can then be pushed to a registry such as Docker Hub and 
be available for you to pull down again into your kubernetes cluster when you configure that.

Therefore you will need to create a Dockerfile such as this:

  $ cd wordpress-xyglo
  $ docker build -t wordpress-xyglo .

For example push to xygloid on Docker Hub:

  $ docker tag e85a2ca20825 xygloid/wordpress
  $ docker push xygloid/wordpress


