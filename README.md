# kubernetes-full-stack-example
Source code for blog post https://nirajsonawane.github.io/2020/04/25/Deploy-React-Spring-Boot-MongoDB-Fullstack-application-on-Kubernetes/

1. Build the the app   
   ``mvn clean build``

2. Create the docker image

   ``docker build -t  johnhunsley/student-app-api ./``
3. Push the image to the docker hub repo 

   ``docker push johnhunsley/student-app-api``
4. Build the Kubernetes resources - mongo and the student api

   ``./k8s/student-api-mongo.sh``
5. expose the port from the minikube host to the ingress   
      ``sudo minikube tunnel``
6. Make a curl request into the api

   ``curl -v -X GET http://10.109.194.223/api/students``
7. After successfull build and push to docker hub, update the deployment and force a new pod and image pull
   
   ``kubectl rollout restart deployment/student-app-api``

[![CircleCI](https://dl.circleci.com/status-badge/img/gh/johnhunsley/kubernetes-full-stack-example/tree/master.svg?style=svg)](https://dl.circleci.com/status-badge/redirect/gh/johnhunsley/kubernetes-full-stack-example/tree/master)
