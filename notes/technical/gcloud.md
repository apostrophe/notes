
### auth

```bash
# authenticate your code & google sdk's
gcloud auth login
gcloud auth application-default login

# Check gcloud auth status
gcloud auth list

# Test authentication by making an API call
gcloud projects list

# Check application-default credentials
gcloud auth application-default print-access-token
```


### general

```bash
# list of projects
gcloud projects list format --help

# json format with filter
gcloud projects list --format="json" \
  --filter="labels.env=test AND labels.version=alpha"

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