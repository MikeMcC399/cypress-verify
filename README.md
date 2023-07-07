# verify logs "Task without title" in GitHub when successful
https://github.com/cypress-io/cypress/issues/26768

### Current behavior

If `npx cypress verify` is executed in a GitHub workflow then the log shows

```text
[STARTED] Task without title.
[SUCCESS] Task without title.
```

### Desired behavior

Executing `npx cypress verify` in a GitHub workflow should give a clearer message in any logs produced which link the logs to the action of verifying Cypress. The text "Task without a title" should not appear.

### Test code to reproduce

```yml
jobs:
  verify:
    runs-on: ubuntu-22.04
    steps:
        - name: Checkout
          uses: actions/checkout@v3
        - run: npm ci
        - run: npx cypress verify
```

- Example workflow on https://github.com/MikeMcC399/cypress-verify/blob/main/.github/workflows/test-verify.yml
- See https://github.com/MikeMcC399/cypress-verify/actions/runs/4988122142/jobs/8930550019 for regular (non-debug) logs

### Cypress Version

First reported in version `12.12.0`
Still present in version `12.16.0`

### Node version

18.16.0

### Operating System

Ubuntu 22.04

### Debug Logs

- See https://github.com/MikeMcC399/cypress-verify/actions/runs/4988122142/jobs/8930550117

```text
Run npx cypress verify
  npx cypress verify
  shell: /usr/bin/bash -e {0}
  env:
    DEBUG: cypress:*
2023-05-16T05:11:12.679Z cypress:cli:cli cli starts with arguments ["/usr/local/bin/node","/home/runner/work/cypress-verify/cypress-verify/node_modules/.bin/cypress","verify"]
2023-05-16T05:11:12.681Z cypress:cli NODE_OPTIONS is not set
2023-05-16T05:11:12.681Z cypress:cli:cli program parsing arguments
2023-05-16T05:11:12.684Z cypress:cli parsed cli options {}
2023-05-16T05:11:12.831Z cypress:cli verifying Cypress app
2023-05-16T05:11:12.832Z cypress:cli checking environment variables
2023-05-16T05:11:12.836Z cypress:cli checking if executable exists /home/runner/.cache/Cypress/12.12.0/Cypress/Cypress
2023-05-16T05:11:12.851Z cypress:cli Binary is executable? : true
2023-05-16T05:11:12.854Z cypress:cli binaryDir is  /home/runner/.cache/Cypress/12.12.0/Cypress
2023-05-16T05:11:12.854Z cypress:cli Reading binary package.json from: /home/runner/.cache/Cypress/12.12.0/Cypress/resources/app/package.json
2023-05-16T05:11:12.857Z cypress:cli Found binary version 12.12.0 installed in: /home/runner/.cache/Cypress/12.12.0/Cypress
2023-05-16T05:11:12.859Z cypress:cli could not read binary_state.json file at "/home/runner/.cache/Cypress/12.12.0/binary_state.json"
2023-05-16T05:11:12.860Z cypress:cli {}
2023-05-16T05:11:12.860Z cypress:cli is Verified ? undefined
2023-05-16T05:11:12.861Z cypress:cli force verify
2023-05-16T05:11:12.861Z cypress:cli running binary verification check 12.12.0

[STARTED] Task without title.
2023-05-16T05:11:12.869Z cypress:cli clearing out the verified version
2023-05-16T05:11:12.871Z cypress:cli undefined DISPLAY environment variable
2023-05-16T05:11:12.871Z cypress:cli Cypress will spawn its own Xvfb
2023-05-16T05:11:12.871Z cypress:cli needs Xvfb? true
2023-05-16T05:11:12.872Z cypress:cli Starting Xvfb
2023-05-16T05:11:12.915Z cypress:cli disabling Electron sandbox
2023-05-16T05:11:12.915Z cypress:cli running smoke test
2023-05-16T05:11:12.915Z cypress:cli using Cypress executable /home/runner/.cache/Cypress/12.12.0/Cypress/Cypress
2023-05-16T05:11:12.915Z cypress:cli smoke test command: /home/runner/.cache/Cypress/12.12.0/Cypress/Cypress --no-sandbox --smoke-test --ping=462
2023-05-16T05:11:12.915Z cypress:cli smoke test timeout 30000 ms
2023-05-16T05:11:14.355Z cypress:cli smoke test stdout "It looks like you are running the Cypress binary directly.

This is not the recommended approach, and Cypress may not work correctly.

Please install the cypress NPM package and follow the instructions here:

https://on.cypress.io/installing-cypress
462"
2023-05-16T05:11:14.356Z cypress:cli Stopping Xvfb
2023-05-16T05:11:14.378Z cypress:cli write verified: true
2023-05-16T05:11:14.379Z cypress:cli could not read binary_state.json file at "/home/runner/.cache/Cypress/12.12.0/binary_state.json"
[SUCCESS] Task without title.
```

### Other

In the case that `npx cypress verify` fails on GitHub, then the error message logged is long and descriptive. It is only the success message which lacks information.
