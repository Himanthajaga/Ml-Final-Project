# AuraCart E-Commerce Analytics & MLOps System

## 1. Install All Required Python Packages
Open a terminal and run:

```
pip install pandas numpy scikit-learn matplotlib seaborn joblib mlflow google-cloud-storage google-cloud-aiplatform
```
This covers all imports in your notebooks.

---

## 2. Step-by-Step: How to Run the Project

### a. Run Each Notebook in Order

1. **1_eda_and_preprocessing.ipynb**
   - Loads and cleans the data, builds and saves the preprocessing pipeline.
2. **2_supervised_modeling.ipynb**
   - Loads the pipeline, trains regression and classification models, tracks experiments with MLflow.
3. **3_unsupervised_clustering.ipynb**
   - Loads the pipeline, performs k-means clustering, and analyzes clusters.
4. **4_mlops_deployment.ipynb**
   - Packages the best model, prepares requirements.txt, uploads artifacts to GCS, and deploys to Vertex AI.

### b. How to Run
- Open each notebook in Jupyter or VS Code.
- Run all cells from top to bottom.
- If you see errors about missing packages, install them using pip as above.

---

## 3. Adapting for Your GCP Buckets and Vertex AI

### a. Set Your GCP Project and Bucket
- In `4_mlops_deployment.ipynb`, replace:
  - `'your-gcs-bucket-name'` with your actual GCS bucket name.
  - `'your-gcp-project-id'` with your GCP project ID.
  - `'your-endpoint-id'` with the endpoint ID you get after deployment.

### b. Authenticate to Google Cloud
- Run in terminal:
  ```
  gcloud auth application-default login
  ```
- Make sure your user has permissions for Storage and Vertex AI.

### c. Enable APIs
- In Google Cloud Console, enable:
  - Vertex AI API
  - Cloud Storage API

### d. Upload Artifacts
- The notebook will upload `model.joblib` and `requirements.txt` to your bucket.

### e. Deploy Model
- The notebook will register and deploy the model using the pre-built Scikit-learn container.
- After deployment, copy the endpoint ID for prediction.

---

## 4. How to Check Everything Works
- Each notebook should run top-to-bottom without errors.
- MLflow UI (`mlflow ui` in terminal) will show your experiment runs.
- In Vertex AI Console, you should see your model and endpoint.
- The last cell in `4_mlops_deployment.ipynb` lets you send a test prediction to your endpoint.

---

## 5. Common Changes to Apply
- Update all placeholder values (`your-gcs-bucket-name`, `your-gcp-project-id`, `your-endpoint-id`) to your actual GCP details.
- If your model expects different input features, update the sample `instance` in the test cell to match your data schema.

---

## 6. MLflow UI: Check Runs and Capture Screenshots

### Step-by-Step: Launch MLflow UI

1. Open terminal in your project directory:

```powershell
cd c:\Users\UsEr\IJSE\ML-Final-Project
```

2. Launch MLflow UI:

```powershell
mlflow ui
```

3. Open the dashboard URL shown in terminal (usually):

```text
http://127.0.0.1:5000
```

You should see experiment runs from `2_supervised_modeling.ipynb`, including parameters, metrics, and artifacts.

### Capture Required Screenshots

1. Screenshot 1 - Experiments Overview
- Open the Experiments page in MLflow.
- Capture a screenshot that shows multiple runs.

2. Screenshot 2 - Individual Run Details
- Open one run.
- Capture parameters, metrics (accuracy/precision/recall/F1), and artifacts.

3. Screenshot 3 - Comparison View
- Select multiple runs.
- Click Compare.
- Capture a screenshot showing metric comparison.

### Quick Commands

| Action | Command |
|---|---|
| Start MLflow UI | `mlflow ui` |
| Stop MLflow UI | `Ctrl + C` |
| Run on another port | `mlflow ui --port 8080` |

### Add Screenshots to Report

Insert the screenshots in `AuraCart_Final_Report.md` under a section like:

```markdown
### MLflow Experiment Tracking
![MLflow Experiments Overview](./screenshots/mlflow_overview.png)
![MLflow Run Details](./screenshots/mlflow_run_details.png)
![MLflow Compare Runs](./screenshots/mlflow_compare.png)
```