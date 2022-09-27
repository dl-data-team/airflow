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

### Crear volumen for dags:

  ```bash
  kubectl apply -f dags_volume.yaml
  ```
  
  
