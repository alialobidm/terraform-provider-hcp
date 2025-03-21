---
page_title: "Resource hcp_vault_secrets_integration"
subcategory: "HCP Vault Secrets"
description: |-
  The Vault Secrets integration resource manages an integration.
---

# hcp_vault_secrets_integration (Resource)

The Vault Secrets integration resource manages an integration.

## Example Usage

```terraform
// AWS
resource "hcp_vault_secrets_integration" "example_aws_federated_identity" {
  name          = "my-aws-1"
  capabilities  = ["DYNAMIC", "ROTATION"]
  provider_type = "aws"
  aws_federated_workload_identity = {
    audience = "<audience>>"
    role_arn = "<role-arn>"
  }
}

resource "hcp_vault_secrets_integration" "example_aws_access_keys" {
  name          = "my-aws-2"
  capabilities  = ["DYNAMIC", "ROTATION"]
  provider_type = "aws"
  aws_access_keys = {
    access_key_id     = "<access-key-id>"
    secret_access_key = "<secret-access-key>"
  }
}

// Confluent
resource "hcp_vault_secrets_integration" "example_confluent" {
  name          = "my-confluent-1"
  capabilities  = ["ROTATION"]
  provider_type = "confluent"
  confluent_static_credentials = {
    cloud_api_key_id = "<cloud-api-key-id>"
    cloud_api_secret = "<cloud-api-secret>"
  }
}

// GCP
resource "hcp_vault_secrets_integration" "example_gcp_json_service_account_key" {
  name          = "my-gcp-1"
  capabilities  = ["DYNAMIC", "ROTATION"]
  provider_type = "gcp"
  gcp_service_account_key = {
    credentials = file("${path.module}/my-service-account-key.json")
  }
}

resource "hcp_vault_secrets_integration" "example_gcp_base64_service_account_key" {
  name          = "my-gcp-2"
  capabilities  = ["DYNAMIC", "ROTATION"]
  provider_type = "gcp"
  gcp_service_account_key = {
    credentials = filebase64("${path.module}/my-service-account-key.json")
  }
}

resource "hcp_vault_secrets_integration" "example_gcp_federated_identity" {
  name          = "my-gcp-3"
  capabilities  = ["DYNAMIC", "ROTATION"]
  provider_type = "gcp"
  gcp_federated_workload_identity = {
    service_account_email = "<service-account-email>"
    audience              = "<audience>"
  }
}

// MongoDB-Atlas
resource "hcp_vault_secrets_integration" "example_mongodb_atlas" {
  name          = "my-mongodb-1"
  capabilities  = ["ROTATION"]
  provider_type = "mongodb-atlas"
  mongodb_atlas_static_credentials = {
    api_public_key  = "<api-public-key>"
    api_private_key = "<api-private-key>"
  }
}

// Twilio
resource "hcp_vault_secrets_integration" "example_twilio" {
  name          = "my-twilio-1"
  capabilities  = ["ROTATION"]
  provider_type = "twilio"
  twilio_static_credentials = {
    account_sid    = "<account-sid>"
    api_key_secret = "<api-key-secret>"
    api_key_sid    = "<api-key-sid>"
  }
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `capabilities` (Set of String) Capabilities enabled for the integration. See the Vault Secrets documentation for the list of supported capabilities per provider.
- `name` (String) The Vault Secrets integration name.
- `provider_type` (String) The provider or 3rd party platform the integration is for.

### Optional

- `aws_access_keys` (Attributes) AWS IAM key pair used to authenticate against the target AWS account. Cannot be used with `federated_workload_identity`. (see [below for nested schema](#nestedatt--aws_access_keys))
- `aws_federated_workload_identity` (Attributes) (Recommended) Federated identity configuration to authenticate against the target AWS account. Cannot be used with `access_keys`. (see [below for nested schema](#nestedatt--aws_federated_workload_identity))
- `azure_client_secret` (Attributes) Azure client secret used to authenticate against the target Azure application. Cannot be used with `federated_workload_identity`. (see [below for nested schema](#nestedatt--azure_client_secret))
- `azure_federated_workload_identity` (Attributes) (Recommended) Federated identity configuration to authenticate against the target Azure application. Cannot be used with `client_secret`. (see [below for nested schema](#nestedatt--azure_federated_workload_identity))
- `confluent_static_credentials` (Attributes) Confluent API key used to authenticate for cloud apis. (see [below for nested schema](#nestedatt--confluent_static_credentials))
- `gcp_federated_workload_identity` (Attributes) (Recommended) Federated identity configuration to authenticate against the target GCP project. Cannot be used with `service_account_key`. (see [below for nested schema](#nestedatt--gcp_federated_workload_identity))
- `gcp_service_account_key` (Attributes) GCP service account key used to authenticate against the target GCP project. Cannot be used with `federated_workload_identity`. (see [below for nested schema](#nestedatt--gcp_service_account_key))
- `gitlab_access` (Attributes) GitLab access token used to authenticate against the target GitLab account. (see [below for nested schema](#nestedatt--gitlab_access))
- `mongodb_atlas_static_credentials` (Attributes) MongoDB Atlas API key used to authenticate against the target project. (see [below for nested schema](#nestedatt--mongodb_atlas_static_credentials))
- `project_id` (String) HCP project ID that owns the HCP Vault Secrets integration. Inferred from the provider configuration if omitted.
- `twilio_static_credentials` (Attributes) Twilio API key parts used to authenticate against the target Twilio account. (see [below for nested schema](#nestedatt--twilio_static_credentials))

### Read-Only

- `organization_id` (String) HCP organization ID that owns the HCP Vault Secrets integration.
- `resource_id` (String) Resource ID used to uniquely identify the integration instance on the HCP platform.
- `resource_name` (String) Resource name used to uniquely identify the integration instance on the HCP platform.

<a id="nestedatt--aws_access_keys"></a>
### Nested Schema for `aws_access_keys`

Required:

- `access_key_id` (String) Key ID used with the secret key to authenticate against the target AWS account.
- `secret_access_key` (String, Sensitive) Secret key used with the key ID to authenticate against the target AWS account.


<a id="nestedatt--aws_federated_workload_identity"></a>
### Nested Schema for `aws_federated_workload_identity`

Required:

- `audience` (String) Audience configured on the AWS IAM identity provider to federate access with HCP.
- `role_arn` (String) AWS IAM role ARN the integration will assume to carry operations for the appropriate capabilities.


<a id="nestedatt--azure_client_secret"></a>
### Nested Schema for `azure_client_secret`

Required:

- `client_id` (String) Azure client ID corresponding to the Azure application.
- `client_secret` (String) Secret value corresponding to the Azure client secret.
- `tenant_id` (String) Azure tenant ID corresponding to the Azure application.


<a id="nestedatt--azure_federated_workload_identity"></a>
### Nested Schema for `azure_federated_workload_identity`

Required:

- `audience` (String) Audience configured on the Azure federated identity credentials to federate access with HCP.
- `client_id` (String) Azure client ID corresponding to the Azure application.
- `tenant_id` (String) Azure tenant ID corresponding to the Azure application.


<a id="nestedatt--confluent_static_credentials"></a>
### Nested Schema for `confluent_static_credentials`

Required:

- `cloud_api_key_id` (String) Public key used alongside the private key to authenticate for cloud apis.
- `cloud_api_secret` (String, Sensitive) Private key used alongside the public key to authenticate for cloud apis.


<a id="nestedatt--gcp_federated_workload_identity"></a>
### Nested Schema for `gcp_federated_workload_identity`

Required:

- `audience` (String) Audience configured on the GCP identity provider to federate access with HCP.
- `service_account_email` (String) GCP service account email that HVS will impersonate to carry operations for the appropriate capabilities.


<a id="nestedatt--gcp_service_account_key"></a>
### Nested Schema for `gcp_service_account_key`

Required:

- `credentials` (String) JSON or base64 encoded service account key received from GCP.

Read-Only:

- `client_email` (String) Service account email corresponding to the service account key.
- `project_id` (String) GCP project ID corresponding to the service account key.


<a id="nestedatt--gitlab_access"></a>
### Nested Schema for `gitlab_access`

Required:

- `token` (String, Sensitive) Access token used to authenticate against the target GitLab account. This token must have privilege to create CI/CD variables.


<a id="nestedatt--mongodb_atlas_static_credentials"></a>
### Nested Schema for `mongodb_atlas_static_credentials`

Required:

- `api_private_key` (String, Sensitive) Private key used alongside the public key to authenticate against the target project.
- `api_public_key` (String) Public key used alongside the private key to authenticate against the target project.


<a id="nestedatt--twilio_static_credentials"></a>
### Nested Schema for `twilio_static_credentials`

Required:

- `account_sid` (String) Account SID for the target Twilio account.
- `api_key_secret` (String, Sensitive) Api key secret used with the api key SID to authenticate against the target Twilio account.
- `api_key_sid` (String) Api key SID to authenticate against the target Twilio account.

## Import

Import is supported using the following syntax:

```shell
# Vault Secrets Integration can be imported by specifying the name of the integration
# Note that since sensitive information are never returned on the Vault Secrets API,
# the next plan or apply will show a diff for sensitive fields.
terraform import hcp_vault_secrets_integration.example my-integration-name
```
