# Build workflow
A new Docker image build will be triggered every time a push is made to the `main` branch. This container image is pushed to a GitHub container registry in this GitHub repository

# Release workflow
Triggered every time a push is made to main, but only creates a new chart release if the chart version changes. Pushes the release to a registry in this repository

# Deployment instructions
1. Add Helm repository
```helm repo add sre-challenge https://StefanBS.github.io/sre-challenge```

2. Install Helm chart in `sre-challenge` namespace
```helm install sre-challenge sre-challenge/sre-challenge -n sre-challenge --create-namespace```

# Upgrading Helm chart
```helm upgrade sre-challenge sre-challenge/sre-challenge -n sre-challenge```

# Decisions
## High availability
Created a HPA for the web app based on cpu utilization and replication from 2 to 4. Deployed Redis Sentinel in two pods.

## Security
Added password authentication to Redis. The password is created on the first Helm install as a secret
