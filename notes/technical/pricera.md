## Background


  -H 'Api-Class-Type: GR' \
  -H 'Api-Class-Unit-Code: SE' \
  -H 'Api-Class-Unit-Type: RU' \


### Running Pricera

## BackEnd

### Initial SetUp
```bash
# set project in gcp cli
gcloud config set project PROJECT_ID
# example
gcloud config set project ingka-pricing-pops-dev

# authenticate your code & google sdk's
gcloud auth login
gcloud auth application-default login

# confirm your sessions are still active
gcloud auth application-default print-access-token && gcloud auth list
```

### Run
```bash
# from project root:
cd ~/repos/pricing-operations/pricera-backend/

# from BE project root
./mvnw clean install -DskipTests
./mvnw -f services/cra-api spring-boot:run -DskipTests

# open new terminal
./mvnw -f services/cra-services spring-boot:run -DskipTests

# run db proxy (open new terminal):
~/repos/pricing-operations/scripts\,config\,misc\ files/backend\ scripts/db-proxy-startup.sh 

# profile
# Use a profile (loads application-<profile>.yml)
./mvnw spring-boot:run -Dspring-boot.run.profiles=local

# run with debug logging
./mvnw --debug -f services/cra-api spring-boot:run -DskipTests 

# run to attach debugger?  - cra-api
./mvnw -f services/cra-api spring-boot:run -DskipTests -Dspring-boot.run.jvmArguments="-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:5005"


# run to attach debugger - cra-services
./mvnw -f services/cra-services spring-boot:run -DskipTests -Dspring-boot.run.jvmArguments="-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:5006"
```

alternative approach to debugging
1. create run/debug configuration
2. in services panel > [new config (eg cra-api)] > Debug

### Run Unit Tests
```bash
./mvnw clean install -DskipTests

# cra-api
./mvnw -f services/cra-api test
# cra-services
./mvnw -f services/cra-services test

# other 2 repos
./mvnw -f services/external-subscriber test # <- *does not* need VPN 
#mvn -f services/support-api test # no tests

# run a specific unit test 
./mvnw test -pl services/cra-api -Dtest=PresetColumnsServiceTest
# code coverage report will be generated
# to find, run from backend project root run:
find . | grep index.html | less
# search for package, eg columnpresets, copy path
# confirm that file has been created recently
ls ./services/cra-api/target/jacoco/reports/com.ikea.cra.api.columnpresets.service/index.html
# then load in browser, using Command-Shift-G /to/edit/file/path/

# generate test coverage for entire project - report in target/site/jacoco/index.html -- some tests are failing locally
./mvnw clean verify jacoco:report

```

### Run Integration Tests
```bash
# run integration tests
./mvnw clean verify

# run tests from last failure?
./mvnw clean verify -rf :cra-services # works, but does it save any time?

# run a suite (ie class) of integration tests
./mvnw -pl services/cra-api test -Dtest=PresetColumnsControllerIT -Dspring-boot.run.profiles=local.db

# run a specific integration test
./mvnw -pl services/cra-api test -Dtest=PresetColumnsControllerIT#getColumnPresets_withExistingUserAndKey_shouldReturn200WithResults -Dspring-boot.run.profiles=local.db
```
### Logging/Tracing
add `--debug` flag
```bash
./mvnw --debug -f services/cra-api spring-boot:run -DskipTests


log.info("from columnpreset endpoint, request: [{}]", request);

columnPresetRepository.findAll().forEach(columnPreset -> {log.info(columnPreset.toString());});
```

------------------------------------------------------------------
## FrontEnd

launch config
  from e2e tests:
    pnpm --prefix pricera-frontend dev
  to run with verbose logging:
    LOG_LEVEL=debug DEBUG=* pnpm --prefix pricera-frontend dev


  pnpm dev maps to "pnpm db:generate && tsx --watch src/index.ts" in api/src/package.json's 

  launch: db:generate

  api/src/config.ts

  packages/internal/lib/
    library components
    optimizely, internal reused components
    

### SetUp
```bash
# 1. cloned FE repo
# 2. open in intellij
# 3. in terminal:
cd /Users/benjamin.schilke/repos/pricing-operations/pricera-frontend
# --- after initial setup ---
pnpm install
pnpm dev
# ✔ Path to orchestrator app: /Users/benjamin.schilke/repos/pricing-operations/pricera-spa-orchestrator
# 8. choose micro frontends -- max 16
# 9. open in browser localhost:8081
```

#### other FE commands
```bash
# more FE commands
pnpm build          # Build all apps (took 3.5 minutes)
pnpm test           # Run tests - not working - error msg w/out much detail
pnpm run test:workspace # worked for Jonathan
pnpm test:coverage  # Run tests with coverage
pnpm lint           # Lint all packages
pnpm lint:fix       # Auto-fix linting issues
pnpm format:fix     # Auto-fix formatting
```

