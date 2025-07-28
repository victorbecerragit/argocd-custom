```yaml

# Use this setup to overwritte the default installation of ArgoCD from scratch using Helm Charts.

mkdir charts/argo-cd
Add Chart.yaml and values.yaml


Disable the dex component (integration with external auth providers).

Disable the notifications controller (notify users about changes to application state).

Disable the ApplicationSet controller (automated generation of Argo CD Applications).

We start the server with the --insecure flag to serve the Web UI over HTTP. For this tutorial, we're using a local k8s server without TLS setup.

argo-cd:
  dex:
    enabled: false
  notifications:
    enabled: false
  applicationSet:
    enabled: false
  server:
    extraArgs:
      - --insecure

 # Install the ArgoCD chart locally , download all the dependences to avoid errors.

$ helm repo add argo-cd https://argoproj.github.io/argo-helm

$ helm dep update charts/argo-cd/


Hang tight while we grab the latest from your chart repositories...
...Successfully got an update from the "argo-cd" chart repository
Update Complete. ⎈Happy Helming!⎈
Saving 1 charts
Downloading argo-cd from repo https://argoproj.github.io/argo-helm
Deleting outdated charts


This will create the Chart.lock and charts/argo-cd-<version>.tgz files. The .tgz file is only required for the initial installation from our local machine. To avoid accidentally committing it, we can add it to the gitignore file:

echo "charts/**/charts" >> .gitignore


# Install your Helm Chart

$ helm install argo-cd charts/argo-cd/

