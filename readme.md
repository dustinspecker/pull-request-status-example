# pull-request-status-demo

> Proof of concepts around external systems providing status for commits and pull requests with
> test results.

View pull requests to see examples.

## Kind/Flux CD setup

1. Create a kind cluster via `kind create cluster`
1. Create a [GitHub PAT](https://github.com/settings/tokens?type=beta) that has the following permissions:
  - Administration: Read and write
  - Contents: Read and write
  - Metadata: Read-only
1. Follow [Get Started with Flux](https://fluxcd.io/flux/get-started/) up until "Install Flux onto your cluster".
1. Bootstrap Flux by running:
   ```bash
   flux bootstrap github \
     --owner=$GITHUB_USER \
     --repository=fleet-infra \
     --branch=main \
     --path=./clusters/my-cluster \
     --personal \
     --private=false
   ```
1. Clone the fleet-infra repository by running:
   ```bash
   git clone git@github.com:$GITHUB_USER/fleet-infra.git
   cd fleet-infra
   ```
1. Make modifications as desired, commit, and push.
1. Watch Flux CD sync via:
   ```bash
   flux get kustomizations --watch
   ```
