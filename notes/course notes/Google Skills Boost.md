
### Useful

- Asset Inventory - a way to view all resources in a project, no gcloud equivalent
  - IAM & Admin > Asset Inventory
  - gcloud option: untested gcloud script someone wrote: https://github.com/javier/gcloud_inventory/blob/master/gcloud_inventory.sh
    - to enhance: 
      - fix errors
      0 find a way to enable or skip uneabled APIs
- Support: https://console.cloud.google.com/support
  - Level of support (Basic, Premiu, Enterprise, Gold, Platinum)
    - incidents and status of incidents
- Access Transparency
  - logging of any google employee access to cloud customer data
  - must be enabled at org level
- Access Approval
  - require permission before google employee can access customer data



### Developing Applications w/Google Cloud: Foundations
https://www.skills.google/course_templates/874

- Cloud development allows for (full) scalability[1], high availability, reduced costs, global access(?)

Best Practices
- allow for **scalability, high availability, security, 'global access'** (these are minimal standarsd, 'table stakes' (poker term?))
  - **high availability and scalability** your application should be able to handle high traffic volumes reliably
- **data isolation to a specific region** for security or compliance reasons
- store code in a **code repository**
- **use dependency manager** to manage dependencies
  - list dependencies and versions in the project
  - lean on dep mgr (maven, npm, nuget) to pull down those dependencies, manage versions, etc
- store **configuration settings** outside of your code as environment variables
  - allows environments the code is running in to dictate configuration
- scope of applications should be considered as features are added
  - applications should be as single-minded in purpose as possible
  - one benefit is being able to scale
  - example:
    - currently pup app backend is an interface for order data between our data store and the FE
    - if we started to support, for example, diverting orders to a customer's orders and we had to build an API to support this, there'd be a good argument for branching this off into another service.
      - you'd be able to scale this differently than the original (for example, if only a few stores supported this feature, and the pup app spread to 50 PUPs, if these 2 services are separate microservices, you could scale the BE that supports orders wihtout having to also scale the order-diversion service) 
  - consider the costs and benefits of refactoring a monolithic app to two or more microservices, because the effort to break them out, test and fix bugs can be significant, but the long-term benefits can also be significant
- keep operations in the **user thread** to a minimum
- perform backend operations **asynchronously**
- use **event-driven processing** whenever possible
  - example async process: processing uploaded images
    - upload images to bucket storage
    - create an image-processing cloud-run function that is triggered when an image is added to bucket storage
- **tightly-coupled components can make an application less resilient to failures, spikes in traffic, and changes to services**
- event/message queues can be used to implement
    - loose coupling,
    - perform asynchronous processing, and
    - buffer requests if traffic spikes
    - examples:
      - loose coupling: 
      - perform asynchronous processing, and
      - buffer requests if traffic spikes

- accessing a commonly **shared state** can be a bottleneck


[1] You can have a very small, simple application and only the simplest, pay-as-you-go infrastructure required to support it (not a full server, network, etc an on-prem solution would require)




---------------------------------------------------------------------------
### Misc

```bash
# capture cloud run service url
SERVICE_URL=$(gcloud beta run services describe {'enter service name here'} --platform managed --region {'enter region here'} --format="value(status.url)")

# example
SERVICE_URL=$(gcloud beta run services describe pdf-converter --platform managed --region us-west1 --format="value(status.url)")
echo $SERVICE_URL
```

---------------------------------------------------------------------------
### Challenge-Lab Prep
https://www.skills.google/course_templates/649/labs/592585

Challenge Lab:
Click on icon for 'Activate Cloud Shell'


**Task 1 - Create firestore database**
- In GCP: search for Firebase service
- Standard Edition
- Firestore Native Mode
- Security: Open
- Choose region

**Task 2 - Populate Database**
**Task 3 - Create a REST API**
Given that you already have a Dockerfile:
```Dockerfile
FROM node:12-slim
WORKDIR /usr/src/app
COPY package.json package*.json ./
RUN npm install --only=production
COPY . .
CMD [ "npm", "start" ]
```
... you can run the below commands,


***get the region and populate below!!***

```bash
PROJECT_ID=$(gcloud config get-value project)
gcloud builds submit --region=us-west2 --tag us-west2-docker.pkg.dev/PROJECT_ID/netflix-dataset-service/rest-api:0.1
```


... then run

```bash
gcloud run deploy netflix-dataset-service --source . --allow-unauthenticated
```

**Task 4 - Firestore Access**
**Task 5 - Deploy the Staging FrontEnd**
**Task 6 - Deploy the Production FrontEnd**


```bash
# authenticated post request:
curl -X POST -H "Authorization: Bearer $(gcloud auth print-identity-token)" $SERVICE_URL


# extract project number to an env variable
export PROJECT_NUMBER=$(gcloud projects describe $(gcloud config get-value project) --format="value(projectNumber)")
```


