# Helm notes

Most helm charts are hosted on the Artifact hub https://artifacthub.io/

### Adding a helm repo
1. Add the chart repo using `helm repo add <local-repo-name> <helm-chart-link>`
2. Execute `helm repo update`

### Installing a helm chart from the web
- `helm install <deployment-name> <local-repo-name>/<chart-name>`

### Installing a helm chart from a local folder
- `helm install <deployment-name> <chart-directory-path>`

### Pulling helm chart
- `helm pull <local-repo-name>/<chart-name> --untar`
--untar will decompress the file to produce the helm folder in one step

### Upgrading helm chart
1. You need to create yaml values file seperate that the default one to avoid mis configuring your cluster in the future when you upgrade the chart to a newer version
2. `helm upgrade <deployment-name> --values=newvalues.yaml` this will make helm use the default values unless there is an override in our values

### Uninstalling Helm chart
- `helm uninstall <deployment-name>`

### Generating yaml files from a chart to be directly installed on our kubernetes cluster
1. `helm template <name> <chart-directory-path> --values=newvalues.yaml > template-name.yaml` the output is a file that can be deployed using kubectl