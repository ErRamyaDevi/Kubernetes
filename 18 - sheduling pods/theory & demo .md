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

https://github.com/ErRamyaDevi/Kubernetes/blob/main/18%20-%20sheduling%20pods/nodeselector.yaml

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

Now, Failed scheduling has been successfully assigned - So pod has been is active now.

# Demo - Node Name:-
```
cd pods_allocation
nano nodename.yaml

https://github.com/ErRamyaDevi/Kubernetes/blob/main/18%20-%20sheduling%20pods/nodename.yaml

kubectl apply -f nodename.yaml
kubectl get pods -o wide
```
![image](https://github.com/user-attachments/assets/cfe852fd-e665-44a0-9a7a-a72e13d2057a)

My nodename pod has been assigned to the particular node what I mentioned in nodename yaml file.

# Demo - Resource Request:-
```
cd pods_allocation
nano resource-request1.yaml

https://github.com/ErRamyaDevi/Kubernetes/blob/main/18%20-%20sheduling%20pods/resource-request1.yaml

//Here this pod will assign to the worker node which has "disktype=ssd and mem - 64 MB & cpu - 1000m"
//disktype=ssd - This label already assigned to the worker node called worker1

kubectl apply -f resource-request1.yaml
kubectl get pods -o wide
```

![image](https://github.com/user-attachments/assets/f4865939-2f3f-4def-83f4-836d3f525075)

This pod also assigned to the same worker1 node.

Lets copy the same pod yaml and name it as resource-request3.yaml . Run it again and check whether it is assigned to the same worker node1 or not
```
nano resource-request3.yaml

https://github.com/ErRamyaDevi/Kubernetes/blob/main/18%20-%20sheduling%20pods/resource-request3.yaml

kubectl apply -f resource-request3.yaml
kubectl get pods -o wide
```
![image](https://github.com/user-attachments/assets/8712992d-2705-456d-b6b3-6e6677644410)

This pod is still pending. Because this pod meet first dependency that is "disktype=ssd" and it cant able to meet the cpu & mem dependency. So it cant able to assign the pod.

Let run one more pod without node selector "disktype=ssd"
```
cd pods_allocation
nano resource-request2.yaml

https://github.com/ErRamyaDevi/Kubernetes/blob/main/18%20-%20sheduling%20pods/resource-request2.yaml

kubectl apply -f resource-request2.yaml
kubect get pods -o wide
```

![image](https://github.com/user-attachments/assets/f57a6a63-1e70-430f-b37a-ec7038ca81e2)

This pod definetely will assign to another node. Because this yaml doesn't mention any label like "disktype=ssd".so the scheduler will assign to the available nodes(free nodes).
