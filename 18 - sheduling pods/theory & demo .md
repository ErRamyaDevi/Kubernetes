Scheduling Pods:-
  + scheduling is the process of assigning pods to nodes, so that kubectl can run them.
  + scheduler: It is a component on K8 Master node, which decides the pod assignment on nodes.
Scheduling process:-
  + K8 scheduler select the suitable nodes for pods.(suitable nodes - healthy, free etc.)
  + other than above K8 default metrics (Healthy, free), we can have some customized metrics also which is termed as "Resource Request".
Resouce Request:-
  + if you define a resource request 4 CPU and 2 GiB Memory then scheduler will allocate this pod to the worker node which meets the requirement. If the required nodes are still busy with pods, then scheduler will keep the new incoming pods in pending state untill 4 CPU and 2 GiB node gets free.

Node Label:-
  + if you define label of the node in the pod manifest yaml
