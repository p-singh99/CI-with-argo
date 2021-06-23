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


