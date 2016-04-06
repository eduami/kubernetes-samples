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
## Deleting Deployment
	kubectl delete deployment/my-nginx
###Get all pods with lablel run
	kubectl get pods -L run
### Get all deployments with label run
	kubectl get deployment/my-nginx -L run
### Get pods that are running on a node
	kubectl get pods -l run=my-nginx -o wide
### Get pod ips
	kubectl get pods -l run=my-nginx -o yaml | grep podIP	
### Create Service for the pods
	kubectl expose deployment/my-nginx
### To know more about service
	kubectl get svc my-nginx
### Get end points for the pods (i.e) pod access ports
	kubectl get ep my-nginx
### Get the environment variables of contatiner running in a pod
	kubectl.sh exec my-nginx-3800858182-23j2c -- printenv	
### Delete all the pods or scale down to zero
	kubectl scale deployment my-nginx --replicas=0
### Manually increase the no of pods
	kubectl scale deployment my-nginx --replicas=2
###  Verify whether skydns service is running or not in your cluster
	kubectl get services kube-dns --namespace=kube-system

#Tips
###READY coloumn shows how many containers are avilable in a POD
	kubectl get pods 
	NAME          READY     STATUS    RESTARTS   AGE
	hello-world   0/1       Pending   0          0s

###Replicas
Unlike in the case where you directly create pods, a Deployment replaces pods that are deleted or terminated for any reason, such as in the case of node failure. For this reason, we recommend that you use a Deployment for a continuously running application even if your application requires only a single pod, in which case you can omit replicas and it will default to a single replica

###--cascade=false
By default delete deployment  will also cause the pods managed by the Deployment to be deleted. If there were a large number of pods, this may take a while to complete. If you want to leave the pods running instead, specify --cascade=false