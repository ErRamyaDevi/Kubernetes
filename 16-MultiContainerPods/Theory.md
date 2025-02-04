
## Multi Container Pods:
+ Kubernetes pods can have single or Multiple containers.
+ Multi-container usage:- why?
Container A wants to connect with container B.
Container A wants to share the Network with container B.
Container A wants to share the location/storage, file with container B.
+ two or more containers inside a single pod can communicate via local host.

## Demo -single container in single pod

```
sudo -i
cd pods_and_container
sudo nano single-container.yaml

kubectl apply -f single-container.yaml
kubectl get pods -o wide
kubectl exec -it one-container -- curl http://192.168.235.139:80
```
## Now you can see the "403 forbidden error" as we can't communicate the other container.
![image](https://github.com/user-attachments/assets/11406e63-6e2f-4688-919c-51812bbc7871)

Remove the single container and run the multi-container pod now.

```
sudo -i
cd pods_and_container
sudo nano multi-container.yaml
kubectl apply -f multi-container.yaml
kubectl get pods -o wide
kubectl exec -it two-containers --curl http://192.168.235.140:80

![image](https://github.com/user-attachments/assets/d651cb84-d693-43cb-9882-09fbcfaeca72)
## Now I can able to access. Because after the multi-container the volume has been shared. second container mounted volume has the custom index.html
