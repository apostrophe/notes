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

### IAM
**Roles**
- all permissions are managed via roles
- types:
  - basic (viewer, editor, owner, billing admin (can control billing, but only view resources))
  - predefined (Cloud Run Admin, Cloud SQL Studio User)
  - custom (create a role )

**Service Accounts**
- a way to grant permissions to an entity/resources that isn't tied to a person
- example: give a VM access to write to a cloud-storage bucket it uses to convert files from one format to another. nothing else should have access because it contains customer data
  - can you just give the app running on this VM the access? prevent someone SSHing into the VM, or a virus, from accessing?

**Cloud Identity**
- allows organization to manage the access of users
- if someone leaves, an org can use CI to remove them

**IaaS**
Compute Engine
VPCs

**PaaS**
Cloud Marketplace - LAMP Stack, etc

