# k8-s-command
Useful short command to perform better in CKA exam

- To create a pod using run cmd

`kubectl run nginx --image=nginx`
`kubectl run nginx --image=nginx -o yaml --dry-run=client > pod.yaml`

- To check the number of pods running in the defautl ns

`kubectl get po`

- what is the image use to create the pod

`kubectl describe po nameofpod | grep -i image`

- To check the details infor for pods like nodename, IP use **-o wide**

`kubectl get po -o wide`

## Replica Set

- To check the replica set

`kubectl get rs`

- To create a rs

check rs.yaml file

- save this file and use

`kubectl apply -f filename.yaml`

- To scale the rs to 5

`kubectl scale --replicas=5 rs/nameofrs`

`kubectl edit rs nameofrs`
and change the replicas option

- To create the deployment check deployment.yaml

OR

`kubectl create deployment nginx --image=nginx`

and scale it using replicas=xx

`kubectl scale deployment --replicas=3 nginx`

- Namespaces
  - Default
  - Kube-System
  - Kube-public

  - To check the ns count 

  `kubectl get ns --no-headers | wc -l`

  - To check pods in a ns

  `kubectl get po --namespace=test`

- To create a pod in test ns

`kubectl run nginx --image=nginx --namespace=test --dry-run=client --dry-run=client -o yaml > red.yml`
- To switch to a ns and use it always by default use

`kubectl config set-context $(kubectl config current-context) --ns=test`

- To get all the po info

`kubectl get po --all-namespaces`

- To check the services in cluster

` kubectl get svc`

- To check the Target port configued for a svc

`kubectl describe svc kubernetes | grep -i target`

- To create svc for existing deployment use

`kubectl expose deployment nameofdeployment --name=nameofsvc --targetport=80 --type=Node/lbtype --port=80 --dry-run=client > servic.yaml`

  - and edit to add the nodePort section in spec ports section

- To create a pod and svc in one command with the same name as nginx use --expose. Below will create a pod nginx and svc nginx expose on port 80 using cluterIP

`kubectl run nginx --image=nginx --expose --port 80`

- TO check the default component for control-plane master use this

`kubectl get po --namespace kube-system`

- To find a pod with selector ex, env=prod

`kubectl get po --selector env=prod`