KUBERNETES - K8S
Kubernetes is not a extended version of Docker.
Kubernetes is a cluster based Technology.
Docker is a containerization platforms and has individual lifecycle and has been managed by Docker Swarm previously. Due to lack of Orchestration of containers in docker swarm, it was replaced by Kubernetes.
Kubernetes is a container orchestration platform.It has many in-built properties.

Why Kubernetes? What are the problems will be solved by K8s?
Docker swarm has lot of drawbacks but some of major failures listed below:

Problem 1: Single Host in Docker:
Docker container is Ephemeral (short lived). It will die and revive at any time.
Eg) If there are 100 containers in a single host OS, first some containers consumes more CPU & Memory utilization, which will trouble the other containers to survive and will not start the new container due to no resource availability.
So, any container may die or new container will not start.

What is Auto - Healing?
Without any manual intervention, container will start by itself.

Problem 2: No Auto-Healing in Docker:
If any one or more containers killed accidentally by any of the reasons, Application hosted in that container will not be accessible to users and it causes a huge downtime and delay.

Problem 3:No Autoscaling with Load Balancer:
HPA - Horizontal Pod Autoscaling
Auto-scaling - Automatically scales up/ down the instances when getting the loads.

Docker swarm Drawback:
In Docker Swarm, we having Manual scaling alone using replicas number to be scaled up/down(containers in few number). But it will not be possible for lakhs requests. Hence we are moving to K8s.
Additionally, Docker swarm has inbuilt load balancer feature. Using that it can serves to users with only existing IP address alone.
i.e, if a container becomes unhealthy, then inbuilt load balancer can't identifies and eliminate it instead lod balancer keeps on routing the requests to unhealthy container and the application becomes unresponsive.

Kubernetes feature:
It has HPA which results in Highly available Auto-scaling and serves the scaling up new containers out with its new IP addresses to users through load balancer by actively sending response to healthy containers and removes the unhealthy one.

Problem 4: Not Supports high Enterprise applications:

Docker is a light-weight container as its resources and OS are being shared which restricts docker to support Enterprise level.Absence of Firewall, Auto-scaling,load balancer,Auto Healing.

Does Kubernetes can install and work in a single Machine?
Yes, it can - but it would be in a development environment i.e., staging, UAT. but not in production environment.
In Development phase we can use Minikube and not in production mode. For interview purpose we should not say that we have worked in Minikube.

single Host- testing
Master Node and worker Node - production

How kubernetes resolves above mentioned problems in Single Host?

If any container is getting down, the K8 Master will up this container in a same or different node. If it is a faulty node, then K8s will start this application or pods into another node.

Kubernetes has old Feature Replica sets where we can change replicas option from 1 to 10 which is a manual scaling. However, it also has HPA. Whenever the load gets increased, HPA will spin up the pods as loads.

Kubernetes will control and fix the damage. when any one of pod is getting down then K8s API server will receive a signal that pods is getting down. Then API server will roll out a new pod before the faulty pod is down.

