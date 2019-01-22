# Create Ops tools pods

### Setup persistent volume on GCP.

```
gcloud compute disks create --size=1GB --zone=us-west1-a ansible-home
gcloud compute disks create --size=1GB --zone=us-west1-a serverspec-home
```

### Edit docker image.

* Your Docker image repogitory.

```
vi deployment.yaml

---
image: <YOUR DOCKER IMAGE>:<TAG>
```

### Pod deployment.

```
kubectl -f deployment.yaml
```
