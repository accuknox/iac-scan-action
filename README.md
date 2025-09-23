# Automate Infrastructure as Code Security Checks with AccuKnox GitHub Action

The **AccuKnox IaC Scan GitHub Action** enables developers and DevSecOps teams to perform automated security scans on Infrastructure-as-Code (IaC) files such as Terraform and Kubernetes manifests. It seamlessly uploads the scan results to the AccuKnox Console, helping teams identify misconfigurations, enforce compliance, and shift security left in the development lifecycle.

Ensure your infrastructure code is secure, compliant, and free from risky misconfigurations — **before it reaches production**.

---

## 🎯 Key Features

- ✅ **IaC Misconfiguration Detection** – Scan Terraform and Kubernetes files for security risks and compliance violations.  
- 🔒 **Shift Left Security** – Integrate security checks directly into your CI/CD pipeline for early issue detection.  
- 📥 **Seamless AccuKnox Console Integration** – Automatically send findings to the AccuKnox dashboard for centralized visibility and triage.  
- ⚙️ **Flexible Configuration** – Support for selective scan directories, frameworks (Terraform / Kubernetes), and baseline comparisons.  
- 🚦 **Fail Builds on Violations** – Choose between hard-fail or soft-fail modes to align with your DevOps policies.  

---

## ⚠️ Prerequisites

Before using this GitHub Action, ensure the following are in place:

- 🔐 **AccuKnox Console Access** – Sign in to your AccuKnox tenant.  
- 🗝️ **API Token & Tenant ID** – Retrieve these from the AccuKnox Console (see Token Generation).  
- 🏷️ **Label Created in Console** – For tagging the uploaded scan reports.  
- 🔑 **GitHub Secrets Configured** – Store the required credentials securely in your repository’s GitHub Secrets.  

---

## 📌 Installation & Usage

### Step 1: Retrieve AccuKnox Credentials

1. Log in to your AccuKnox Console.  
2. Navigate to **Settings → Tokens**.  
3. Click **Create Token** and save the following values:  
   - `accuknox_token`  
4. *(Optional)* Create a label under **Dashboard → Labels** to tag scan results.  

---

### Step 2: Configure GitHub Secrets

1. Go to your GitHub repository: **Settings → Secrets and variables → Actions → New repository secret**.  
2. Add the following secrets:

| Secret Name | Description |
|------------|-------------|
| `TOKEN`    | Your AccuKnox API token for authentication |
| `ENDPOINT` | The AccuKnox API URL (e.g., `cspm.demo.accuknox.com`) |
| `LABEL`    | Label used to tag and group scan results |

These secrets are required to authenticate the scan and send results to your AccuKnox SaaS dashboard.

---

### Step 3: Define Your GitHub Workflow

Create a workflow file (e.g., `.github/workflows/iac-scan.yml`) and add the following configuration:

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
        uses: actions/checkout@v3

      - name: Run IaC scan
        uses: accuknox/iac-scan-action@v0.0.1
        with:
          directory: "."              # Optional: Directory to scan
          compact: true               # Optional: Minimise output
          quiet: true                 # Optional: Show only failed checks
          output_format: json         # Optional: Format of output
          output_file_path: "./results.json" # Optional: Output file path
          token: ${{ secrets.TOKEN }}
```


### ⚙️ Configuration Options (Inputs)

| Input            | Description | Optional/Required | Default |
|-----------------|------------|-----------------|---------|
| `file`           | Specify a single file to scan (e.g., `.tf`). Cannot be used with a directory. | Optional | — |
| `directory`      | Directory with IaC files to scan. | Optional | `.` (current directory) |
| `compact`        | Minimise output (e.g., hides code blocks). | Optional | — |
| `quiet`          | Show only failed checks in output. | Optional | `false` |
| `soft_fail`      | Prevent CI from failing on failed checks. | Optional | `false` |
| `framework`      | Limit scan to a specific framework: terraform, kubernetes, etc. (lowercase) | Optional | `all` |
| `skip_framework` | Skip scanning of a specific framework. | Optional | — |
| `token`          | API token for authenticating with AccuKnox SaaS. | Required | — |
| `endpoint`       | URL of the AccuKnox Console to push results. | Optional | `cspm.demo.accuknox.com` |
| `label`          | Label used in AccuKnox SaaS to organise and identify scan results. | Required | — |
| `output_format`  | Format of the output. Supported: json, cli, etc. | Optional | `cli` |
| `output_file_path` | File path to write output results to. | Optional | — |
| `baseline`       | Path to a baseline file to suppress known findings | Optional | `baseline` |

---

## 🔍 How It Works

1. **Developer pushes code** – Push or pull request triggers the GitHub Action.  
2. **IaC Scanner runs** – Scans Terraform or Kubernetes files for:  
   - Misconfigurations  
   - Policy violations  
   - Compliance issues (e.g., NIST, CIS)  
3. **Scan results uploaded to AccuKnox Console** – Using the provided `token`, `tenant_id`, and `label`.  
4. **Review findings** – Available in AccuKnox Console: **Dashboard → Issues → Findings → Filter by IaC Findings**.  
5. **Optional: Fail the pipeline** – If `soft_fail: false`, the pipeline will break on violations, enforcing CI/CD security.  

---

## 🛠️ Troubleshooting & Best Practices

| Issue | Cause | Solution |
|-------|-------|---------|
| "Missing required input: token" | GitHub secret not set | Ensure `ACCUKNOX_TOKEN` is added in Settings → Secrets |
| "Failed to connect to endpoint" | Incorrect API URL or network issue | Check if the endpoint is correct and accessible |
| No scan results in AccuKnox Console | Missing label or invalid credentials | Verify label, token, and tenant_id values |
| Workflow fails even with minor findings | `soft_fail` not set | Set `soft_fail: true` if you want the build to continue despite findings |
| Empty scan report | Wrong directory or framework used | Check if the directory and framework inputs are correctly set and point to valid IaC files |

---

## 📖 Support & Documentation

- 📚 **Read More:** [AccuKnox Docs](https://www.accuknox.com/docs)  
- 📧 **Contact Support:** support@accuknox.com  

---

## 🏁 Conclusion

The AccuKnox IaC Scan GitHub Action empowers your CI/CD pipelines with automated security scanning for Terraform and Kubernetes configurations. Identify misconfigurations early, enforce policy controls, and maintain continuous compliance for your infrastructure code.

**🔐 Shift Left with AccuKnox – Secure Your Infrastructure from Code to Cloud! ☁️🛡️**
          endpoint: ${{ secrets.ENDPOINT }}
          label: ${{ secrets.LABEL }}
