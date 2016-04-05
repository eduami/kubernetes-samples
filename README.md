# kubernetes-samples
#Useful commands
##Have kubernetes scripts in the path
	export PATH=/Users/choba02/work/k8s/kubernetes/cluster:$PATH
 
##Get all pods
	kubectl get pods
 
##Create a ngnix server
	kubectl.sh run my-nginx --image=nginx --replicas=2 --port=80 --expose --service-overrides='{ "spec": { "type": "LoadBalancer" } }'
##To find the public IP address assigned to your application, execute:
  kubectl.sh get service/my-nginx
##To know more about service  
	kubectl.sh describe service/my-nginx 
##To know more about deployment
	kubectl.sh describe deployment/my-nginx 
##To delete existing deployment and service
	kubectl delete deployment,service my-nginx
## Create a pod from configuration file
	 kubectl create -f ./hello-world.yaml  
## View output or logs of the pod
	kubectl logs  hello-world  





#Tips
###READY coloumn shows how many containers are avilable in a POD
	kubectl get pods 
	NAME          READY     STATUS    RESTARTS   AGE
	hello-world   0/1       Pending   0          0s