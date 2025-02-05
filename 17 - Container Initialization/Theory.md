## Init Container:
#### when a pod deploys an application to UI, there will be a downphase. At that time, a dummy container will be invoked default before our application container run.
#### Dummy container-->container Initialize (Init container) -->pre-checks the db,network connectivity.Till the Init containers completes its pre-check activity, application container will not be come into picture.
#### Init containers can be many not only one.

➢ Init Containers are specialized containers that run before app containers in a Pod.

➢ Init Container only run once during the start-up process of Pod.

➢ Init containers can contain utilities or setup scripts not present in an app image.

➢ User Can define N Number of Init Container in Pod.

![364616052-6620dc04-36c0-4025-b62e-d665310d45e6](https://github.com/user-attachments/assets/61c33485-4a1a-441b-8fc5-6375d9479d2c)


## Init Containers: Use Case

➢ SetUp the Application Init or SetUp Scripts.

➢ Init containers offer a mechanism to block or delay app container startup until a set of preconditions are met.

➢ Init containers can securely run utilities or custom code that would otherwise make an app container image less secure.

➢ Populate Data at Shared Volume before Application StartUp.

# Demo - Init Container

```
sudo -i
cd pods_and_containers
sudo nano init-containers.yaml
(paste the code) https://github.com/ErRamyaDevi/Kubernetes/blob/main/17%20-%20Container%20Initialization/Init-container.yaml
kubectl apply -f init-containers.yaml
kubectl get pods -o wide
kubectl logs example-pod<podname> -c main-app
```

![image](https://github.com/user-attachments/assets/cc8f6a05-671d-4883-9d01-0b098385f5ab)

> [!Note]
> When we use K8 cluster, please enable master node and worker node. Master node containers will always be deployed in worker node.
