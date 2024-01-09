# post-config-test
This Repo demonstrates a crude method to version control config files that are published to an API endpoint.

Pushed changes to `*.staging.config.json` or `*.prod.config.json` json files in `main` branch will trigger the appropriate workflow to run and publish changes to endpoints defined in action files for staging or prod based on path filters.

Using PR flow, configs can be made in the lower `dev` branch for review, and a PR and push to `main` would publish the changes.

Another trigger strategy is to trigger off long lived branches that represent each environment. This works well when configs aren't different between environments. 