```bash
git clone https://github.com/rosera/pet-theory.git
cd pet-theory/lab03

# add 'start' line to package.json
"scripts": {
    "start": "node index.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },


# Dockerfile contents:
FROM node:20
WORKDIR /usr/src/app
COPY package.json package*.json ./
RUN npm install --only=production
COPY . .
CMD [ "npm", "start" ]

# Running `gcloud builds submit` in a folder with a Dockerfile
# pushes the image to gcr.io? Do this for updates as well.
gcloud builds submit \
  --tag gcr.io/$GOOGLE_CLOUD_PROJECT/pdf-converter

# it's odd that gcr.io is the name of the repository created

# Deploy this image in grc to Cloud Run
gcloud run deploy pdf-converter \
  --image gcr.io/$GOOGLE_CLOUD_PROJECT/pdf-converter \
  --platform managed \
  --region Region \
  --no-allow-unauthenticated \
  --max-instances=1
  --set-env-vars PDF_BUCKET=$GOOGLE_CLOUD_PROJECT-processed
```

**Related Articles**  
[Build And Push Docker Image To Artifact Registry](https://docs.cloud.google.com/build/docs/build-push-docker-image) 


**Create a docker file and call `gcloud builds submit`**  

Create a folder for your project:  
```bash
mkdir quickstart-docker
cd quickstart-docker
```

Create a simple script, name it quickstart.sh:
```bash
#!/bin/sh
echo "Hello, world! The time is $(date)."
```

Make it executable:  
`chmod +x quickstart.sh`

Create a simple Dockerfile:
```dockerfile
FROM alpine
COPY quickstart.sh /
CMD ["/quickstart.sh"]
```

Create a GCP artifact repository and then query the list of repositories to confirm it was created:
```bash
gcloud artifacts repositories create quickstart-docker-repo --repository-format=docker \
    --location=us-west2 --description="Docker repository"
gcloud artifacts repositories list
```

Store your project id into an env variable, and then call `gcloud builds submit`, which will look for source code and will build the docker image when it finds the Dockerfile:
```bash
PROJECT_ID=$(gcloud config get-value project)
gcloud builds submit --region=us-west2 --tag us-west2-docker.pkg.dev/PROJECT_ID/quickstart-docker-repo/quickstart-image:tag1
```

after the build you'll see something like this:
```bash
DONE
------------------------------------------------------------------------------------------------------------------------------------
ID                                    CREATE_TIME                DURATION  SOURCE   IMAGES     STATUS
545cb89c-f7a4-4652-8f63-579ac974be2e  2020-11-05T18:16:04+00:00  16S       gs://gcb-docs-project_cloudbuild/source/1604600163.528729-b70741b0f2d0449d8635aa22893258fe.tgz  us-west2-docker.pkg.dev/gcb-docs-project/quickstart-docker-repo/quickstart-image:tag1  SUCCESS
```


**Create a docker file and call `gcloud builds submit` with cloudbuild.yaml**

Create `cloudbuild.yaml`
```bash
steps:
- name: 'gcr.io/cloud-builders/docker'
  script: |
    docker build -t us-west2-docker.pkg.dev/$PROJECT_ID/quickstart-docker-repo/quickstart-image:tag1 .
  automapSubstitutions: true
images:
- 'us-west2-docker.pkg.dev/$PROJECT_ID/quickstart-docker-repo/quickstart-image:tag1'
```

call cloud build:
```bash
gcloud builds submit --region=us-west2 --config cloudbuild.yaml
```

The results of the above can be seen by going to Cloud Build > Build History.
Then click on one of the builds and review Build Summary and Build Artifacts.

To clean up: go to the artifact repository, click on 'quickstart-docker-repo' and then click Delete.


```bash
```

```bash
```

```bash
```

```bash
```

```bash
```

-------- challenge lab history --------
```bash
PROJECT_ID=$(gcloud config get-value project)
echo $PROJECT_ID 


gcloud artifacts repositories create challenge-lab-repo --repository-format=docker --location=us-east1 --description="Docker repository"

gcloud builds submit --region=us-east1 --tag us-east1-docker.pkg.dev/$PROJECT_ID/challenge-lab-repo/rest-api:0.1
gcloud run deploy netflix-dataset-service --image us-east1-docker.pkg.dev/qwiklabs-gcp-01-53536273fe42/challenge-lab-repo/rest-api:0.1 --max 1

gcloud builds submit --region=us-east1 --tag us-east1-docker.pkg.dev/$PROJECT_ID/challenge-lab-repo/rest-api:0.2

gcloud run deploy netflix-dataset-service --image us-east1-docker.pkg.dev/qwiklabs-gcp-01-53536273fe42/challenge-lab-repo/rest-api:0.2 --max 1



# set default region
gcloud config set run/region us-east1
# check env var to default region
REGION=$(gcloud config get run/region)
echo $REGION
```