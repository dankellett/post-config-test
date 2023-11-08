# post-config-test
This Repo demonstrates a crude method to version control config files that are published to an API endpoint.

Pushed changes to json files in [`main`, `dev`] branches will trigger the workflows to run and publish changes to endpoints defined in action files for specific branches.

Using PR flow, configs can be made in the lower `dev` branch to be published to a lower environment and when ready, a PR and push to `main` would publish the changes to production.

If configs are different between environments, one might setup seperate files and use naming convention to trigger/filter the correct actions to run as an alternate strategy.
