# docker-ghost-ai
Uses original ghost image https://hub.docker.com/_/ghost/ as base image and adds App-Insights support.

# usage
docker build https://github.com/keyoke/docker-ghost-ai.git --file 3/alpine/ai/DOCKERFILE --tag ghost-custom

# Azure Container Registry Tasks

## Run task ad-hoc

az acr task run --registry [ACR Name] --file acr-task-3.yaml https://github.com/keyoke/docker-ghost-ai.git

## Schedule task (Commit & base image trigger)

az acr task identity assign --registry [ACR Name] --name docker-ghost-ai --identities "[Managed Identity Resource Id]"

az acr task create --registry [ACR Name] --name docker-ghost-ai --file acr-task-3.yaml --context https://github.com/keyoke/docker-ghost-ai.git --branch master --git-access-token [Github PAT] --set aksRG=[AKS RG] --set aksName=[AKS NAME] --set aksDeploymentName=[AKS DEPLOYMENT NAME] --set aksContainerName=[AKS CONTAINER NAME]

az acr task run --registry [ACR Name] --name docker-ghost-ai

az acr task list-runs --registry [ACR Name] --output table