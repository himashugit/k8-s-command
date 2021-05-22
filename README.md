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