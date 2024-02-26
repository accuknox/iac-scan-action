# Automate Infrastructure as Code Security Checks with AccuKnox GitHub Action

## Learn More

- [About Accuknox](https://www.accuknox.com/)


| Input Values | Description | Optional/Required | Default Values |
|--------------|-------------|-------------------|----------------|
| file | Specify a file for scanning; cannot be used with directory input. Filter runners by file type, e.g., '.tf' for Terraform. | Optional | - |
| directory | Directory with infrastructure code and/or package manager files to scan | Optional | `.` |
| compact | Do not display code blocks in output | Optional | - |
| quiet | Display only failed checks | Optional | - |
| output_format | The format of the output. Options: cli, json, junitxml, github_failed_only, or sarif (comma-separated) | Optional | `json` |
| output_file_path | Path and name for the output file, needs to end with a comma for a single output format | Optional | ./results.json |
| soft_fail | Do not return an error code if there are failed checks | Optional | - |
| framework | Run only on a specific infrastructure, values can be Kubernetes or Terraform. | Optional(🚧) | - |
| skip_framework | Skip a specific infrastructure | Optional(🚧) | - |
| baseline | Path to a baseline file to compare. Report will include only failed checks that are not in the baseline | Optional | `baseline` |
| token | The token for authenticating with the CSPM panel | Required | - |
| tenant_id | The ID of the tenant associated with the CSPM panel | Required | - |
| endpoint | The URL of the CSPM panel to push the scan results to | Optional | `cspm.demo.accuknox.com` |
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
          file:                #Optional
          directory:           #Optional
          compact:             #Optional
          quiet:               #Optional
          output_format:       #Optional
          output_file_path:    #Optional
          framework:           #Optional
          skip_framework:      #Optional
          soft_fail:           #Optional
          endpoint:            #Optional
          baseline:            #Optional
          token: 
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
          output_format: 
          output_file_path:
          framework: 
          skip_framework: 
          soft_fail:
          endpoint:
          baseline: 
          token: ${{ secrets.TOKEN }}
          tenant_id: ${{ secrets.TENANT_ID }}

```
