## Init Container:
when a pod deploys an application to UI, there will be a downphase. At that time, a dummy container will be invoked default before our application container run.
Dummy container-->container Initialize (Init container) -->pre-checks the db,network connectivity.Till the Init containers completes its pre-check activity, application container will not be come into picture.
Init containers can be many not only one.

➢ Init Containers are specialized containers that run before app containers in a Pod.

➢ Init Container only run once during the start-up process of Pod.

➢ Init containers can contain utilities or setup scripts not present in an app image.

➢ User Can define N Number of Init Container in Pod.

