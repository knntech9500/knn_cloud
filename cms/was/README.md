## was 설치 및 배포
1. sudo podman pull tomcat:9.0.55-jdk11
2. was_tom.yaml
3. was_tomservice.yaml
4. ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: was-test6
     namespace: springtest
   spec:
     replicas: 2
     selector:
       matchLabels:
         app: was-app
     template:
       metadata:
         labels:
           app: was-app
       spec:
         containers:
         - name: lanzam-was6
           image: harbor.192.168.118.138.nip.io/test/was:v1
           command: ["/bin/sh", "-ec", "while :; do echo 'Hello World'; sleep 5 ; done"]
           ports:
           - containerPort: 8080
         imagePullSecrets:
           - name: harbor-credentials
   ```




5. asdasd
6. ```
7. kubectl get apply -f was_tom.yaml
8. kubectl get apply -f was_tomservice.yaml
9. kubectl get service -n springtest
10. kubectl get pods -n springtest
11. kubectl exec -it <컨테이너ID> /bin/bash
12. mv ./webapps ./webapps2
13. mv ./webapps.dist ./webapps
