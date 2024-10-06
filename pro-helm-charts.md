# Professional helm charts patterns

### Professional helm charts often have common characteristics between them
1. Appending the deployment or release name as a prefix to the resources created  
To do that just add the pre-defined label {{ .Release.Name }} to the resource name.
- This can enable us to have multiple releases in the same namespace without having any issue and removes some of the ambigouty that you might have latter on about which resource belongs to which Helm chart release
> Beware that if the service names are embedded in the application code itself then appending the release name will break the code and the application won't work. so, keep that in mind