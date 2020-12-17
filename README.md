sfdx-source-scanner
=========================

The source scanner will run static analysis on Salesforce source to ensure both best practices and potential errors are avoided. The scanner is configurable, this will allow you to define the rules that are executed, any files that you wish to ignore rules on, the severity of each rule and any specific error messages that should be output when a rule is violated.

[![Version](https://img.shields.io/npm/v/sfdx-source-scanner.svg)](https://npmjs.org/package/sfdx-source-scanner)
[![CircleCI](https://circleci.com/gh/gavinhughpalmer/sfdx-source-scanner/tree/master.svg?style=shield)](https://circleci.com/gh/gavinhughpalmer/sfdx-source-scanner/tree/master)
[![Known Vulnerabilities](https://snyk.io/test/github/gavinhughpalmer/sfdx-source-scanner/badge.svg)](https://snyk.io/test/github/gavinhughpalmer/sfdx-source-scanner)
[![Downloads/week](https://img.shields.io/npm/dw/sfdx-source-scanner.svg)](https://npmjs.org/package/sfdx-source-scanner)
[![License](https://img.shields.io/npm/l/sfdx-source-scanner.svg)](https://github.com/gavinhughpalmer/sfdx-source-scanner/blob/master/package.json)

<!-- toc -->
* [Installation](#installation)
* [Usage](#usage)
* [Rule Sets](#rule-sets)
* [Rule Refrence](#rule-refrence)
* [Debugging your plugin](#debugging-your-plugin)
<!-- tocstop -->


<!-- install -->

# Installation
To install the source scanner you can either use NPM or the sfdx plugins command to install as shown below.
```sh-session
$ npm install -g sfdx-source-scanner
```

```sh-session
$ sfdx plugins:install sfdx-source-scanner
```
# Usage
Once the plugin is installed it can be executed using the below [Commands](#commands) section, the plugin expects a rule refrence to be passed in this allows you to configure the rule refrence, there will be more detail below at [Rule Sets](#rule-sets).
<!-- Can we generate this from a file in the repo? -->
```json
{
    "name": "Example Rule Set (All)",
    "description": "This rule set shows all the scanners as enabled",
    "scanners": [
        { "name": "any-file-scanner" },
        { "name": "approval-process-scanner" },
        { "name": "duplicate-rule-scanner" },
        { "name": "flow-scanner" },
        { "name": "field-scanner" },
        { "name": "object-scanner" },
        { "name": "permission-set-scanner" },
        { "name": "quick-action-scanner" },
        { "name": "validation-rule-scanner" },
        { "name": "workflow-scanner" }
    ]
}
```
*Additional example rulesets can be found at [examples](/src/main/config/examples)*

## Commands
<!-- commands -->
* [`sfdx scanner:source:scan -s <string> [-r <string>] [-d <string>] [-e <number>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]`](#sfdx-scannersourcescan--s-string--r-string--d-string--e-number---json---loglevel-tracedebuginfowarnerrorfataltracedebuginfowarnerrorfatal)

## `sfdx scanner:source:scan -s <string> [-r <string>] [-d <string>] [-e <number>] [--json] [--loglevel trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]`

This utility will scan salesforce metadata (in source format) to identify any potential issues, this can be built into CI pipelines to ensure work admins are checking in is up to standard

```
USAGE
  $ sfdx scanner:source:scan -s <string> [-r <string>] [-d <string>] [-e <number>] [--json] [--loglevel 
  trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL]

OPTIONS
  -d, --targetdir=targetdir                                                         [default: force-app] The directory
                                                                                    that should be targeted whilst
                                                                                    scanning the files

  -e, --errorlevel=errorlevel                                                       [default: 3] The level at which the
                                                                                    severty should raise an error,
                                                                                    otherwise the results will be logged
                                                                                    silently. Numbers range between 1-5,
                                                                                    where 1 is Minor and 5 is Extreme

  -r, --resultsfile=resultsfile                                                     The path to the file that the
                                                                                    results should be written to

  -s, --rulesetfile=rulesetfile                                                     (required) The file path for the
                                                                                    rule set that should be applied

  --json                                                                            format output as json

  --loglevel=(trace|debug|info|warn|error|fatal|TRACE|DEBUG|INFO|WARN|ERROR|FATAL)  [default: warn] logging level for
                                                                                    this command invocation

EXAMPLE
  $ sfdx config:scan --targetdir force-app --errorlevel 2
       Errors in the files have been identified
```

_See code: [lib/commands/scanner/source/scan.js](https://github.com/gavinhughpalmer/sfdx-source-scanner/blob/v0.0.0/lib/commands/scanner/source/scan.js)_
<!-- commandsstop -->

# Rule Sets
<!-- Configurable items, setting the priotities, error messages, and other configurable items, ignoring files, including or excluding rules -->

<!-- Can we autogenerate the rule refrence? -->
# Rule Refrence
The rules are executed by a number of scanners, each scanner is defined for a set of files (based of a file name pattern, mostly the extension for that file), within each scanner a number of rules are defined. A few of the rules are reused across a number of scanners. Below we will go into the detail for each of the scanners and the rules that are available for each.

## Any File Scanner

## Approval Process Scanner

## Duplicate Rule Scanner

## Filed Scanner

## Flow Scanner

## Object Scanner

## Permission Set Scanner

## Quick Action Scanner

## Validation Rule Scanner

## Workflow Rule Scanner
The workflow rule scanner is slightly unique as this actually splits the file up to scan for the components that make up the workflow rule, that is the rule itself, field updates and email alerts

### Workflow Rule

### Field Update Rule

### Email Alert Rule


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
