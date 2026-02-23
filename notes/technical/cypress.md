# Cypress/e2e Tests

## Config/Launch

```bash

# launch:
pnpm test:e2e

# launches script in /e2e/package.json
  "test:e2e": "cypress open --e2e --config-file cypress/cypress.config.ts"
```
In cypress.config.ts, the setupPlugins function from `/e2e/cypress/plugins/index.ts` is registered as the plugin handler.
`setupPlugins` is called when Cypress starts.

`setupPlugins`