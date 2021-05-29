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

** Taint and Toleration

- To check if a node has toleration enable or not use. By default master/control plane node has toleration enabled and this is the reason no pod schedule there

`kubectl describe nodes node01 | grep -i taint`

- To schedule a taine on a node use

`kubectl taint NODE NAME KEY_1=VAL_1:TAINT_EFFECT_1(NoSchedule)`

- To check the spec of a pod you can use --recursive option

`kubectl explain po --recursive| less`

### Monitoring cluster

- To check the logs for a pod and multiple container in a pod

`kubectl logs -f podname` `kubectl logs -f podname container name` 

- To deploy a monitoring metric-server

(github)[git clone https://github.com/kodekloudhub/kubernetes-metrics-server.git]

- To check the max cpu utilization for po and node

`kubect top node/po`

#### Deployment

- To check update the deployment use the edit command

`kubectl edit deployment.v1.apps/nginx-deployment`

- To check the rollout status

`kubectl rollout status deployment/nginx-deployment`

- To undo a deployment rollout

`kubectl rollout undo deployment.v1.apps/nginx-deployment`

- Config map are used as env var to use with the pod. ex like with Db pod for hostname/port(key:value)To create a config map

`kubectl create configmap NAME [--from-file=[key=]source] [--from-literal=key1=value1] [--dry-run=server|client|none]`

- To create secret use declaratice way as in secret.yml file or use

`kubectl create secret name --from-literal key=value`

- To add a secret in a pod check secretpod.yml file 

