# Sample application to demonstrate usage of Keda with Apache Kafka
(Fork from https://github.com/ChamilaLiyanage/kafka-keda-example. In this sample, We upgrade Keda to 2.4.0 and deploy Kafka on Minikube.)

## Deploying KEDA on Minikube
Please refer to https://keda.sh/docs/2.4/deploy/#helm

## Deploying Kafka on Minikube
Please fefer to https://strimzi.io/quickstarts/

## Create Kafka Topic for demo
```
kubectl exec -it --namespace=kafka my-cluster-kafka-0 -- bash bin/kafka-topics.sh --create --topic test --partitions 5 --replication-factor 1 --bootstrap-server localhost:9092
```

## Build the Java Projects
```
mvn clean install
```

## Build the Docker images (Windows Hyper-v)
Open Powershell window with administrator privilege
```
minikube docker-env
minikube -p minikube docker-env | Invoke-Expression
docker build -t kafka-producer kafka-producer/
docker build -t kafka-consumer kafka-consumer/
```

## Deploying Kafka-producer
```
kubectl create -f kafka-producer/deployment.yaml
```

## Deploying Kafka-consumer
```
kubectl create -f kafka-consumer/deployment.yaml
```

## Create the Kafka Scaled Object
```
kubectl create -f kafka-scaled-object.yaml
```
You'll find out that eventually the pod number of Kafka-consumer decrease to 0.


Use command kubectl port-forward/pods/kafka-producer-deployment... 8090:8090 -n default to expose the service.
Accessing http://localhost:8090/orders/50 will produce 50 messages. Wait till pod numbers of kafka-consumer 
decreate to 9, then change 50 to 60, 100, 150, 200, 300, or 1000 etc, find out how the pod numbers changes.
