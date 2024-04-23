## DB 설치 및 이중화
이미지 가져오기
```
sudo podman pull postgresql:latest
```

db_deployment.yaml
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
          image: harbor.192.168.118.138.nip.io/test/postgres:v2
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
