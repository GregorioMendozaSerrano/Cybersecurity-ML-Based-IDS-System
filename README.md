# **Intrusion Detection System (IDS) based on Machine Learning**
## Gregorio Mendoza Serrano

### Overview

This project focuses on developing an **Intrusion Detection System (IDS)** using **artificial intelligence algorithms** to analyze network traffic and detect potential intrusions. Initially, two models were considered: a **Convolutional Neural Network (CNN)** and a **RandomForest**. However, after extensive testing, **RandomForest** was chosen for its high performance and stability. Additionally, the **K-nearest neighbors (KNN)** algorithm was incorporated to enhance robustness and comparison. The CNN model, although promising, faced unresolved instability issues and remains experimental for future improvements.

![Alt text](cybersecurity2_img.jpg)

---

## Technical Details

The solution follows a structured approach in two main phases:

1. **Data Preparation and Exploratory Analysis** - Performed in the notebook `GMS-ML-IDS-Data-Preparation.ipynb`.
2. **Model Development, Evaluation, and Explainability** - Detailed in the notebook `GMS-ML-IDS-Models-and-Evaluation.ipynb`.

---

## Data Preparation

### Objectives
The goal was to curate a dataset suitable for training and testing the models, focusing on:
- **Binary classification** (0: Benign, 1: Attack).
- **Maximizing test metrics** while keeping the dataset easily interpretable.
- **Feature reduction** to minimize training time and prevent overfitting.
- **Cost-effectiveness** by limiting manual work.

### Data Processing Steps

1. **Importing the dataset** and removing null/duplicate values.
2. **Feature renaming** for better manipulation.
3. **Converting the dataset** from multiclass to binary.
4. **Feature selection** using technical definitions, correlation matrices, and variance analysis.
5. **Outlier Study** using the interquartile range (IQR), where outlier removal was avoided to preserve attack data.
6. **Class Balancing** via downsampling of the benign class to ensure equal representation of benign and attack records.

The resulting dataset consists of **10 features**, chosen after rigorous correlation and variance analysis. These features represent the most significant indicators for intrusion detection.

---

## Model Implementation

The model-building phase focused on two algorithms: **RandomForest** and **KNN**. The CNN model, despite improvements, remained unstable and was excluded from final implementation. Here is an outline of the approach:

- **RandomForest**: The algorithm showed consistent performance, achieving **99.46% accuracy** on the test set. This high performance was validated with **cross-validation**, confirming the model's robustness.
  
- **KNN**: This algorithm served as a complementary approach. The optimal parameter `k=5` was identified by plotting accuracy curves. KNN achieved **98% accuracy** and exhibited good stability, though it demands higher memory during prediction.

Both models were evaluated based on multiple metrics, with **RandomForest** ultimately being chosen as the primary solution due to its superior performance and computational efficiency.

### Computational Considerations

- **RandomForest**: Requires manageable computational resources. Hyperparameters are relatively easy to tune, making it cost-effective.
- **KNN**: While effective, KNN's memory demands during prediction and sensitivity to irrelevant features make it less optimal in certain scenarios.

---

## Model Evaluation

### Selected Metrics

Given the sensitivity of the problem, where predicting an attack as benign is critical, the following metrics were chosen:
- **Recall**: Focused on detecting true attacks.
- **F1-Score**: Balances precision and recall, providing insights into performance for each class.
- **Accuracy**: Offers a global perspective on model performance.
- **Confusion Matrix**: Compares predicted and actual values for each class.
- **ROC Curve**: Visualizes model robustness across different classification thresholds.

### Final Results

- **RandomForest**: Achieved **99% accuracy**, with 100% recall for benign traffic and 99% recall for attack traffic. The model exhibited no signs of overfitting.
- **KNN**: Reached **98% accuracy** and demonstrated stability across both benign and attack classes.

In a side-by-side comparison, **RandomForest** was found to be slightly better calibrated and easier to explain, making it the preferred solution.

---

## Explainability

In compliance with European AI regulations on explainability, feature importance was analyzed for both models using the SHAP library (https://shap.readthedocs.io/en/latest/).

### RandomForest
The most influential feature was `Packet_Length_Mean`, while `Idle_Mean` was the least significant. This insight helps explain how the model makes its decisions and offers guidance for future improvements.

### KNN
For KNN, the most critical feature was `Fwd_IAT_Total`, with `Bwd_Packet_Length_Std` contributing the least. However, due to the computational cost, only 100 random samples were analyzed.

---

## Conclusion

The **RandomForest** algorithm was selected as the optimal solution due to its performance, ease of explainability, and computational efficiency. The **KNN** model serves as a reliable backup option, while the **CNN** model remains experimental for potential future use. Together, these models provide a robust system for intrusion detection that balances accuracy, computational cost, and explainability.


