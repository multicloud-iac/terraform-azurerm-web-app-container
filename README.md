# Terraform Module to create Azure Web App Containers

Create Web App for Containers (Azure App Service).

## Example Usage

```hcl
resource "azurerm_resource_group" "example" {
  name     = "example-resources"
  location = "centralus"
}

module "web_app_container" {
  # Example source URL points to Terraform Enterprise Private Module Registry

  source  = "app.terraform.io/multicloud/web-app-container/azurerm"
  version = "1.5.0"

  name = "hello-world"

  resource_group_name = "${azurerm_resource_group.example.name}"

  container_type = "docker"

  container_image = "robpco/palacearcade:latest"
}
```

## Required Inputs

| Name | Type | Description |
| --- | --- | --- |
| `name` | `string` | The name of the web app. |
| `resource_group_name` | `string` | The name of an existing resource group to use for the web app. |
| `container_image` | `string` | Container image name. Example: `robpco/palacearcade:latest`. |

## Optional Inputs

| Name | Type | Description |
| --- | --- | --- |
| `container_type` | `string` | Type of container. The options are: `docker`, `compose` and `kube`. Default: `docker`. |
| `container_config` | `string` | Configuration for the container. This should be YAML. |
| `port` | `string` | The value of the expected container port number. |
| `enable_storage` | `bool` | Mount an SMB share to the `/home/` directory. Default: `false`. |
| `start_time_limit` | `string` | Configure the amount of time (in seconds) the app service will wait before it restarts the container. Default: `230`. |
| `command` | `string` | A command to be run on the container. |
| `app_settings` | `map` | Set web app settings. These are avilable as environment variables at runtime. |
| `app_service_plan_id` | `string` | The ID of an existing app service plan to use for the web app. |
| `sku_tier` | `string` | The pricing tier of an app service plan to use for the web app. Default: `Standard`. |
| `sku_size` | `string` | The instance size of an app service plan to use for the web app. Default: `S1`. |
| `always_on` | `bool` | Either `true` to ensure the web app gets loaded all the time, or `false` to to unload after being idle. |
| `https_only` | `bool` | Redirect all traffic made to the web app using HTTP to HTTPS. Default: `true`. |
| `ftps_state` | `string` | Set the FTPS state value the web app. The options are: `AllAllowed`, `Disabled` and `FtpsOnly`. Default: `Disabled`. |
| `ip_restrictions` | `list` | Configure IP restrictions for the web app. |
| `custom_hostnames` | `list` | List of custom hostnames to use for the web app. |
| `docker_registry_username` | `string` | The container registry username. |
| `docker_registry_url` | `string` | The container registry url. Default: `https://index.docker.io` |
| `docker_registry_password` | `string` | The container registry password. |
| `tags` | `map` | A mapping of tags to assign to the web app. |
