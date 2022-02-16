# Tekton Pipelines and Triggers example

This repo is an example for Tekton Triggers and is based over Tekton Pipelines article, it intended to bridge the gap of the Tekton documentation and the Tekton newbie.

```
README.md
apps
 ┣ argocd
 ┃ ┗ sampleapp-api.yaml
 ┗ sampleapp-api
 ┃ ┣ templates
 ┃ ┃ ┣ tests
 ┃ ┃ ┃ ┗ test-connection.yaml
 ┃ ┃ ┣ NOTES.txt
 ┃ ┃ ┣ _helpers.tpl
 ┃ ┃ ┣ deployment.yaml
 ┃ ┃ ┣ hpa.yaml
 ┃ ┃ ┣ ingress.yaml
 ┃ ┃ ┣ service.yaml
 ┃ ┃ ┗ serviceaccount.yaml
 ┃ ┣ .helmignore
 ┃ ┣ Chart.yaml
 ┃ ┣ values.modified.yaml
 ┃ ┣ values.production.yaml
 ┃ ┗ values.yaml
ci
 ┣ conf
 ┃ ┣ docker
 ┃ ┃ ┗ config.json
 ┃ ┣ sonarqube
 ┃ ┃ ┗ sonar-project.properties
 ┃ ┗ ssh
 ┃ ┃ ┣ config
 ┃ ┃ ┣ id_rsa
 ┃ ┃ ┗ known_hosts
 ┣ mandatory
 ┃ ┣ namespace.yaml
 ┃ ┣ pipeline-account.yaml
 ┃ ┣ secrets.yaml
 ┃ ┣ task-build.yaml
 ┃ ┣ task-git-cli.yaml
 ┃ ┣ task-git-clone.yaml
 ┃ ┣ task-sonarqube-scanner.yaml
 ┃ ┗ task-yaml-edit.yaml
 ┣ sampleapp-api
 ┃ ┣ pipeline-run.yaml
 ┃ ┣ pipeline.yaml
 ┃ ┗ task-test.yaml
 ┗ triggers
 ┃ ┣ webhook-event-listener.yaml
 ┃ ┣ webhook-ingress.yaml
 ┃ ┗ webhook-service-account.yaml
```    
    
    
#### Install TektonCD Pipelines
Follow [this instructions](https://github.com/tektoncd/pipeline/blob/main/docs/install.md#installing-tekton-pipelines-on-kubernetes)

## Tekton

### Install Tekton resources
[install from here](https://github.com/tektoncd/pipeline/blob/main/docs/install.md#installing-tekton-pipelines-on-kubernetes)

```
kubectl apply --filename https://storage.googleapis.com/tekton-releases/pipeline/latest/release.yaml
kubectl apply --filename https://storage.googleapis.com/tekton-releases/triggers/latest/release.yaml
kubectl apply --filename https://storage.googleapis.com/tekton-releases/triggers/latest/interceptors.yaml

```

### Install Tekton CLI tkn

[install from here](https://github.com/tektoncd/cli)

### Install Tekton dashboard

[Install from here](https://github.com/tektoncd/dashboard/blob/main/docs/install.md)
```
kubectl apply --filename https://storage.googleapis.com/tekton-releases/dashboard/latest/tekton-dashboard-release.yaml
```

Enter the Dashboard via:

```
kubectl proxy
http://localhost:8001/api/v1/namespaces/tekton-pipelines/services/tekton-dashboard:http/proxy/
```


### Using the TKN CLI
Get the tasks
```
tkn tasks list
```

Delete tasks
```
tkn tasks delete <taskname>
```

Get the Taskrun
```
tkn taskrun list
```

Delete taskrun
```
tkn taskrun delete <taskrun name>
```
Get the taskriun logs

```
tkn taskrun logs -f <taskrun name>
```