# Regression and Classification

| Key              | Value                                                                                                                                                                                                      |
|:-----------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Course Codes** | BBT 4106, BCM 3104, and BFS 4102                                                                                                                                                                           |
| **Course Names** | BBT 4106: Business Intelligence I (Week 10-12 of 13),<br/>BCM 3104: Business Intelligence and Data Analytics (Week 10-12 of 13) and<br/>BFS 4102: Advanced Business Data Analytics (Week 4-6 of 13)        |
| **Semester**     | April to July 2025                                                                                                                                                                                         |
| **Lecturer**     | Allan Omondi                                                                                                                                                                                               |
| **Contact**      | aomondi@strathmore.edu                                                                                                                                                                                     |
| **Note**         | The lecture contains both theory and practice.<br/>This notebook forms part of the practice.<br/>It is intended for educational purposes only.<br/>Recommended citation: [BibTex](RecommendedCitation.bib) |

## 📦 Project Structure

```text
.
├── 0_helloKenya.ipynb
├── 1a_decision_tree.ipynb
├── 1b_decision_tree.ipynb
├── 2_naive_bayes.ipynb
├── 3_knn.ipynb
├── 4_svm.ipynb
├── 5_random_forest.ipynb
├── LICENSE
├── README.md
├── RecommendedCitation.bib
├── api.py
├── data
│   ├── DataCoSupplyChainDataset.csv
│   ├── DataCoSupplyChainDataset_description.csv
│   ├── DataCoSupplyChainDataset_new_data.csv
│   ├── DataCoSupplyChainDataset_predicted_data.csv
│   ├── DataCoSupplyChainDataset_predicted_with_prob.csv
│   ├── SuperStoreSales.csv
│   ├── SuperStoreSales.xlsx
│   ├── SuperStoreSales_new_data.csv
│   ├── SuperStoreSales_predicted.csv
│   ├── customer_data_with_clusters.csv
│   ├── online_shoppers_intention.csv
│   ├── online_shoppers_intention_new_data.csv
│   ├── online_shoppers_intention_predicted_data.csv
│   ├── online_shoppers_intention_predicted_data_rf.csv
│   ├── online_shoppers_intention_predicted_data_svc.csv
│   ├── paper2_dataset.csv
│   ├── siwaka_dishes_view_profit_per_product.csv
│   ├── siwaka_dishes_view_profit_per_product_new_data.csv
│   ├── siwaka_dishes_view_profit_per_product_predicted_data.csv
│   ├── subscription_churn.csv
│   ├── subscription_churn_new_data.csv
│   └── subscription_churn_predicted_data.csv
├── frontend_tests
│   ├── api_test_DT_classifier.html
│   └── api_test_DT_regressor.html
├── main.py
├── model
│   ├── decisiontree_classifier_baseline.pkl
│   ├── decisiontree_regressor_optimum.pkl
│   ├── knn_classifier_optimum.pkl
│   ├── label_encoders_1b.pkl
│   ├── label_encoders_2.pkl
│   ├── label_encoders_4.pkl
│   ├── label_encoders_5.pkl
│   ├── naive_Bayes_classifier_optimum.pkl
│   ├── onehot_encoder_3.pkl
│   ├── random_forest_classifier_optimum.pkl
│   ├── scaler_4.pkl
│   ├── scaler_5.pkl
│   └── support_vector_classifier_optimum.pkl
└── requirements.txt

4 directories, 50 files
```

## ⚙️ Project Setup Instructions

### Install all the packages listed in `requirements.txt` in a virtual environment

1. Confirm that you have Python installed. You can check this by running:

    ```shell
    python --version
    ```

    or

    ```shell
    python3 --version
    ```

    - If Python is not installed, download and install it from the official website: <https://www.python.org/downloads/>

2. Create and activate a virtual environment to keep your project dependencies isolated from the system Python packages.

   - In the root of your project folder, run:

    ```shell
    python -m venv .venv
    ```

   - To activate the virtual environment, use the following commands:
       - For Windows (Git Bash):

         ```shell
         source .venv/Scripts/activate
         ```

       - For Windows (PowerShell):

         ```shell
         .venv\Scripts\Activate
         ```

       - For macOS/Linux:

         ```shell
         source .venv/bin/activate
         ```

3. Install the packages from **requirements.txt**
    - Once the virtual environment is active, run:

    ```shell
    pip install -r requirements.txt
    ```

    - `-r` tells **pip** to install all packages listed in the file.
    - **pip** will automatically find compatible versions (or raise an error if there is a conflict).

4. You can confirm the installed packages using:

   ```shell
   pip list
   ```
