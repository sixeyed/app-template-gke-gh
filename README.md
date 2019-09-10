# app-template-gke-gh

Docker App Template for deploying to GKE using GitHub Actions

## Pre-reqs

You need a version of [Docker Desktop](https://www.docker.com/products/docker-desktop) with [Application Templates](https://blog.docker.com/2019/07/application-templates-docker-desktop-enterprise/) enabled.

Your GitHub account needs to be approved for [GitHub Actions](https://help.github.com/en/articles/about-github-actions) (currently in beta).

Then create an empty repo and set the following secrets (under _Settings...Secrets_):

- `GCP_SA_KEY_ENCODED` - base64 encoded JSON key for your GCP [Service Account](https://console.cloud.google.com/apis/credentials/serviceaccountkey)
- `GCP_PROJECT_ID` - ID of the GCP project where GKE will be deployed
- `GCP_ZONE` - GCP zone for deployment
- `DOCKER_HUB_USERNAME` - username for Docker Hub pushes
- `DOCKER_HUB_PASSWORD` - password for Docker Hub pushes

## Setup

Copy `gke-gh-library.yaml` from this repo to somewhere useful:

```
cp gke-gh-library.yaml /tmp
```

Update your App Template config in `~/.docker/application-template/preferences.yaml` to include the new template library. 

This example includes the local demo libraries and the main Docker library:

```
apiVersion: v1alpha1
disableFeedback: false
kind: Preferences
repositories:
- name: gke-gh-library
  url: file:///tmp/gke-gh-library.yaml
- name: library
  url: https://docker-application-template.s3.amazonaws.com/production/v0.1.1/library.yaml
```

## Run

> TODO