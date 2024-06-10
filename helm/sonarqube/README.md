## Building the sonarqube dockerimage uring Girlab
- The sonarqube image is built from my [Gitlab repo](https://gitlab.com/cafanwi_group/docker/-/tree/main/sonarqube?ref_type=heads)

- Here is the image :  
repository: cafanwii/sonarqube
  tag: 1.0.0

- My database is external: [sonarqubeprod]

- create a secret with database details.

## Downloading the helm chart and updating detains in values file

```bash
helm repo add sonarqube https://SonarSource.github.io/helm-chart-sonarqube
helm repo update
kubectl create namespace sonarqube
helm search repo
helm pull sonarqube/sonarqube --untar=true
```

## update values file and install chart

```sh
helm install -n sonarqube sonarqube sonarqube/sonarqube
```