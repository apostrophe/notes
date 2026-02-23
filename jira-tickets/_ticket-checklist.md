## Ticket Workflow Checklist

Ticket: Sales Item API 

### Code
- [ ] update jira story status to IN PROGRESS
- [ ] review acceptance criteria
- [ ] pull latest from develop (or main)
- [ ] create a new branch
- [ ] talk to team about specifics if there’s any doubt
- [ ] add `/src` to `.prettierignore` to avoid formatting warnings
- [ ] make changes
    - [ ] commit often
- [ ] double-check acceptance criteria
- [ ] review changes with scrum team and/or engineering team

### Tests, Linting
- [ ] comment out `/src` in `.prettierignore` to allow for formatting warnings when running lint
- [ ] add unit tests
- [ ] run unit tests
- [ ] run lint
- [ ] `npm audit` (checks for security vulnerabilities)
    - [ ] if you have to fix, re-run tests
- [ ] confirm all changes are in git stage
- [ ] commit
- [ ] push to github

### Infra
- [ ] add to infra/terraform project?
    - [ ] dev
    - [ ] prod
- [ ] add manually in gcp?
    - [ ] dev
    - [ ] prod

### PR
- [ ] create PR
    - [ ] look over your changes again
    - [ ] confirms
        - [ ] no merge conflicts
        - [ ] jobs ran successfully
    - [ ] request review by someone
    - [ ] move jira story to review
    - [ ] **check dependabot alerts**
- [ ] merge PR
- [ ] delete branch
- [ ] confirm successful deployment
- [ ] test in dev env

### main/prod
- [ ] create PR develop → main
- [ ] merge PR
- [ ] delete branch
- [ ] confirm successful deployment
- [ ] test in prod env

### jira
- [ ] add comments to jira story
- [ ] move jira story to done