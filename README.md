# Udagram Image Filtering Microservice
Udagram is a simple cloud application developed alongside the Udacity Cloud Engineering Nanodegree. It allows users to register and log into a web client, post photos to the feed, and process photos using an image filtering microservice.

### Create Docker Images and run it locally
* Build the images:
```
docker-compose -f docker-compose-build.yaml build --parallel
```
* Starting the app as a container on a local system:
```
docker-compose up
```
* to share those images through the Docker Hub:
```
docker-compose -f docker-compose-build.yaml push
```
The docker hub images used in this project: [rafiktchek/reverseproxy](https://hub.docker.com/r/rafiktchek/reverseproxy), [rafiktchek/udacity-restapi-feed](https://hub.docker.com/r/rafiktchek/udacity-restapi-feed), [rafiktchek/udacity-restapi-user](https://hub.docker.com/r/rafiktchek/udacity-restapi-user), [rafiktchek/udacity-frontend](https://hub.docker.com/r/rafiktchek/udacity-frontend).

### Deploy the application to to a kubernetes cluster

1. First we create the infrastructure (kubernetes cluster) using the AWS management console.

2. Setup the credentials & secrets:
```
kubectl apply -f env-configmap.yaml
kubectl apply -f aws-secret.yaml
kubectl apply -f env-secret.yaml
```

3. Launch the deployments and the services in your Kubernetes cluster as follows:
```
kubectl apply -f backend-feed-deployment.yaml
kubectl apply -f backend-user-deployment.yaml
kubectl apply -f frontend-deployment.yaml
kubectl apply -f reverseproxy-deployment.yaml

#Launch the services
kubectl apply -f backend-feed-service.yaml
kubectl apply -f backend-user-service.yaml
kubectl apply -f frontend-service.yaml
kubectl apply -f reverseproxy-service.yaml
```
