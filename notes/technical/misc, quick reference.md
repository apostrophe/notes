

**DB/PostgreSQL**
command to start local db
`/usr/local/Cellar/postgresql\@16/16.6/bin/psql pilot-dev`

**open cloud-sql-proxy**
`~/Documents/installations/cloud-sql-proxy ingka-ushub-pupapp-prod:us-east4:pilot-prod --port 3303 --auto-iam-authn`

DBeaver SQL files: /Users/benjamin.schilke/Library/DBeaverData/workspace6/General/Scripts/Script-17.sql

file filter for searches in JS/TS Projects:
node_modules, *.json, *.scss, *.html, *.js, *.yaml

Regex:

***Terraform***
*cd into /dev or /prod folder*
terraform init
terraform plan -no-color -lock=false
terraform apply -auto-approve -input=false -lock=false

**Logs Explorer Queries**
resource.type = "cloud_run_revision"
resource.labels.service_name = "pup-app-fe"
resource.labels.location = "us-east4"
timestamp>="2025-10-10T16:23:00Z" AND timestamp<="2025-10-11T16:25:00Z"

Example Queries: https://cloud.google.com/logging/docs/view/query-library


ssh bschilke@192.168.0.151
