# nest-js-api-practice-deploy

GitOps deploy repo for [nest-js-api-practice](https://github.com/vadym-dubykhvist/nest-js-api-practice).

ArgoCD watches this repo and reconciles cluster state to whatever is in `main`.

## Layout

```
applications/         ArgoCD Application CRDs (one per env)
  nestjs-dev.yaml
environments/         Per-env Helm values
  dev/
    values.yaml
```

## How it works

1. Helm chart lives in the app repo (`chart/`).
2. Application CRDs here point at: chart in app repo + values from this repo.
3. CI in the app repo bumps `image.tag` here on every `v*` tag → ArgoCD picks it up → deploys.

Do not edit cluster state by hand — push to this repo instead.
