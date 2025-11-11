```bash
# list of projects
gcloud projects list format --help

# json format with filter
gcloud projects list --format="json" \
  --filter="labels.env=test AND labels.version=alpha"

gcloud auth application-default login

gcloud components update

# default region (in compute at least)
gcloud config list compute/region | less

# get the current project
gcloud info --format='value(config.project)'

# get all assets in json format
gcloud asset search-all-resources --format=json | less

# table format
gcloud asset search-all-resources --format="table(assetType, displayName, project, state)" | less

# output a single value
gcloud info --format='value(config.account)'

# all assets in table format
gcloud asset search-all-resources --format="table(assetType, displayName, project, state)" | less

# return a single value
gcloud info --format='value(config.account)'

```
more examples: https://docs.cloud.google.com/sdk/docs/scripting-gcloud