# gha-scan-bd-sast

Github action containing the scan bd-SAST functionality for CI pipeline workflow

Note the action requires the following permission:

```
permissions:
    contents: read
```

For example usage, please view the workflow scanbd-SAST.yaml, which is found under
`./github/workflows`

Most likely, the scan bd-SAST job will require a larger runner, when the action is
used internally (e.g. within a PR), hence it should be invoked with

```
runs-on: internal-large
```

Note the value `internal-large` can be retrieved using the helper function
setRunner from [gha-helper](https://github.tools.sap/AI/gha-helper) action, e.g.
using

```
setRunner:
  runs-on: internal-small
  permissions: {}
  outputs:
    runner-small: ${{ steps.set-runner.outputs.runner-small }}
    runner-large: ${{ steps.set-runner.outputs.runner-large }}
  steps:
    - uses: AI/gha-helper@v0.0.7
      id: set-runner
      with:
        function: setRunner
        release: false
```

## Context

The library scan tool `BlackDuck Binary Analyst` (bd-SAST) - formally known as
Protecode - must be used in a compliant build and its result must be uploaded to
[Cumulus](https://wiki.one.int.sap/wiki/display/DevFw/Documentation%3A+Cumulus).

## Prerequisites

For validating scan results in the BD-SAST UI, you first have to register with the
Black Duck service [here](https://bd-SAST.tools.sap/sso/login/).

The AI unit shares 1 protecode group called
[AI Platform](https://bd-SAST.tools.sap/#/groups/2997/applications). The group
members are managed
[here](https://svmprod-zdohvhnx0v.dispatcher.int.sap.eu2.hana.ondemand.com/webapp/index.html#/ProtecodeSelfServiceEntry/2997).

Current admins are

- Sotiris Oikonomou

## Technical user for black duck 


## Open tasks

Note the image used for testing the scan in this repo is only a test image for
now. This might not be available all the time, a proper test image should be
made available, which allows testing the action, anytime.
