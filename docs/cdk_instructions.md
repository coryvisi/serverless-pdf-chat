---
title: CDK Instructions
parent: Developer Documentation
nav_order: 3
---
# CDK Instructions

## Contents

* [Prerequisities](#prerequisites)
* [Setup Instruction](#setup-instructions)
* [Useful Commands](#useful-commands)
* [Visual Studio Code Debugging](#visual-studio-code-debugging)

## Prerequisites

1. Install [Python](https://www.python.org/downloads/) on your local computer
1. Install [Node.js](https://nodejs.org/en/download/package-manager/) on your local computer
   - CDK uses Node.js under the hood; the code will be in Python for this application
1. Install [CDK](https://docs.aws.amazon.com/cdk/v2/guide/getting_started.html) on your local computer
   ```bash
   sudo npm install -g aws-cdk
   ```

## Setup Instructions

The `cdk.json` file tells the CDK Toolkit how to execute your app.

This project is set up like a standard Python project.  The initialization
process also creates a virtualenv within this project, stored under the `.venv`
directory.  To create the virtualenv it assumes that there is a `python3`
(or `python` for Windows) executable in your path with access to the `venv`
package. If for any reason the automatic creation of the virtualenv fails,
you can create the virtualenv manually.

To manually create a virtualenv on MacOS and Linux:

```bash
python3 -m venv .venv
```

After the init process completes and the virtualenv is created, you can use the following
step to activate your virtualenv.

```bash
source .venv/bin/activate
```

If you are a Windows platform, you would activate the virtualenv like this:

```bash
% .venv\Scripts\activate.bat
```

Once the virtualenv is activated, you can install the required dependencies.

```bash
pip install -r requirements.txt
```

At this point you can now synthesize the CloudFormation template for this code.

```bash
cdk synth
```

To add additional dependencies, for example other CDK libraries, just add
them to your `setup.py` file and rerun the `pip install -r requirements.txt`
command.

---

## Useful Commands

 1. `cdk ls`          list all stacks in the app
 1. `cdk synth`       emits the synthesized CloudFormation template
 1. `cdk deploy`      deploy this stack to your default AWS account/region
 1. `cdk diff`        compare deployed stack with current state
 1. `cdk docs`        open CDK documentation

 ---

## Visual Studio Code Debugging

 To configure Visual Studio Code for debugging CDK, use the following launch configuration in `launch.json`:

 ```json
 {
	"version": "0.2.0",
	"configurations": [
		{
			"name": "CDK Synth",
			"type": "python",
			"request": "launch",
			"program": "app.py",
			"console": "integratedTerminal",
			"justMyCode": true
		}
	]
}
```