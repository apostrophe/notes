# Cypress/e2e Tests

## Config/Launch

```bash
# launch with command:
$ pnpm test:e2e

# launches script in /e2e/package.json
  "test:e2e": "cypress open --e2e --config-file cypress/cypress.config.ts"
```
`config.ts` contains the `ExtendedEnv` interface (create form/strcutre of this object), which is wrapped into `ExtCypressConfig`, an instance `Cypress.PluginConfigOptions`
`cypress.config.ts` consists of `baseurl` and `localEnv`, an instance of `ExtendedDev`. This class eventually exports the `defineConfig` function, used in `cypress.config.dev.ts` or `cypress.config.test.ts`.

`setupNodeEvents: setupPlugins,` in `cypress.config.ts` indicates how the the plugins are created. `setupPlugins` is a function in `e2e/cypress/plugins/index.ts`

There is a the below log statement -- where does this appear?
`console.log('[CONFIGURATION] run db setup:', config.env.db_setup);`

`setupPlugins`



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

