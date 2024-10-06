# Creating and managing helm templates

### Creat new chart
- `helm create <chart-name>` the outputs are: charts, templates folders, .helmignore, Chart.yaml and values.yaml files

#### Files breakdown
- Chart.yaml: is the metadata for the chart. in other words it holds a useful information about the chart that the end user will find useful
- templates directory: Holds the files that defines the resources and will be processed to create the deployable yaml file

### Generating yaml files from a chart to be directly installed on our kubernetes cluster
1. `helm template <chart-directory-path> > template-name.yaml` the output is a file that can be deployed using kubectl