# Setup the k8s cluster

## Create a Secret file

* Create a secret (for MySQL and Postgres)

```
kubectl create secret generic postgres-pass --from-literal=password=<password>
kubectl create secret generic mysql-pass --from-literal=password=<password>
kubectl create secret generic onem2m --from-literal=origin=<origin>
```

* Apply the ConfigMap for the MySQL and PostgreSQL init scripts

```
kubectl apply -f mysql-configmap.yml -f postgres-configmap.yml
```

* Apply MySQL, PostgreSQL and Mobius deployment

```
kubectl apply -f mysql-deployment.yaml -f mobius-deployment.yaml -f postgres-deployment.yaml -f onem2m-recorder-deployment.yaml
```

# Commands used to create the config files

## Create the ConfigMap file

* Create ConfigMap from a file 

```
kubectl create configmap mysql-init-db --from-file=./data/mobiusdb.sql
```

* Dump ConfigMap into a yaml file (then `kubectl apply` it as any other config file)

```
kubectl get configmaps mysql-init-db -o yaml > mysql-configmap.yml
```

# Misc useful commands

* Get pods

```
kubectl get pods
```

* Get a shell into a container

```
kubectl exec -it mosquitto -- /bin/sh
```

* Get services

```
kubectl get services
```

* View a pod logs

```
kubectl logs mobius-6f699d8f8d-4h967
```

* Get the URL of a service running into Minikube

```
minikube service mobius --url
```
