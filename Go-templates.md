# Creating and managing helm templates

### Creat new chart
- `helm create <chart-name>` the outputs are: charts, templates folders, .helmignore, Chart.yaml and values.yaml files

#### Files breakdown
- Chart.yaml: is the metadata for the chart. in other words it holds a useful information about the chart that the end user will find useful
- templates directory: Holds the files that defines the resources and will be processed to create the deployable yaml file

### Generating yaml files from a chart to be directly installed on our kubernetes cluster
1. `helm template <chart-directory-path> > template-name.yaml` the output is a file that can be deployed using kubectl

### Functions
There are a list of functions that you can use in the templates and all is listed here https://helm.sh/docs/chart_template_guide/function_list/

- function syntax is {{ function-name args }}
  
One of the most important functions is the default
- {{ default "default-value" user-defined-value }}

### Pipelines
Pipelines are used to chain functions together just like linux pipelines
- {{ value | function | another-function }}

### Conditional statement
- `{{ if eq value-of-variable specific-value }}true-expression{{ else }}false-expression{{ end }}`
This evaluates to if a value-of-variable equals a specific-value then the true-expression will be the right one, else false-expression

### Named or sub templates
Is a block of Yaml that you want to use multiple times
1. create a file in the template folder with the following convention _whatever-name.tpl or .yaml it is not important really  
The underscore tells Helm that this is not a regular Yaml file
2. The template syntax is as follows  
`
{{ define "template-name" }}
vaild Yaml block
{{ end }}
`
3. To embed a template into your code you can use template or include  
- Template syntax is `{{ template "template-name" tree-start }}` tree start can affect how you specify the variables coming from the values.yaml  
for example `{{ template "template-name" .Values }}` will make you no longer need to put .Values infront of every variable.  
if it is just a dot like this `{{ template "template-name" . }}` then this will have no effect on the values
> **Two problems that we need to solve are** that the above code will leave an empty line after the go substitution happen, this happens everytime we have a substitution code having it is own line of code.  
> **The solution** is to use - (minus sign) directive `{{- template "template-name" .Values }}`  
  
> **The other problem is** that template will have the indentation of the yaml block starting from the start of the line and that will break the code.  
> **The solution** is to use the function **indent** in a pipeline but sadly template doesn't support that, and that's why **include** is needed  
- Include syntax will be `{{ include "template-name" tree-start | indent number-of-spaces }}`
