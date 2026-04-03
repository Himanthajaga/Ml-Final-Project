# GCP Setup Guide — AuraCart Vertex AI Deployment

## Step 1: Open Google Cloud Console

1. Go to **https://console.cloud.google.com**
2. Sign in with your Google account

---

## Step 2: Create a New Project

1. Click the **project dropdown** at the top of the page (next to "Google Cloud")
2. Click **"New Project"**
3. Enter:
   - **Project name:** `auracart-ml-2026` (or any name you like)
   - **Organization:** Leave as default
4. Click **Create**
5. **Copy your Project ID** — you'll need it (it's shown under the project name, looks like `auracart-ml-2026`)

---

## Step 3: Enable Required APIs

1. In the search bar at the top, type **"Vertex AI API"**
2. Click on it, then click **"Enable"**
3. Search for **"Cloud Storage API"** → click **"Enable"**
4. Search for **"Cloud Storage JSON API"** → click **"Enable"** (if not already enabled)

---

## Step 4: Enable Billing

1. Go to **Navigation Menu (☰)** → **Billing**
2. If you don't have a billing account:
   - Click **"Link a billing account"**
   - Follow the prompts to add a credit/debit card
   - Google Cloud offers **$300 free credits** for new accounts — this is more than enough
3. Make sure your project is linked to the billing account

> **Cost estimate:** This project will cost approximately $1–$5 total:
> - GCS storage: < $0.01
> - Vertex AI model upload: Free
> - Vertex AI endpoint (n1-standard-2): ~$0.10/hour — deploy, test, then **delete immediately**

---

## Step 5: Install Google Cloud CLI

### On Windows (PowerShell):
1. Download the installer: https://cloud.google.com/sdk/docs/install-sdk#windows
2. Run **GoogleCloudSDKInstaller.exe**
3. Keep default options and finish installation
4. Close and reopen PowerShell (or VS Code terminal)

Verify installation:
```powershell
gcloud --version
```

### On macOS:
```bash
# Using Homebrew
brew install google-cloud-sdk
```

### Alternative (manual):
```bash
curl https://sdk.cloud.google.com | bash
# macOS/Linux only: reload shell after install
exec -l $SHELL
```

> `exec -l $SHELL` is for Bash/Zsh on macOS/Linux. Do not run it in PowerShell.

After installation, initialize:
```bash
gcloud init
```
- Select your Google account
- Select your project (`auracart-ml-2026`)

---

## Step 6: Authenticate

Run this in your terminal:
```bash
gcloud auth application-default login
```
- A browser window will open
- Sign in with your Google account
- Click **"Allow"**
- Close the browser tab when prompted

This creates a local credential file that the Python SDK uses automatically.

---

## Step 7: Update Notebook 4

Open `notebooks/4_mlops_deployment.ipynb` and update **cell 4.2**:

```python
PROJECT_ID   = "auracart-ml-2026"        # YOUR actual project ID
REGION       = "us-central1"              # Keep this as-is
BUCKET_NAME  = "auracart-ml-YOUR-NAME"    # Must be globally unique — add your name
```

> **Important:** Bucket names must be globally unique across ALL Google Cloud users.
> Add your name or a random suffix, e.g., `auracart-ml-avindu-2026`

---

## Step 8: Re-Run Notebook 4

After updating the configuration, re-run all cells in Notebook 4.
This time, the GCP cells will execute and:
1. Create the GCS bucket
2. Upload `model.joblib` and `requirements.txt`
3. Register the model in Vertex AI
4. Deploy to an endpoint
5. Test the live endpoint

---

## Step 9: Take Screenshots (REQUIRED for report)

After deployment succeeds, take screenshots of:

1. **Vertex AI → Model Registry** — shows `auracart-segment-classifier`
2. **Vertex AI → Endpoints** — shows the active endpoint
3. **Notebook output** — showing the successful prediction response
4. **MLflow UI** — launch with `mlflow ui` and capture experiment runs




---

## Step 10: IMPORTANT — Delete the Endpoint After Testing!

To avoid ongoing charges:

1. Go to **Vertex AI → Endpoints** in the console
2. Click on your endpoint
3. Click **"Undeploy model"** then **"Delete endpoint"**

Or run in the notebook:
```python
endpoint.undeploy_all()
endpoint.delete()
```

The model in the registry and GCS bucket can stay — they cost almost nothing.
