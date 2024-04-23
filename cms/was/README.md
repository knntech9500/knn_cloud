## was 설치 및 배포
1. sudo podman pull tomcat:9.0.55-jdk11
2. was deployment 작성
 ```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: tomcat-deployment
  namespace: springtest
spec:
  replicas: 2
  selector:
    matchLabels:
      app: tomcat
  template:
    metadata:
      labels:
        app: tomcat
    spec:
      containers:
      - name: tomcat
        image: tomcat:9.0.55-jdk11
        ports:
        - containerPort: 8080
        env:
        - name: TOMCAT_USERNAME
          value: admin
        - name: TOMCAT_PASSWORD
          value: admin123

   ```
3. was_tomservice.yaml
```yaml
apiVersion: v1
kind: Service
metadata:
  name: tomcat-service
  namespace: springtest
spec:
  selector:
    app: tomcat
  ports:
  - protocol: TCP
    port: 80
    targetPort: 8080
    nodePort: 30300
  type: NodePort
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