#### running in 'prod' mode
`pnpm build:prod`


------------------------------------------------------------------
## Running Containerized Database
```bash
# stop local postgresql, if running
brew services # list all services with status
brew services info postgresql@16 # check postgres' status
brew services stop postgresql@16

# build docker containers -> follow podman build and compose steps in e2e tests
# building containers | BE, Docker terminal
cd ~/repos/pricing-operations/pricera-backend
./mvnw clean install -DskipTests -DskipITs
podman buildx build --load --file ./db/Dockerfile -t pricing-db .
podman images # confirm images were built 

# to run just the postgres/db image
podman compose up -d db --force-recreate
podman ps # confirm container is runng

# to run cra-api using local db (from component's readme):
mvn spring-boot:run  -Dspring.profiles.active=development,local-db
# to run cra-services using local db (from component's readme):
CLOUD_SQL_PROXY_HOST=localhost:5432 mvn spring-boot:run

# what about cra-services?

# running flyway migrations


# get bash shell for running container
podman exec -it pricera-backend-db-1 bash

# running sql from terminal
psql -U pricing -d postgres -c 'select * from pricing.service_pricing'
psql -U pricing -d postgres -c 'SELECT table_name, * FROM information_schema.tables'
```


# query containers 
podman containers ls
podman ps

podman container list
# use container id 
podman inspect <container id> | less # search for Network > IPAddress

**configuring DBeaver**
127.0.0.1:5432
database:postgresql
username/password:pricera/pricera

------------------------------------------------------------------
### E2E Tests 

**e2e tests - set up**  
```bash
# colima start --network-address
# # or 
# colima status
# export TESTCONTAINERS_DOCKER_SOCKET_OVERRIDE=/var/run/docker.sock
# export DOCKER_HOST="unix://${HOME}/.colima/default/docker.sock"
```
---------
podman, colima and docker have all been installed
colima is required because
  1. docker is difficult to run on mac (you really need a VM, similar to how it runs on windows) 
  2. if i don't have colima running, i can (can't?) run `docker buildx build`
i am using podman as well: podman creates a VM?

update:
- just using podman now
- for the most part podman can replace docker on the command line
---------

```bash
# check if podman is running
podman machine info | grep machinestate

# confirm images exist 
podman images

# after installing podman via brew, ran below:
# podman machine init
# podman machine start

# installed helper - only needed once
# sudo /usr/local/Cellar/podman/5.8.0/bin/podman-mac-helper install
# podman machine stop; podman machine start

# set up env vars as recommended with integration test instructions here:
# https://github.com/ingka-group-digital/pricera-backend/tree/main/services/cra-api
# if you don't run these, containers get created in docker. do i need podman?
# export DOCKER_HOST=unix://$(podman machine inspect --format '{{.ConnectionInfo.PodmanSocket.Path}}')
# export TESTCONTAINERS_DOCKER_SOCKET_OVERRIDE=/var/run/docker.sock

# get authorized
gcloud auth login
gcloud auth application-default login

# Check gcloud auth status
gcloud auth list

# Test authentication by making an API call
gcloud projects list

# Check application-default credentials
gcloud auth application-default print-access-token

# pull latest from main and merge, or
git pull origin main --rebase

# make sure you're running the same code as what's in github
git pull origin {feature branch}

# building containers | BE, Docker terminal
cd ~/repos/pricing-operations/pricera-backend
./mvnw clean install -DskipTests -DskipITs
podman buildx build --load --file ./db/Dockerfile -t pricing-db .
podman buildx build --build-arg ARTIFACTORY_USR=$ARTIFACTORY_USR --build-arg ARTIFACTORY_PWD=$ARTIFACTORY_PWD --load --file services/cra-api/Dockerfile -t cra-api .
podman buildx build --build-arg ARTIFACTORY_USR=$ARTIFACTORY_USR --build-arg ARTIFACTORY_PWD=$ARTIFACTORY_PWD --load --file services/cra-services/Dockerfile -t cra-services .

# confirm images were built 
podman images
podman containers ls
podman ps

# front end | FE-Orch terminal, FE 
#cd ~/repos/pricing-operations/ # FE-Orch terminal
#pnpm --prefix pricera-spa-orchestrator start # FE-Orch terminal
cd ~/repos/pricing-operations/pricera-frontend # FE terminal
pnpm install # FE terminal
pnpm dev

# cra-ui is typically not needed, getting phased out
# cd ~/repos/pricing-operations/cra-ui 
# pnpm start # legacy
# docker | BE, Docker terminal
cd ~/repos/pricing-operations/pricera-backend
ls compose.yml # confirm compose file is there
podman compose up --force-recreate
# back to front end | e2e terminal
cd ~/repos/pricing-operations/pricera-frontend # e2e terminal
PRICERA_DB_PORT=5432 pnpm test:e2e # http://localhost:8081/
```

