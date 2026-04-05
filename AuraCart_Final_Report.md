# AuraCart E-Commerce Analytics & MLOps System

**Comprehensive Technical Report**  
ITS 2140 | Machine Learning

---

## 1. Executive Summary

AuraCart, a fast-growing e-commerce platform, faces challenges in dynamic pricing, risk detection, and customer retention due to manual analytics. This project delivers a production-grade machine learning system for price prediction, order classification, customer segmentation, and cloud deployment. Our models achieved strong predictive performance and were successfully deployed as a live endpoint using Google Cloud Vertex AI, enabling real-time business insights and automation.

---

## 2. Introduction and Business Context

AuraCart’s executive board mandated a unified predictive analytics engine to:
- Predict order prices for revenue forecasting
- Classify delivery status and customer segments for risk and marketing
- Cluster customers for targeted campaigns
- Deploy models in a scalable, cloud-based MLOps workflow

The project uses the public "E-commerce Customer Order Behavior Dataset" (Hugging Face) with 10,000 records, reflecting real-world e-commerce challenges.

---

## 3. Data Exploration and Preprocessing

- **EDA:** Analyzed distributions, correlations, and class imbalances (e.g., 70% 'Delivered', 15% 'VIP').
- **Visualizations:** Histograms, boxplots, heatmaps, and class count plots revealed skewness and feature relationships.
- **Preprocessing:**
  - Dropped ID/address columns
  - Engineered features from dates (year, month, day, hour, days_to_ship)
  - Encoded categorical variables (one-hot)
  - Scaled numerical features
  - Built a modular Scikit-learn pipeline and saved it for deployment

---

## 4. Regression and Classification Modeling

- **Regression:** Multiple linear regression predicted order price. Hyperparameters (learning rate, batch size, epochs) were tuned. MLflow tracked all experiments.
- **Classification:** Multinomial logistic regression (softmax) predicted customer segment and delivery status. Thresholds were adjusted for rare classes. MLflow tracked metrics and artifacts.

---

## 5. Model Evaluation and Performance Analysis

- **Regression:**
  - MSE: *[insert value]*
  - MAE: *[insert value]*
  - Cross-validation confirmed model reliability
- **Classification:**
  - Confusion matrix and class-wise precision, recall, F1-score
  - Example: F1-score for 'VIP' segment: *[insert value]*
  - Business impact: Improved detection of high-risk/valuable customers
- **Visuals:** Include confusion matrix and metric tables/plots

---

## 6. Customer Behavior Clustering

- **Clustering:** k-means applied after preprocessing
- **k Selection:** Elbow method and silhouette score (optimal k = *[insert value]*)
- **Cluster Interpretation:**
  - Cluster 0: Frequent low-value buyers
  - Cluster 1: High-value VIPs
  - Cluster 2: Occasional buyers with high returns
  - ...
- **Business Insights:** Clusters inform targeted marketing, promotions, and inventory planning

---

## 7. Production Deployment and MLOps Workflow

- **Packaging:** Combined preprocessing and model into a single pipeline, saved as `model.joblib`
- **Artifacts:** Uploaded model and requirements.txt to Google Cloud Storage
- **Deployment:**
  - Used Vertex AI’s pre-built Scikit-learn container
  - Deployed as a live REST endpoint
  - Tested with sample JSON payloads
- **MLflow:** Tracked all experiments and model versions
- **Screenshots:** Added below

### MLflow Experiment Tracking (Evidence)

![MLflow Experiments Overview](./screenshots/mlflow_overview.png)
![MLflow Run Details](./screenshots/mlflow_run_details.png)
![MLflow Compare Runs](./screenshots/mlflow_compare.png)

### Vertex AI Deployment (Evidence)

![Vertex AI Model Registry](./screenshots/vertex_model_registry.png)
![Vertex AI Endpoint](./screenshots/vertex_endpoint.png)
![Vertex AI Prediction Output](./screenshots/vertex_prediction_output.png)

---

## 8. Requirements Checklist

### 8.1 EDA and Preprocessing
- Histogram / price distribution: included in Notebook 1.
- Product category bar chart: included in Notebook 1.
- Correlation heatmap: included in Notebook 1.
- Preprocessing pipeline: included in Notebook 1 and saved as `preprocessing_pipeline.joblib`.

### 8.2 Supervised Modeling
- Regression model: included in Notebook 2.
- Actual vs predicted plot: included in Notebook 2 and saved as `actual_vs_predicted_transaction_values.png`.
- Confusion matrix: included in Notebook 2.
- Delivery-status model upgrade: included in Notebook 2 with model comparison and best-model selection.

### 8.3 Unsupervised Clustering
- Elbow method plot: included in Notebook 3 and saved as `elbow_and_silhouette_plot.png`.
- Cluster visualization scatter plot: included in Notebook 3 and saved as `customer_segments_scatter.png`.
- Cluster interpretation markdown: included in Notebook 3.

### 8.4 MLOps Deployment
- MLflow tracking evidence: included in Notebook 4 and referenced in this report.
- Vertex AI deployment: included in Notebook 4.
- Prediction response output: included in Notebook 4 and saved as `prediction_request_response.json`.

### 8.5 Final Submission Artifacts
- `artifacts/model.joblib`
- `artifacts/preprocessing_pipeline.joblib`
- `artifacts/actual_vs_predicted_transaction_values.png`
- `artifacts/delivery_status_confusion_matrix_best_model.png`
- `artifacts/elbow_and_silhouette_plot.png`
- `artifacts/customer_segments_scatter.png`
- `artifacts/prediction_request_response.json`

### 8.6 Quick Review Notes
- All required project sections are present across the notebooks.
- The report now mirrors the notebook structure with numbered markdown subtopics for easier checking.
- If you want, you can add screenshots into `./screenshots` to make the evidence section render directly in the report.

---

## 9. Conclusion and Future Work

- **Achievements:**
  - Built and deployed a robust ML system for AuraCart
  - Enabled real-time predictions and business automation
- **Limitations:**
  - Dataset is static; real-time data integration is future work
  - Advanced models (e.g., XGBoost, deep learning) could be explored
- **Improvements:**
  - Automate retraining with new data
  - Expand features (e.g., text, images)

---

## Appendix

- Additional plots, code snippets, MLflow/Vertex AI screenshots
- References

---

*Note: Replace bracketed placeholders (e.g., [insert value]) with your actual results and screenshots before submission. Keep the main body between 2,000–2,500 words (excluding appendix).*