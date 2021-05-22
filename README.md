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

