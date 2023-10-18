## Build workflow
A new Docker image build will be triggered every time a push is made to the `main` branch. This container image is pushed to a GitHub container registry in this GitHub repository

## Release workflow
Triggered every time a push is made to main, but only creates a new chart release if the chart version changes. Pushes the release to a registry in this repository

## Deployment instructions
1. Add Helm repository

```helm repo add sre-challenge https://StefanBS.github.io/sre-challenge```

2. Install Helm chart in `sre-challenge` namespace

```helm install sre-challenge sre-challenge/sre-challenge -n sre-challenge --create-namespace```

The app is made available through an ingress:

```kubectl get ingress -l app=sre-challenge -n sre-challenge```

## Upgrading Helm chart
```helm upgrade sre-challenge sre-challenge/sre-challenge -n sre-challenge```

## Decisions
Each exercise was implemented in a PR:
1. Pipelines: https://github.com/StefanBS/sre-challenge/pull/1
2. Kubernetes: https://github.com/StefanBS/sre-challenge/pull/2
3. Documentation: https://github.com/StefanBS/sre-challenge/pull/3

### High availability
Created a HPA for the web app based on cpu utilization and replication from 2 to 4 instances. Deployed Redis Sentinel in two pods

### Security
Added password authentication to Redis. The password is created on the first Helm install as a secret

## Improvements
- A basic Helm chart test is implemented. This test could be improved by adding a health-check endpoint to the app that checks there is communication with Redis
- The Helm chart test could be integrated into the `release` GitHub workflow or a PR workflow
- Using a HTTPS ingress endpoint
