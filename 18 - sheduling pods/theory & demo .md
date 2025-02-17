### Scheduling Pods:-
  + scheduling is the process of assigning pods to nodes, so that kubectl can run them.
  + scheduler: It is a component on K8 Master node, which decides the pod assignment on nodes.
    
### Scheduling process:-
  + K8 scheduler select the suitable nodes for pods.(suitable nodes - healthy, free etc.)
  + other than above K8 default metrics (Healthy, free), we can have some customized metrics also which is termed as "Resource Request".
    
### Resouce Request:-
  + If you define a resource request 4 CPU and 2 GiB Memory then scheduler will allocate this pod to the worker node which meets the requirement. If the required nodes are still busy with pods, then scheduler will keep the new incoming pods in pending state untill 4 CPU and 2 GiB node gets free.

### Node Label:-
  + If you define label of the node in the pod manifest yaml file, then scheduler assign this pod to the particular worker node.

### Node selector:-
  + NodeSelector is define in Pod Spec to limit which Node(s) the pod can be scheduled on.
  + NodeSelector use Labels to select the suitable Node.
### Node Name:-
  + User can bypass scheduling and assign Pod to a Specific Node using Node Name.
  + NodeName is typically is not good option to use for Pod scheduling due to its limitations. (Dynamically any worker node down and new worker node will be join to the cluster)



# Demo - Node selector:-

```
sudo -i
mkdir pods_allocation
cd pods_allocation
nano nodeselector.yaml

kubectl apply -f nodeselector.yaml
kubectl get pods -o wide
kubect describe pod nginx-nodeselector
```

![image](https://github.com/user-attachments/assets/ae2b12d2-b2fb-43fa-b197-519edc2504df)
Its Failed scheduling due to missed label "disktype=ssd" in any worker nodes.

*What are the labels are attached to the cluster?*
```
kubectl get nodes --show-labels
```
![image](https://github.com/user-attachments/assets/ae75215f-ef01-48ee-b091-5a7c0bf0ea71)
*How to assign the label to the particular worker node?*
```
kubectl label nodes <hostname> disktype=ssd
kubectl get nodes --show-labels
```

![image](https://github.com/user-attachments/assets/0f8be97a-96c6-4dad-ae69-3026e8d89543)