```bash
# overwrite these env variables based on 
export DOCKER_HOST=unix://$(podman machine inspect --format '{{.ConnectionInfo.PodmanSocket.Path}}')
export TESTCONTAINERS_DOCKER_SOCKET_OVERRIDE=/var/run/docker.sock

[see instructions here](https://github.com/ingka-group-digital/pricera-backend/tree/main/services/cra-api)

```

view video of a test run from :
  - go to tests in github
  - search for artifact zip file
  - download and expand zip
  - videos in e2e/cypress/videos



### PRs

- branch names: **POPS-xxxx**
- commit descriptions: 
  **chore/chore(deps)/feat/feat(iam)/perf/refactor(ci): {description of change}**
-  & PR names:
  **chore/chore(deps)/feat/feat(iam)/perf/refactor(ci): {description of change} {jira ticket id}**


### Logging

FE 
    console.warn('getCurrentUserData: data', null);
    -> dev tools
    console.log(`pgConnection: ${JSON.stringify(pgConnection,null,2)}`);


### Misc
**Optimizely** - feature flags
- The code in `packages/internal/lib/optimizely/index.ts` sets up Optimizely for React using the official SDK.
  - It configures the Optimizely instance based on the current environment (dev, test, prod) by matching the hostname.
  - The Optimizely SDK key and datafile URL are selected per environment.
  - `OptimizelyProvider` and `useDecision` are exported from here.
  - The exported `OptimizelyProvider` is used to wrap React components, enabling feature flagging and experimentation.
  - The `useDecision` hook is exported for components to check feature flags or experiment variations at runtime.


- `@pricera/internal/lib/optimizely` is mapped to packages/internal/lib/optimizely:
```jsx
// apps/core/src/App.tsx
import { optimizely, OptimizelyProvider } from '@pricera/internal/lib/optimizely';

export const App = () => {
  return (
    <OptimizelyProvider optimizely={optimizely}>
      <AuthenticationProvider>
        <QueryClientProvider client={queryClient}>
          <SidebarMenuProvider>
            <ItemSearchProvider>
            <!- ...>
```


### Calling APIs
commercial activity: /api/ui/commercial-activity?fromDate=2024-01-01&toDate=2024-01-31


### Functional API Testing Tools Research
- Option #1: Newman (Postman CLI)
  - Project: https://github.com/postmanlabs/newman
    - instructions: https://learning.postman.com/docs/collections/using-newman-cli/installing-running-newman
      - installed with `npm -g install newman` (available in brew as well)
  - What: CLI runner for Postman collections — good for running Postman test suites in CI, easy to execute exported collections + environment files.
  - Typical use: run exported collection(s) and environments, integrate with reports (JUnit, HTML).
  - Example GitHub Actions step:
```yaml
- name: Run Postman collection with newman
  uses: actions/setup-node@v4
- run: |
    npm install -g newman
    newman run ./collections/my-collection.json -e ./environments/ci.json --reporters cli,junit --reporter-junit-export results/newman-results.xml
```
  - get a call to bearer token working
  - how do i back out this merge?
    - hard reset -- I haven't pushed the changes up yet.



### Issues
**cra-api shuts down immediately**
- it looks like it's due to other java instances being open, using the same port?
- fix
  - stop all java jobs
  - close all intellij and any other java application
  - open activity monitor and close any remaining java processes
    - when you're done there should be 0 running java processes
  - restart intellij

**`Error: Failed to fetch for user id`**
```
message: 'An error occurred while processing request.', 
error: 'Error: Failed to fetch for user id: "ad6ce09a-87f4-4af6-9ea3-397589de719f"',
```
- make sure you're using port 5435 (port used to connect to dev db)
   api/src/config.ts, line 7
   ```
  port: Number(process.env.SQL_INSTANCE_PORT) || 5435,
  ```
- make sure proxy cloud_sql_proxy is running
- go to http://localhost:8081/login 


**Immediate Shutdown after Startup (cra-api)**
```
com.zaxxer.hikari.HikariDataSource       : HikariPool-7 - Shutdown initiated...
com.zaxxer.hikari.HikariDataSource       : HikariPool-7 - Shutdown completed.
o.apache.catalina.core.StandardService   : Stopping service [Tomcat]
```
* can happen when the component is already running. check services window, another terminal window

**Global Find Not Working in IntelliJ**
Invalidate Cache & Restart doesn't work
Following these instructions: https://youtrack.jetbrains.com/projects/IJPL/issues/IJPL-218976/IDEA-unable-to-find-list-files-after-a-while
Search for instructioms that start with 'Re-create project configuration settings from scratch'
(I didn't do final 2 steps under 'Manually remove the following folders using file explorer')

Another valueable resource: folders used by IntelliJ: https://www.jetbrains.com/help/idea/directories-used-by-the-ide-to-store-settings-caches-plugins-and-logs.html


