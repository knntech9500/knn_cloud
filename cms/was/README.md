## was 설치 및 배포
1. sudo podman pull tomcat:9.0.55-jdk11
2. was_tom.yaml
3. was_tomservice.yaml
4. ```
5. asdasd
6. ```
7. kubectl get apply -f was_tom.yaml
8. kubectl get apply -f was_tomservice.yaml
9. kubectl get service -n springtest
10. kubectl get pods -n springtest
11. kubectl exec -it <컨테이너ID> /bin/bash
12. mv ./webapps ./webapps2
13. mv ./webapps.dist ./webapps
