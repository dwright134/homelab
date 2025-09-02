# Talos
## Required Software
To install the required software on a client run the following commands.
```
brew install siderolabs/tap/talosctl
brew install talhelper
brew install kubectl
brew install fluxcd/tap/flux
```
Optional software
```
brew install k9s
```
## Bootstrap the cluster
The cluster uses flux for configuration. We need to bootstrap the cluster to pull this repo.
```
kubectl create namespace flux-system
cat {{.SOPS_AGE_KEY_FILE}} | kubectl -n flux-system create secret generic sops-age --from-file=age.agekey=/dev/stdin
export GITHUB_TOKEN=<github token>
flux bootstrap github --token-auth --owner=dwright134 --repository=homelab --branch=master --path=cluster/flux/ --personal=true
```
