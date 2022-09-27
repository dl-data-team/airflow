# airflow
Deploy Airflow on Kubernetes with Helm

### Create namespace:

  ```bash
  kubectl create namespace airflow
  ```

You should see in the console this: `namespace/airflow created`

### Create secret in namespace:

  ```bash
  kubectl -n airflow create secret generic my-webserver-secret --from-literal="webserver-secret-key=$(python3 -c 'import secrets; print(secrets.token_hex(16))')"
  ```

### Create pv for dags:

  ```bash
  kubectl apply -f dags_volume.yaml
  ```
  
### Add and update the Airflow helm repository:

  ```bash
  helm repo add apache-airflow https://airflow.apache.org && helm repo update
  ```
  
### Install Airflow:

  ```bash
   helm install airflow apache-airflow/airflow --namespace airflow --debug -f values.yaml
  ```
  
### Accessing the UI:

The following command forwards the port 8080 on the webserver pod (through its service or svc) to port 8080 on your machine. Navigate to http://localhost:8080 to view the UI and see your DAGs.

 ```bash
  kubectl port-forward svc/airflow-webserver 8080:8080 -n airflow  
 ``` 
 
 
