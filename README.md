appopsdxcli
===========

The CLI for Prodly AppOps DX.

[![Version](https://img.shields.io/npm/v/appopsdxcli.svg)](https://npmjs.org/package/appopsdxcli)
[![CircleCI](https://circleci.com/gh/prodly/appopsdxcli/tree/master.svg?style=shield)](https://circleci.com/gh/prodly/appopsdxcli/tree/master)
[![Appveyor CI](https://ci.appveyor.com/api/projects/status/github/prodly/appopsdxcli?branch=master&svg=true)](https://ci.appveyor.com/project/heroku/appopsdxcli/branch/master)
[![Codecov](https://codecov.io/gh/prodly/appopsdxcli/branch/master/graph/badge.svg)](https://codecov.io/gh/prodly/appopsdxcli)
[![Greenkeeper](https://badges.greenkeeper.io/prodly/appopsdxcli.svg)](https://greenkeeper.io/)
[![Known Vulnerabilities](https://snyk.io/test/github/prodly/appopsdxcli/badge.svg)](https://snyk.io/test/github/prodly/appopsdxcli)
[![Downloads/week](https://img.shields.io/npm/dw/appopsdxcli.svg)](https://npmjs.org/package/appopsdxcli)
[![License](https://img.shields.io/npm/l/appopsdxcli.svg)](https://github.com/prodly/appopsdxcli/blob/master/package.json)

<!-- toc -->
* [Debugging your plugin](#debugging-your-plugin)
<!-- tocstop -->
<!-- install -->
```sh-session
$ sfdx plugins:install appopsdxcli
```
<!-- usage -->
```sh-session
$ npm install -g appopsdxcli
$ appopsdxcli COMMAND
running command...
$ appopsdxcli (-v|--version|version)
appopsdxcli/1.1.0 darwin-x64 node-v11.6.0
$ appopsdxcli --help [COMMAND]
USAGE
  $ appopsdxcli COMMAND
...
```
<!-- usagestop -->
<!-- commands -->
* [`appopsdxcli appops:deploy [-s <string>] [-d <string>] [-t <string>] [-p <string>] [-v <string>] [-u <string>] [--apiversion <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]`](#appopsdxcli-appopsdeploy--s-string--d-string--t-string--p-string--v-string--u-string---apiversion-string---json---loglevel-tracedebuginfowarnerrorfataltracedebuginfowarnerrorfatal)

## `appopsdxcli appops:deploy [-s <string>] [-d <string>] [-t <string>] [-p <string>] [-v <string>] [-u <string>] [--apiversion <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]`

Launches an AppOps relational data deployment for a scratch org.

```
USAGE
  $ appopsdxcli appops:deploy [-s <string>] [-d <string>] [-t <string>] [-p <string>] [-v <string>] [-u <string>] 
  [--apiversion <string>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

OPTIONS
  -d, --destination=destination                                                     destination connection name or
                                                                                    record id

  -p, --plan=plan                                                                   deployment plan to deploy name or
                                                                                    record id

  -s, --source=source                                                               source connection name or record id

  -t, --dataset=dataset                                                             data set to deploy name or record id

  -u, --targetusername=targetusername                                               username or alias for the target
                                                                                    org; overrides default target org

  -v, --targetdevhubusername=targetdevhubusername                                   username or alias for the dev hub
                                                                                    org; overrides default dev hub org

  --apiversion=apiversion                                                           override the api version used for
                                                                                    api requests made by this command

  --json                                                                            format output as json

  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)  [default: warn] logging level for
                                                                                    this command invocation

EXAMPLES
  $ sfdx appops:deploy -u FixesScratchOrg -v MainDevHub
     Command output... deploying from the dev hub, the control org, to the scratch org.
     Command output...
  
  $ sfdx appops:deploy --targetusername test-utxac7gbati9@example.com --targetdevhubusername jsmith@acme.com 
     Command output... deploying from the dev hub, the control org, to the scratch org. Long param names.
  
  $ sfdx appops:deploy -u test-utxac7gbati9@example.com -v jsmith@acme.com -d "UAT Sandbox Connection"
     Command output... deploying from the scratch org to the UAT sandbox, using the named connection record in the dev 
  hub, control org.
  
  $ sfdx appops:deploy --targetusername test-utxac7gbati9@example.com --targetdevhubusername jsmith@acme.com --source 
  "UAT Sandbox Connection"
     Command output... deploying to the scratch org from the UAT sandbox, using the named connection record in the dev 
  hub, control org. Long param names.
```

_See code: [src/commands/appops/deploy.ts](https://github.com/prodly/appopsdxcli/blob/v1.1.0/src/commands/appops/deploy.ts)_
<!-- commandsstop -->
<!-- debugging-your-plugin -->
# Debugging your plugin
We recommend using the Visual Studio Code (VS Code) IDE for your plugin development. Included in the `.vscode` directory of this plugin is a `launch.json` config file, which allows you to attach a debugger to the node process when running your commands.

To debug the `hello:org` command: 
1. Start the inspector
  
If you linked your plugin to the sfdx cli, call your command with the `dev-suspend` switch: 
```sh-session
$ sfdx hello:org -u myOrg@example.com --dev-suspend
```
  
Alternatively, to call your command using the `bin/run` script, set the `NODE_OPTIONS` environment variable to `--inspect-brk` when starting the debugger:
```sh-session
$ NODE_OPTIONS=--inspect-brk bin/run hello:org -u myOrg@example.com
```

2. Set some breakpoints in your command code
3. Click on the Debug icon in the Activity Bar on the side of VS Code to open up the Debug view.
4. In the upper left hand corner of VS Code, verify that the "Attach to Remote" launch configuration has been chosen.
5. Hit the green play button to the left of the "Attach to Remote" launch configuration window. The debugger should now be suspended on the first line of the program. 
6. Hit the green play button at the top middle of VS Code (this play button will be to the right of the play button that you clicked in step #5).
<br><img src=".images/vscodeScreenshot.png" width="480" height="278"><br>
Congrats, you are debugging!
