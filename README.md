# Setup the k8s cluster

Apply (default and weak !) secret (see https://kubernetes.io/docs/concepts/configuration/secret/ to create one with a __real__ password)

```
kubectl apply -f mysql-secret.yaml
```

Create the ConfigMap with the MySQL init script

```
kubectl apply -f mysql-configmap.yml
```

Deploy MySQL and Mobius

```
kubectl apply -f mysql-deployment.yaml -f mobius-deployment.yaml
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
