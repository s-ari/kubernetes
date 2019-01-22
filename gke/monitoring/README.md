# Create monitoring services.

## Influxdb

* Create persistent disk in GCP.
* Add configmap of influxdb.conf.
* Create service and pod for influxdb.

```
gcloud compute disks create --size=1GB --zone=us-west1-a influxdb-home
kubectl create configmap influxdb.conf --from-file=influxdb.conf=./influxdb.conf
kubectl create -f influxdb_deployment.yaml
```

* Create DB and user for a cadvisor in an influxdb after attach an influxdb pod.

```
kubectl exec -it <POD NAME> sh
influx
CREATE DATABASE cadvisor
CREATE USER cadvisor IDENTIFIED BY '<YOUR PASSWORD>';
show database
show users
```

* Caution !!
  * This influxdb manifest allow admin interface but it is testing files.
    Disable admin setting value: "false".

```
        env:
        - name: INFLUXDB_ADMIN_ENABLED
          value: "true"
```

## Cadvisor

* Create damonset and nodeport service for a cadvisor.
* If use a web interface, allow a firewall of 8080 port of gcp instances.

```
kubectl create -f cadvisor.yaml
```

## Grafana

* Create persistent disk in GCP.
* Create service and pod for grafana.

```
gcloud compute disks create --size=1GB --zone=us-west1-a grafana-home
kubectl crate -f grafana.yaml
```

* Setting grafana for influxdb database soruce.

```
http://influxdb:8086
```
