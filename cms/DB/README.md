## DB 설치 및 이중화
1. 이미지 가져오기
```
sudo podman pull postgresql:latest
```

2. db_deployment.yaml 작성
```yaml
apiVersion: v1
kind: Service
metadata:
  name: postgresql
  namespace: springtest
spec:
  selector:
    app: postgresql
  ports:
    - protocol: TCP
      port: 5432
      targetPort: 5432
      nodePort: 30203
  type: NodePort

---
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: postgresql
  namespace: springtest
spec:
  serviceName: "postgresql"
  replicas: 2
  selector:
    matchLabels:
      app: postgresql
  template:
    metadata:
      labels:
        app: postgresql
    spec:
      containers:
        - name: postgresql
          image: docker.io/library/postgres:latest
          ports:
            - containerPort: 5432
          env:
            - name: POSTGRES_DB
              value: dbtest
            - name: POSTGRES_USER
              value: knn
            - name: POSTGRES_PASSWORD
              value: knnnps2011
          volumeMounts:
            - name: postgresql-storage
              mountPath: /var/lib/postgresql/data
          resources:
            requests:
              memory: "500Mi"
              cpu: "100m"
  volumeClaimTemplates:
    - metadata:
        name: postgresql-storage
      spec:
        accessModes: ["ReadWriteOnce"]
        resources:
          requests:
            storage: 2Gi
```

3. yaml 배포
```
kubectl apply -f db_deployment.yaml
```
4. service 및 컨테이너 배포 확인
```
kubectl get service -n springtest
kubectl get statefulset -n springtest
```
5. 컨테이너 접속
```
kubectl exec -it <컨테이너ID> /bin/bash
```
6. sql 접속
```
psql -U knn -d dbtest
```
7. 계정 정보 확인
```
\du
```
8. 테이블 접근
```
\c dbtest knn
```
9. 테이블 생성
```
CREATE TABLE star (
id integer NOT NULL,
name character varying(255),
class character varying(32),
age integer,
radius integer,
lum integer,
magnt integer,
CONSTRAINT star_pk PRIMARY KEY (id)
);
```
10. 테이블 생성 확인
```
\dt
```
11. pod 삭제
```
kubectl delete statefulset -n springtest <테이블 생성한 pod name>
```
12. pod 생성 확인
```
kubectl get pods -n springtest
```
13. 컨테이너 접속
```
kubectl exec -it <컨테이너ID> /bin/bash
```
14. sql 접속
```
psql -U knn -d dbtest
```
15. DB 테이블 접근
```
\c dbtest knn
```
16. 테이블 확인
```
\dt
```
