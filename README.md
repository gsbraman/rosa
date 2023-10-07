## Source Procedure
https://github.com/terraform-redhat/terraform-provider-rhcs/tree/main/examples/create_rosa_sts_cluster/classic_sts/cluster
https://docs.aws.amazon.com/ROSA/latest/userguide/getting-started-sts-auto.html


### Set Vars
Get Token From:
https://console.redhat.com/openshift/token
```
export TF_VAR_token=xxx
```
```
export TF_VAR_url=https://api.openshift.com
```
```
export TF_VAR_operator_role_prefix=xxx
```
```
export TF_VAR_account_role_prefix=xxx
```
```
export TF_VAR_cluster_name=xxx
```


### Optional Vars
```
export TF_VAR_openshift_version=<choose_openshift_version>
export TF_VAR_tags=...
```

### Deploy Cluster
```
terraform init
terraform plan -var-file="prod.tfvars"
terraform apply -var-file="prod.tfvars"
rosa logs install -c xxx --watch
```
```
rosa list versions
rosa list clusters
rosa logs install -c xxx --watch
rosa create admin --cluster=ocp-test
rosa delete admin --cluster=ocp-test
rosa describe cluster -c <CLUSTER_NAME>
rosa describe cluster -c <CLUSTER_NAME> | grep Console

```
### Delete Cluster
```
terraform destroy
terraform destroy -var-file="prod.tfvars" -auto-approve
```

#### Ignore Changes
https://developer.hashicorp.com/terraform/language/meta-arguments/lifecycle#ignore_changes

#### Dependencies
https://developer.hashicorp.com/terraform/tutorials/configuration-language/dependencies

Data sources thus inherently manage the dependencies for creating dynamic resources dependent on the existence of the data.
```
aws sts get-caller-identity --query "Account" --output text
```
```
terraform plan # No changes. Your infrastructure matches the configuration.
rosa list clusters
rosa list users --cluster=ocp-test
rosa create admin --cluster=ocp-test
```
### Cleanup
```
terraform destroy -var-file="prod.tfvars"
rosa logs uninstall -c xxx --watch
```