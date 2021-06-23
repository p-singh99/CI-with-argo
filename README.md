# CI-with-argo

Create a Continuous Integration pipeline using Argo Events and Argo workflows

## Install Argo Workflows

1) Create a Namespace for Argo Workflows
  - kubectl create ns argo

2) Apply the quick start manifest to install commonly used components
  - kubectl apply -n argo -f https://raw.githubusercontent.com/argoproj/argo-workflows/stable/manifests/quick-start-postgres.yaml

3) Forward port for Workflows UI
  - kubectl -n argo port-forward deployment/argo-server 2746:2746
  - https://localhost:2746/

4) If deploying on cloud, follow the instructions at - https://argoproj.github.io/argo-workflows/argo-server/#access-the-argo-workflows-ui

5) Download the Argo CLI
  - curl -sLO https://github.com/argoproj/argo/releases/download/v3.0.8/argo-darwin-amd64.gz
  - gunzip argo-darwin-amd64.gz
  - chmod +x argo-darwin-amd64
  - mv ./argo-darwin-amd64 /usr/local/bin/argo

## Install Argo Events

1) Create a Namespace for Argo Events
  - kubectl create namespace argo-events

2) Deploy Argo Events and other components (EventBus, EventSource)
  - kubectl apply -f https://raw.githubusercontent.com/argoproj/argo-events/stable/manifests/namespace-install.yaml

3) Deploy the Eventbus
  - kubectl apply -n argo-events -f https://raw.githubusercontent.com/argoproj/argo-events/stable/examples/eventbus/native.yaml

## Apply the necessary Yaml files

1) Apply the Event Source
  - kubectl -n argo-events apply -f ${event-source.yaml}

2) Apply the Sensor
  - kubectl -n argo-events apply -f ${sensor.yaml}

3) Expose the Event Source
  - kubectl -n argo-events port-forward ${event-source-pod-name} 12000:12000

4) Test out the hook using curl
  - curl -d '{"message":"this is my first webhook"}' -H "Content-Type: application/json" -X POST http://localhost:12000/example

5) Check the workflow status
  - kubectl -n argo-events get wf


