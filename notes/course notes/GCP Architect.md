TOTP (Time-based One-Time Password)
- the 6-digit code created in authenticator (it has other use cases)
- algorithm:
 - shared secret between server and client (for a particular identity), often shared via QR Code
 - time window is divided into a fix interval (typically 30s)
 - hash computed using secret key and current time window
 - 6-8 digit code is extracted from hash
 - both client and server generate the same code


Identity vs Access Token
- Identity:
  - signed, longer, 
  - bearer tokens
  - generate: `gcloud auth print-identity-token | pbcopy`
  - read identity token: 
    ```bash
    # method 1
    $ vi identity-token
    $ cat identity-token | step crypto jwt inspect --insecure
    
    # method 2
    $ gcloud auth print-identity-token | step crypto jwt inspect --insecure

    # extract date from int, ("exp": 1767793073)
    $ date -r 1767793073
    Wed Jan  7 08:37:53 EST 2026
    ```
- Access token
  - grants to a client very specific access of a resource
  - examples: read user messages, update user status
  - generate: `gcloud auth print-access-token | pbcopy`

source: https://auth0.com/blog/id-token-access-token-what-is-the-difference/

WIF - Workload Identity Federation

[Examples for Authenticating to Google Cloud from GitHub Actions
](https://github.com/google-github-actions/auth/blob/main/docs/EXAMPLES.md)

**Principals**
- an entity that can be granted access to a resource
- represent the 'who' or 'what' that is requesting access
- types:
  - user accounts
  - service accounts
  - groups
  - domains
  - special entities:
    - allUsers
    - allAuthenticatedUsers

**Identifiers**
- unique strings that specific/referenence gcp resources, principals or entities

**PrincipalSet**
- a set of principals
- example: all service accounts in a project
  - identifier: `principalSet://cloudresourcemanager.googleapis.com/projects/123456789012/type/ServiceAccount`
- more examples: https://cloud.google.com/iam/docs/principal-identifiers


**Principal vs Identity**

In computer security:
- A principal is any entity (user, service, device, etc.) that can be granted access to resources.
- An identity is the unique information or credentials that distinguish and authenticate a principal.

In simple terms:
- The principal is "who" wants access.
- The identity is "how you know who they are"—for example, a username, email address, certificate, or token.

Example:
- Principal: Alice (the user)
- Identity: alice@example.com (her email address used to log in)

Identity is what allows the system to recognize and verify the principal.


(GCP) Cloud Artitect
https://www.skills.google/paths/12
test user
unlocking.delegator@gmail.com / XSh^5m%twSz8nC

**Cloud Identity**
- allows organization to manage the access of users
- if someone leaves, an org can use CI to remove them

**IaaS**
Compute Engine
VPCs

**PaaS**
Cloud Marketplace - LAMP Stack, etc


### Cloud Computing
Definition (my order):
- cloud provider has a pool of computing resources made available to customers
- customers can request and consume those resources on-demand via self-service
- customers get access to those resources from anywhere over internet
- resources are elastic and flexible
- customer only pay for what they use, reserve as they go

### IaaS PaaS
- IaaS - individual infra resources are reserved (network, compute, storage)
- PaaS - platform overall is reserved (eg lamp stack), application is dropped into platform and all resources are available to him
    - marketplace

### Google Cloud Network
- gcp infra available on all 6 contentents and austrailia

- Regions - different locations, bringing resources closes to customers
- (Availability) Zones (~AWS AZs) - redundant areas within a region, if one zone goes down, traffic diverted to other region, if configured


### resources hierarchy
- organization
- folder
- (subfolders)
- projects
- resources

- deny trumps allow
- allow and deny policies are inherited and flow down to lower levels of hierarchy

### IAM
**Roles**
- all permissions are managed via roles
- types:
  - basic (viewer, editor, owner, billing admin (can control billing, but only view resources))
  - predefined (Cloud Run Admin, Cloud SQL Studio User)
  - custom (create a role, copy existing role (optional), add permissions)

**Service Accounts**
- a way to grant permissions to an entity/resources that isn't tied to a person
- example: give a VM access to write to a cloud-storage bucket it uses to convert files from one format to another. nothing else should have access because it contains customer data
  - can you just give the app running on this VM the access? prevent someone SSHing into the VM, or a virus, from accessing?


### Compute Engine 

**Virtual Private Clouds (VPCs)**
- a network within a public cloud infrastructure, defined by a user, that gives security and data isolation by using network segmentation, firewall rules to control what can and cannot access each component on the network
- there's a default vpc
- vpc subnets can be created in any region of gcp and can span zones within a region, so resources in different zones can share the same network


**Billing**
- sustained use discount
- if running for 25% of the month, sustained-use discount added automatically
- CE also offers committed-use discounts (57% for 1- to 3-year commitments)
- Preemptible or Spot VMs to run low-priority batch jobs
  - requires a job that can be terminated and/or restarted suddenly
  - Preemptible VMs can only be run for max 24 hours
  - Spot VMs - no max

- Scaling out (incr number of VMs) vs up (incr the size of the VMs)
- Max # of CPUs constrained by machine family, user's quota, zone-dependent
https://cloud.google.com/compute/docs/machine-types


https://cloud.google.com/run/docs


### Load Balancers
- a way to distribute traffice over multiple instances of an application in order to reduce the risk that the application experiences performance issues
- a fully-distributed, software-defined, managed service
- load balancers run in VMs that you don't manage, so you don't have to worry about scaling the load balance VMs themselves
- you can put cloud load-balancing front of all your traffic:
  - http, https
  - tcp, ssl
  - udp

### 

### 

### 

