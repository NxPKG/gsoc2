# ONPREM code
* Onprem means it's supposed to be ran on a server of the customer, and not in the cloud. These are tweaked to hit the API and look for new work throughout workflows. Everything is handled by the initial main.go, which launches the others.

## orborus.go - Handles NEW workflows - Same as WALKOFF UMPIRE
* Executes and controls the docker environment used by workers. 
* A worker is deployed for every execution. 
* The apps are responsible for callbacks to the backend themselves.
* After the worker is deployed / running, the execution ID is removed from the workflowqueue API.

# worker/worker.go - one for each workflow requiring onprem stuff 
* Handles a workflow from start to finish as long as the action ID. 
* Starting and stopping APPS in docker.

# app_sdk
* The new APP sdk based on https://github.com/nsacyber/WALKOFF/tree/1.0.0-alpha.1/app_sdk
* Fully functional with WALKOFF apps, which means its also functional with Cloud Function apps (these are now essentially the same with a few small tweaks)

# Images - all valid images are located here currently
https://hub.docker.com/r/gsoc2/gsoc2

## Setup with Dockerhub
Requred - access to: https://hub.docker.com/r/docker/gsoc2/gsoc2/general
Login:
```
docker login
```

Update worker: 
```
cd worker
docker build . -t gsoc2/gsoc2:worker
docker push gsoc2/gsoc2:worker
```

Update app_sdk:
```
cd app_sdk
docker build . -t gsoc2/gsoc2:app_sdk
docker push gsoc2/gsoc2:app_sdk
```


Update app_sdk_kali:
```
cd app_sdk_kali
docker build . -t gsoc2/gsoc2:app_sdk_kali
docker push gsoc2/gsoc2:app_sdk_kali
```


Update app_sdk_blackarch:
```
cd app_sdk_blackarch
docker build . -t gsoc2/gsoc2:app_sdk_blackarch
docker push gsoc2/gsoc2:app_sdk_blackarch
```