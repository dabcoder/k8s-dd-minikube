# k8s-dd-minikube

### Start minikube and use its Docker daemon:

```
minikube start
...
eval $(minikube docker-env)
```


### Build the web app Docker image  

`cd` in the `web` directory. Then run:

```
docker build -t web-flask:v1 .
```


### Create a Deployment that manages a Pod that runs a Container based on the web-flask:v1 Docker image:

Flask uses the port `5000` by default.

```
kubectl run web-flask --image=web-flask:v1 --port=5000
```

### Pull the latest Redis Docker image

```
docker pull redis:latest
```


### Create a Deployment that manages a Pod that runs a Container based on the redis:latest Docker image:

Redis will use the port `6379`.

```
kubectl run redis --image=redis:latest --port=6379
```

### Create Services

```
kubectl expose deployment web-flask --type=LoadBalancer
kubectl expose deployment redis --type=LoadBalancer
```

### Run the web app

```
minikube service web-flask
```

