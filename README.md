# Sample application to demonstrate usage of Keda with Apache Kafka
(Fork from https://github.com/ChamilaLiyanage/kafka-keda-example)

## Deploying KEDA on Minikube
Please refer to https://keda.sh/docs/2.4/deploy/#helm

## Deploying Kafka on Minikube
Please fefer to https://strimzi.io/quickstarts/

## Create Kafka Topic for demo
```
kubectl apply -f kafka-topic.yaml
```

## Build the Java Projects
```
mvn clean install
```

## Build the Docker images (Windows Hyper-v)
Open Powershell window with Administrator
```
minikube docker-env
minikube -p minikube docker-env | Invoke-Expression
docker build -t kafka-producer kafka-producer/
docker build -t kafka-consumer kafka-consumer/
```

