# Rancher login reusable action

It will install and setup rancher cli and login to rancher server. 
It will optionally install also `kubectl` to run raw k8s commands against
the cluster.

## Inputs

### `url`

Target url of rancher server. e.g. `https://rancher.example.com/v3`

### `token`

Token to authenticate against server.

### `context`

Numeric project identifier to select as login context.

### `rancher_version`

Version of `rancher` cli to install. Default `2.6.7`.

### `kubectl`

Whether to install also `kubectl` or not. Default `true`.

### `kubectl-version`

Version of `kubectl` to install. Default `1.25.0`.

## Example usage in a workflow

```yaml
on: [push]

jobs:
  rancher:
    name: Login with rancher and kubectl
    runs-on: ubuntu-latest
    steps:
      - uses: fabn/rancher-login-action@v1
        with:
          token: ${{ secrets.RANCHER_TOKEN }}
          url: ${{ secrets.RANCHER_URL }}
          context: ${{ secrets.RANCHER_CONTEXT }}
      - run: rancher --version
      - run: rancher ps
      - run: kubectl version --short  
```
