# install-action

Github actions to install AccuKnox IaC Scanner.

## Learn More

- [About Accuknox](https://www.accuknox.com/)

## Inputs

```yaml
name: 'Accuknox IaC Scan'
description: 'Run Scan against infrastructure as code.'
inputs:
  file:
    description: 'File with infrastructure code or packages to scan'
    required: false
  directory:
    default: '.'
    description: 'Directory with infrastructure code and/or package manager files to scan'
    required: false
  compact:
    description: 'Do not display code blocks in output'
    required: false
  quiet:
    description: 'display only failed checks'
    required: false
  output_format:
    description: 'The format of the output. cli, json, junitxml, github_failed_only, or sarif (comma separated)'
    required: false
    default: 'json'
  output_file_path:
    description: 'Path and name for output file, needs to end with a comma for a single output format'
    required: false
  soft_fail:
    description: 'do not return an error code if there are failed checks'
    required: false
  framework:
    description: 'run only on a specific infrastructure'
    required: false
  skip_framework:
    description: 'skip a specific infrastructure'
    required: false
  github_pat:
    description: 'Environment variable name for a Github personal access token for scanning external modules sourced from private repositories'
    required: false
  token:
    description: 'The token for authenticating with the CSPM panel.'
    required: true
  tenant_id:
    description: 'The ID of the tenant associated with the CSPM panel.'
    required: true
  endpoint:
    description: 'The URL of the CSPM panel to push the scan results to.'
    required: true
    default: 'cspm.demo.accuknox.com'
```

## Usage

Steps for using Install-action in a workflow yaml file 
- Checkout into the repo using checkout action.
- Utilize the accuknox/iac-scan-action repository with version tag v0.0.1.

### Token Generation from Accuknox SaaS and Viewing Tenant ID

Navigate to Tokens within the Settings section in the sidebar:

![1](https://github.com/udit-uniyal/iac-scan-action/assets/115368361/e3916e08-ab5c-46da-8504-d47778f7d6a8)

Click on Create Token: 
After clicking on 'Create Token,' the Tenant ID will be visible.
![2](https://github.com/udit-uniyal/iac-scan-action/assets/115368361/b49e25dd-fca0-458e-84d3-48de152ef57d)


Click on Generate:

![3](https://github.com/udit-uniyal/iac-scan-action/assets/115368361/11a2b277-649d-4ef7-b51f-861e8b947b59)


### workflow steps:

```yaml
      - name: Run IaC scan
        uses: accuknox/iac-scan-action@v0.0.1
        with:
          file:
          directory:
          compact:            
          quiet:                
          output_file_path: 
          framework: 
          skip_framework: 
          soft_fail:         
          github_pat: 
          token: 
          endpoint: 
          tenant_id: 
```


## Sample Configuration 

```yaml

name: AccuKnox IaC Scan Workflow

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  tests:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@main
      
      - name: Run IaC scan
        uses: accuknox/iac-scan-action@v0.0.1
        with:
          file: 
          directory: 
          compact: 
          quiet: 
          output_file_path:
          framework: 
          skip_framework: 
          soft_fail:
          github_pat: 
          token: 
          endpoint: 
          tenant_id:

```
