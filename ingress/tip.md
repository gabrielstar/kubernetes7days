https://kubernetes.io/docs/tasks/access-application-cluster/ingress-minikube/
https://kubernetes.io/docs/concepts/services-networking/ingress/#load-balancing

#What is ingress?

An ingress controller is a piece of software that provides reverse proxy, configurable traffic routing, and TLS termination for Kubernetes services. Kubernetes ingress resources are used to configure the ingress rules and routes for individual Kubernetes services. Using an ingress controller and ingress rules, a single IP address can be used to route traffic to multiple services in a Kubernetes cluster.

[./ingress.png]

#Requires k8 1.19

Sample:

#Prepare
#Create deployment from img
kubectl create deployment web --image=gcr.io/google-samples/hello-app:1.0
#Expose port to  on k8 interface 
kubectl expose deployment web --type=NodePort --port=8080
#Get service details
kubectl get service web
#Visit it using minikube shortcut (via IP)
minikube service web --url


#Make sure ingress on
minikub addons list
minikube addons enable ingress
#Add ingress
kubectl apply -f https://k8s.io/examples/service/networking/example-ingress.yaml
kubectl get ingress 
#wait until ADDRESS is populated
NAME              CLASS    HOSTS   ADDRESS           PORTS   AGE
example-ingress   <none>   *       192.168.148.211   80      31m

#On windows - specify host to point to minikube IP
minikube ip 
192.168.148.211
Add C:\Windows\System32\drivers\etc\hosts:
192.168.148.211 hello-host.info

under 192.168.148.211 or hello-host.info we will see our page now
curl hello-host.info
StatusCode        : 200

#WARNING - it can takes up minutes first time so wait a few minutes for ingress to come 

#One can add default backend to route non-existing paths to

Now, let us add 2nd deployment for simple LB scenario as on teh image.
kubectl create deployment web2 --image=gcr.io/google-samples/hello-app:2.0
kubectl expose deployment web2 --port=8080 --type=NodePort

add path to ingress now.