# Google Compute Engine Node Helloworld
The goal of this example is to turn a simple Hello World node.js app into a replicated application running on Kubernetes.

## Node.js application
You can find a simple Node.js helloworld application in the server.js file.

## Docker image
A simple Docker image can be built using the provided Dockerfile.
### Build Docker image
Build an image of your container by running *docker build*, tagging the image with the Google Container Registry repo for your PROJECT_ID

<code>
docker build -t gcr.io/PROJECT_ID/hello-node:v1 .
</code>

and push it to your private Google Container Registry

<code>
gcloud docker push gcr.io/PROJECT_ID/hello-node:v1
</code>

## Create your Pod
<code>
kubectl run hello-node --image=gcr.io/PROJECT_ID/hello-node:v1 --port=8080
</code>
### Allow external traffic
By default, the pod is only accessible by its internal IP within the Kubernetes cluster. 

In order to make the hello-node container accessible from outside the kubernetes virtual network, you have to expose the pod as a kubernetes service.

<code>
kubectl expose deployment hello-node --type="LoadBalancer"
</code>

Source: http://kubernetes.io/docs/hellonode/
