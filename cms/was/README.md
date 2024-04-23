## was 설치 및 배포
1. sudo podman pull tomcat:9.0.55-jdk11
2. was_tom.yaml
3. was_tomservice.yaml
4. kubectl get apply -f was_tom.yaml
5. kubectl get apply -f was_tomservice.yaml
6. kubectl get service -n springtest
7. kubectl get pods -n springtest
8. kubectl exec -it <컨테이너ID> /bin/bash
9. mv ./webapps ./webapps2
10. mv ./webapps.dist ./webapps
