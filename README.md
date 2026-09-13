# Deployment-using-APACHE

- Deployed a test application using Apache on K8 kind clusters.
- Tested HPA and autoscaling of replicas with load-generator
- Ports:
  - Procol: TCP
  - port: 80 (exposed port in the cluster)
  - targetPort 80 (container port)
 
--> sudo -E kubectl port-forward service/apache-service -n apache 82:80 --address=0.0.0.0
--> AWS -> running instance -> new inbound rule was added in the security group to allow traffic on port 82 (which is mapped to targetPort 80) - this is TCP too

    Testing autoscaling of replicas using a load generator:
kubectl run -I --tty load-generator --image=busybox -n apach /bin/sh
/#   while true; do wget -q -O- http://apache-service.namespace.svc.cluster.local; done

(-i -> interactive terminal, --tty -> wait for your response, busybox -> single file containing hundreds of unix & linux cli tools, the url is for accessing apache service {on port 82})
