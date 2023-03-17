<!-- PROJECT LOGO -->
<br />
<p align="center">
 

  <h2 align="center"> Deploying an Application on Kubernetes with ingress and test it on browser with ngrok 🐳 ❄ </h2>

  <p align="center">
    Using ingress to deploy a Node.js application on Kubernetes and ngrok to test application on a browser. Build Kubernetes using Minikube and manage Docker Container using Pods, Deployment, Services, and ingress manifest files
    <br />
    <br />

  </p>
</p>



<!-- TABLE OF CONTENTS -->
## Table of Contents

* [About the Project](#about-the-project)
* [Getting Started](#getting-started)
  * [Prerequisites](#prerequisites)
  * [Installation](#installation)
 
* [Contact](#contact)

<!-- ABOUT THE PROJECT -->
## About The Project
Here's important point of this assignment:
Using ingress to deploy a Node.js application on Kubernetes and with ngrok test application on a browse. 
Build Kubernetes using Minikube and manage Docker Container using Pods, Deployment, Services, and ingress manifest files

<!-- GETTING STARTED -->
## Getting Started

To get a local copy up and running follow these simple example steps.

### Prerequisites 

1. AWS EC2 instance.

2. Docker.

3. Minikube.

4. K8s Manifest Files. (Deployment ,service ,ingress)

## Installation:

1. Create AWS EC2 instance of ubuntu OS image.

2. Install Docker on Ubuntu.

3. Install Minikube which uses Docker as driver.

Ref : https://medium.com/@sanjuthamke9699/day-31-task-launching-your-first-kubernetes-cluster-using-minikube-49e7ddef9ade

4. Minikube runs as a Docker Container to server the purpose of K8s.

5. Github url: https://github.com/sanjanathamke/Kubernet_Project.git

## Steps:

### 1. Create namespace and check it created or not using below commands

```sh
kubectl create namespace <namespace-name>
kubectl get namespaces
```
### 2. Create one Deployment file to deploy a sample app on K8s using “Auto-healing” and “Auto-Scaling” feature

add a deployment.yaml file use namespace as kubeproject
apply the deployment to your k8s (minikube) cluster by command kubectl apply -f deployment.yaml

```sh
kubectl apply -f deployment.yaml -n <namespace-name>
```



### 3. Create service file of type loadbalancer


Apply the LoadBalancer Service definition to your K8s (minikube) cluster using the below command

```sh
kubectl apply -f load-balancer-service.yaml -n <namespace-name>

```



### 4. Verify that the LoadBalancer Service is working by accessing the todo-app from outside the cluster in your Namespace.

Get the LoadBalancer IP service:

The minikube service command is used to interact with services in a Minikube cluster. The — url option will return the URL that you can use to access the Service in your browser.

```sh
minikube service <service_name> -n=<namespace> --url

```

Note the LoadBalancer IP address of the LoadBalancer Service you want to verify.

Access the todo-app from outside the cluster using the LoadBalancer IP and the exposed port:
```sh
curl -L <load-balancer-ip>:<service-port>
curl -L http://http://192.168.49.2:31188
```


If the LoadBalancer Service is working correctly, you should see the response from the app


### 5. An Ingress is an API object that defines rules which allow external access to services in a cluster

To enable the NGINX Ingress controller, run the following command:
```sh
minikube addons enable ingresss

```


create ingress.yaml file and apply ingress file


Create the Ingress object by running the following command

```sh
kubectl apply -f ingress.yaml -n <namespace-name>

```

Note the LoadBalancer IP address of the LoadBalancer Service

```sh
minikube service <service-name> -n <namespace-name> --url
```



Add the following line to the bottom of the /etc/hosts file on your computer (you will need administrator access):


```sh
192.168.49.2 nodejs-todo-app.info

```



Verify that the Ingress controller is directing traffic:

```sh
curl -L http://nodejs-todo-app.info
```



### 6. To test Kubernetes application on browser we use tool — ngrok

ngrok is a cross-platform application that enables developers to expose a local development server to the Internet with minimal effort. It creates a secure tunnel from the public internet to a local web server on your computer, making it possible to access the local web server from anywhere in the world.

Go to ngrok site, In that right click on Linux and copy link address


Create a new folder for ngrok setup, inside folder use command wget <copied_linux_address> this command will download ngrok.

wget https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-v3-stable-linux-386.tgz


unzip downloaded file using :

```sh
 tar -xvzf <file_name>
```



Add authentication — Running below command will add your authtoken to the default ngrok.yml configuration file

```sh

./ngrok config add-authtoken 2N5jh4oJTnp0xM4z3ktc1JYeaAF_7agSW56UrMKSVNCshmBdu
 
```


Use command :

```sh

./ngrok http 192.168.49.2:31188
 
```

./ngrok http 192.168.49.2:31188 to make a tunnel. Here http 192.168.49.2:31188 is url of a service given by minikube service.


above command creates a tunnel and gives IP address which is ended with ngrok.io
Copy and paste that ip in your browser.
click on visit site and your website will visible 




<!-- CONTACT -->
## Contact

Sanjana Thamke - www.linkedin.com/in/sanjana-thamke-68827417b - My LinkedIn

Project Link: https://medium.com/@sanjuthamke9699/kubernetes-project-c1faded2499f



