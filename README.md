# kubernetes-full-stack-example
Source code for blog post https://nirajsonawane.github.io/2020/04/25/Deploy-React-Spring-Boot-MongoDB-Fullstack-application-on-Kubernetes/

1. Create the Kubernetes config-map from the application.properties file. Remove the application.props files 
   after running this otherwise it will still be used in the app

     ``kubectl create configmap ../k8s/student-app-api-configmap.yaml --from-file=src/main/resources/application.properties``
2. Build the the app   
   ``mvn clean build``

3. Create the docker image

   ``docker build -t  johnhunsley/student-app-api ./``
4. If you don't have a Docker hub account and personal repository then create one here:
   https://hub.docker.com/
5. Login to Docker from your cmd line so you can push the image

   ``docker login --username <username> --password <password>``
6. Push the image to the docker hub repo 

   ``docker push johnhunsley/student-app-api``
7. Build the Kubernetes resources - mongo and the student api

   ``./k8s/student-api-mongo.sh``
8. expose the port from the minikube host to the ingress   
      ``sudo minikube tunnel``
9. Make a curl request into the api

   ``curl -v -X GET http://10.109.194.223/api/students``
10. After successfull build and push to docker hub, update the deployment and force a new pod and image pull
   
    ``kubectl rollout restart deployment/student-app-api``

[![CircleCI](https://dl.circleci.com/status-badge/img/gh/johnhunsley/kubernetes-full-stack-example/tree/master.svg?style=svg)](https://dl.circleci.com/status-badge/redirect/gh/johnhunsley/kubernetes-full-stack-example/tree/master)
