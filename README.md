# NOTES
In this simple kubernetes pod deployment we will understand the creation of a pod and NodePort Service, creating both yaml configuration files. After that, we will clone the repository to our cluster and we will apply it.

## Clone repository
git clone https://github.com/Sarony11/first_simplek8s.git

With this command we are cloning this same repository and all files contained. We will need these files to apply them in our k8s cluster.

## Apply yaml files
sudo microk8s kubectl apply -f client-pod.yaml
sudo microk8s kubectl apply -f client-node-port.yaml

In both cases, we expect to get a message saying that the application of the yaml configuration file was created or updated (in case it was already created and running). If an error arise, the most common cause is because the yaml file has some spelling or sintax errors, so we would need to chekc them again using documentation.

## Get information status to check results
sudo microk8s kubectl get pods
sudo microk8s kubectl get services

With these commands, we are able to get actual information about our kubernetes. With the "get pods" command, we will see our pod named client-pod. With "get services" we will see two different services. One called kubernetes that belongs to the k8s cluster and the one created by use, called client-node-port.

## Visit the website
Visit http://<kubernetes_ip>:31515

You should be able to access to a simple react website.
