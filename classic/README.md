## Kubernetes deployment

  

### Create kubernetes deployment

The alpine-tor-deployment.yaml can be used to create an deployment which ensures 1 running running pod and uses a service to expose 9050 via NodePort.

  

To create the service and deployment run

  

```

kubectl create -f alpine-tor-deployment.yaml

```

The result should look like

  

```

service/alpine-tor-service created

deployment.apps/alpine-tor created

```

  

In order to be able to connect to the socks proxy you'll need to note down the automatically assigned port. Run the below command to view the ports

  

```

kubectl get service alpine-tor-service

```

  

Which should look like

```

NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE

alpine-tor-service NodePort 10.152.183.117 <none> 9050:30848/TCP 82s

```

  

You can test the proxy by running

```

curl -x socks5h://${ExternalNodeIP}:30848 -L http://ifconfig.me

```

  

### Delete kubernetes deployment

```

kubectl delete -f alpine-tor-deployment.yaml

```