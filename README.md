# post-config-test
This Repo demonstrates a crude method to version control config files that are published to an API endpoint.

Pushed changes to `*.staging.config.json` or `*.prod.config.json` json files in `main` branch will trigger the appropriate workflow to run and publish changes to endpoints defined in action files for staging or prod based on path filters.

Using PR flow, configs can be made in the lower `dev` branch for review, and a PR and push to `main` would publish the changes.

NOTE: An alternate trigger strategy is to trigger off long lived branches that represent each environment. This works well when configs aren't different between environments.

## Getting Started
1. Create a folder with a name that matches a tenant name
1. Create a 1pass vault and set config with the chosen name
1. Create an item in the 1pass vault and match the name with the folder created in an earlier step
1. Set all tenant secrets within the single 1pass item by adding more password fields
1. Obtain the service account token to the vault and store it as a secret `OP_SERVICE_ACCOUNT_TOKEN`
1. Create a tokenized config file with a name that ends in either `.staging.config.json` or `.prod.config.json`

## Config
Separate triggers are maintained to allow discrete variables to be set that differ between environments that are being posted to.

| variable | description |
|---|---|
| `publish-url` | the endpoint to POST the config to |
| `vault-name` | the name of the 1password vault |

## Secrets
The following secrets are expected to be available to the workflow.

| secret | description |
|---|---|
| `OP_SERVICE_ACCOUNT_TOKEN` | credentials to a 1pass service account |
| `PUBLISH_BEARER_TOKEN` | the bearer token required for auth to the `publish-url` endpoint |

## Conventions and 1password
Successful lookup of secrets requires a convention to be followed.

1. Configs formatted as JSON and saved in folders at the root of this project i.e. configs are always 1-level deep.
1. An item exists in the vault that matches the folder name that the config resides in at the root level.
1. The vault name matches the variable set in `vault-name`
1. The config token is added to the `Load Secrets` step as an env variable in the workflow file.
1. The config files contain the variable using the following pattern `${TOKEN-NAME}`
1. This project currently assumes that a the same 1pass service account token is used for all vaults in scope

