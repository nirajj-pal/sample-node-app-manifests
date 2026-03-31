# sample-node-app-manifests

GitOps manifests repository for the sample Node.js application.

## Repository layout

```text
base/
  deployment.yaml
  service.yaml
  kustomization.yaml
overlays/
  dev/
  staging/
  prod/
argocd/
  sample-node-app-dev.yaml
  sample-node-app-staging.yaml
  sample-node-app-prod.yaml
```

## What Jenkins updates

Jenkins updates this file by default:

- `overlays/dev/kustomization.yaml`

Specifically, Jenkins updates the `images[].newTag` value with a new immutable image tag after a successful build.

## What you must change before use

Replace `your-github-org` in these files:

- `overlays/dev/kustomization.yaml`
- `overlays/staging/kustomization.yaml`
- `overlays/prod/kustomization.yaml`
- `argocd/sample-node-app-dev.yaml`
- `argocd/sample-node-app-staging.yaml`
- `argocd/sample-node-app-prod.yaml`
- `base/deployment.yaml`

## Argo CD apply commands

Install the applications after Argo CD is installed:

```bash
kubectl apply -f argocd/sample-node-app-dev.yaml
kubectl apply -f argocd/sample-node-app-staging.yaml
kubectl apply -f argocd/sample-node-app-prod.yaml
```

## Promotion approach

- `dev` can be updated automatically by Jenkins
- `staging` should be promoted by Pull Request
- `prod` should be promoted by Pull Request and approval

## Suggested GitHub repo name

`sample-node-app-manifests`
