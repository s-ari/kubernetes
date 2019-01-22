# Create jenkins pods

### Setup jenkins docker image.

* Enter variable of the gcp project id.

```
export GCP_PROJECT_ID=""
export DATE=$(date "+%Y%m%d%H%M%S")

docker pull jenkins:alpine
docker tag jenkins:alpine gcr.io/${GCP_PROJECT_ID}/jenkins:${DATE}
gcloud docker -- push gcr.io/${GCP_PROJECT_ID}/jenkins:${DATE}
```

### Setup persistent volume.

```
gcloud compute disks create --size=10GB --zone=us-west1-a jenkins-home
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

### Service deployment.

```
kubectl -f servie.yaml
```
