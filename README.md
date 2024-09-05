# rabbitmq-cluster-kubernetes

![image](https://github.com/user-attachments/assets/8dbf7c04-f843-41cd-94e1-32ed3e1095d9)

## RABBITMQ CLUSTER OPERATOR

first you need install rabbitmq cluster operator. you can use various method

with directly manifest you can use below

```
kubectl apply -f "https://github.com/rabbitmq/cluster-operator/releases/latest/download/cluster-operator.yml"
```

but i think best and easy way krew plugins. you can install krew via their site. ```https://krew.sigs.k8s.io/docs/user-guide/setup/install/```

then install rabbitmq plugin.

```kubectl krew install rabbitmq```

after installing cluster opreator

```kubectl rabbitmq install-cluster-operator```

you can check from CRDs for rabbitmq operator.

```kubectl get customresourcedefinitions.apiextensions.k8s.io | grep rabbitmq```

## RABBITMQ CLUSTER

final part is easist part.

you can use this yaml or change what you want. below yaml file install 1 replica rabbitmq cluster with NodePort you can change with your requirements.
for AWS you can use directly storageclass.

```
apiVersion: rabbitmq.com/v1beta1
kind: RabbitmqCluster
metadata:
  labels:
    app: rabbitmq
  name: rabbitmqcluster
spec:
  replicas: 1
  service:
    type: NodePort
  persistence:
    storageClassName: gp2
    storage: 10Gi
```

!!! if you want to use onpremise solution and there is no storage solution. you must to create pv by yourself with non-storage-definiton.yaml

then apply and your cluster is ready to go.

```kubecolor apply -f rabbitMQ.yaml```

you can find user and password on secrets. 



