# Python Service

## Developer Guide

### <a name="installation"></a>Installation

#### Required Software

| Software       | URL                                                    |
|----------------|--------------------------------------------------------|
| Python 3.10.11 | https://www.python.org/downloads/release/python-31011/ |
| Poetry         | https://python-poetry.org/docs/                        |
| Docker         | https://docs.docker.com/get-docker/                    |

#### Application Setup

* Clone from GitHub
  ```shell
  git clone git@github.com:go-gsd/demo.git
  ```
* Change directory
  ```shell
  cd demo
  ```
* Create Python environment and install dependencies
  ```shell
  poetry install
  ```

### <a name="running"></a>Running

* The following command will obtain user access credentials and put them in `$HOME/.config/gcloud/application_default_credentials.json`
  ```
  gcloud auth application-default login
  ```
* Copy the `.env.template` file and name it `.env`
* The `.env.template` uses the sandbox environment and has most configuration values.

#### Run using Python

* Activate the Python environment
  ```shell
  poetry shell
  ```
* _Note: To exit a Python environment use the following command_
  ```shell
  exit
  ```
* Start the application
  ```shell
  uvicorn app.main:app --reload
  ```

#### Run using Docker

* Start with `docker-compose`:
  ```shell
  docker compose up --build
  ```
* Check to see if the application is running
  ```shell
  curl localhost:8000
  ```

### <a name="analysis"></a>Static Analysis

#### Please run the following before committing code:

* `flake8` to resolve linting issues
  ```shell
  poetry run flake8
  ```
* `radon` to get complexity score (1-5: A-perfect, 6-10: B-low, 11-20: C-moderate, 21-30: D-high, 31+: F-unstable)
  ```shell
  poetry run radon cc app -na --total-average
  ```
* `black` to format code
  ```shell
  poetry run black .
  ```

### <a name="documentation"></a>Documentation

* View the Swagger Documentation
    ```shell
    http://localhost:8000/docs
    ```

### <a name="troubleshooting"></a>Troubleshooting

#### Configure the `gcloud` command line tool to connect to a Google Cloud environment and GKE cluster:

* Create a `gcloud` configuration (using the sandbox project as an example, where `<account>` is your BCG email address)
    ```shell
    gcloud config configurations create prj-python-demo
    gcloud config set project prj-python-demo-sbx-3839 --configuration prj-python-demo
    gcloud config set account <account> --configuration prj-python-demo
    ```
* Activate a `gcloud` configuration
    ```shell
    gcloud config configurations activate prj-python-demo
    ```
* Update `$HOME/.kube/config` to point kubectl to the `prj-python-demo-a1ff0d61` GKE cluster
    ```shell
    gcloud container clusters get-credentials prj-python-demo-a1ff0d61 --region us-east1
    ```

#### Remote Environment

* Port-forward to the running pod
    ```shell
    kubectl -n lh port-forward $(kubectl get pods -n lh | ggrep Running | ggrep demo-service | awk '{print $1}') 8010:80
    ```
* Tail logs from the running pod
    ```shell
    kubectl -n lh logs -f $(kubectl get pods -n lh | ggrep Running | ggrep demo-service | awk '{print $1}')
    ```
* SSH into the running pod
    ```shell
    kubectl -n lh exec -it $(kubectl get pods -n lh | ggrep Running | ggrep demo-service | awk '{print $1}') -- /bin/sh
    ```
* Restart the running pod
    ```shell
    kubectl -n lh delete pod $(kubectl get pods -n lh | ggrep Running | ggrep demo-service | awk '{print $1}')
    ```

### Local Environment (developer workstation)

* SSH into a running Docker container
    ```shell
    docker exec -it <container id>
    ```
