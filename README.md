# NOTES
In this simple kubernetes pod deployment we will understand the creation of a pod and NodePort Service, creating both yaml configuration files. After that, we will clone the repository to our cluster and we will apply it.

## Theory
### Objectos
Pod: Runs a single sets of containers with a very specific configuration. Good for some dev porpuses but not so useful for prod.
Deployment: Runs a set of identical Pods. Monitors the state of each pod. It is good both for dev and prod.
Services: Runs a set of instruction for networking.
  - ClusterIP: Exposes the Service on a cluster-internal IP. Choosing this value makes the Service only reachable from within the cluster. This is the default ServiceType.
  - NodePort: Exposes the Service on each Node's IP at a static port (the NodePort). A ClusterIP Service, to which the NodePort Service routes, is automatically created. You'll be able to contact the NodePort Service, from outside the cluster, by requesting <NodeIP>:<NodePort>.
  - NodePort: Exposes the Service on each Node's IP at a static port (the NodePort). A ClusterIP Service, to which the NodePort Service routes, is automatically created. You'll be able to contact the NodePort Service, from outside the cluster, by requesting <NodeIP>:<NodePort>.
  - ExternalName: Maps the Service to the contents of the externalName field (e.g. foo.bar.example.com), by returning a CNAME record with its value. No proxying of any kind is set up.

## Practical

### Clone repository
git clone https://github.com/Sarony11/first_simplek8s.git

With this command we are cloning this same repository and all files contained. We will need these files to apply them in our k8s cluster.

### Apply yaml files
sudo microk8s kubectl apply -f client-pod.yaml
sudo microk8s kubectl apply -f client-node-port.yaml

In both cases, we expect to get a message saying that the application of the yaml configuration file was created or updated (in case it was already created and running). If an error arise, the most common cause is because the yaml file has some spelling or sintax errors, so we would need to chekc them again using documentation.

### Get information status to check results
sudo microk8s kubectl get pods
sudo microk8s kubectl get services

With these commands, we are able to get actual information about our kubernetes. With the "get pods" command, we will see our pod named client-pod. With "get services" we will see two different services. One called kubernetes that belongs to the k8s cluster and the one created by use, called client-node-port.

sudo microk8s kubectl describe pod <service_pod_optional>
sudo microk8s kubectl describe service <servce_name_optional>

These commands will give us very tons of information about the services describe. if you want to be more precise, you can add the name of the object to narrow the information given.

### Visit the website
Visit http://<kubernetes_ip>:31515

You should be able to access to a simple react website.
