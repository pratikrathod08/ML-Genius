# 🤖 ML-Genius

**ML-Genius** is a lightweight Python library that automates key machine learning tasks including preprocessing, training, and evaluation — with just a few lines of code. It supports both regression and classification pipelines and enables users to quickly test multiple models, select the best one, and store reusable components.

---

## 🚀 Features

- One-line data preprocessing with support for CSV/Excel
- Automated model training and evaluation
- Supports both regression and classification
- Easily store and reuse trained models and preprocessors
- Extensible for new models and components

---

## How to use 

### Installation 

Github : `https://github.com/pratikrathod08/ML-Genius`

Pypi : `pip install ML-Genius==0.0.2`

### Read Data

```bash
from ml_genius.ml.preprocessor.datareader import ReadData

reader = ReadData()
df = reader.read_csv("data.csv")
```

### Describe Data

```bash
from ml_genius.ml.preprocessor.datadescriber import DataDescribe

desc = DataDescribe(df_csv, target_column="target_column")
desc.summarize()  # Print summary
summary_data = desc.get_summary_dict()
```

### Preprocess Data
```bash

from ml_genius.ml.preprocessor.preprocess import AutoPreprocess

# Create the processor instance
processor = AutoPreprocess(
    path="data.csv",                                        # Path to the file
    file_type="csv",                                        # "csv" or "excel"
    store_path="output/processed.csv",                      # Path to save the result
    target_column="price",                                  # Target column name
    preprocessor_store_path="output/preprocessor.pkl",      # path to store preprocessor 
    encoding="utf-8",                                       # Optional parameters passed to read_csv
    delimiter=","                                           # Optional (if CSV uses different delimiter)
)

# Run the full processing pipeline
processed_df= processor.process()

# You can now work with processed_df
print(processed_df.head())
```

### Use stored preprocessor

```bash 
import pandas as pd 
import joblib 

preprocessor = joblib.load("output/preprocessor.pkl")
csv_path = "data/data.csv"
df = pd.read_csv(csv_path)
preprocessed_df = preprocessor.transform(df)
preprocessed_df = pd.DataFrame(preprocessed_df)

## Note : add headers and output column in processed df as it is returning processed raw data. 
```

### Train Model

### Regression

```bash 
from ml_genius.ml.regression import AutoRegression

regression = AutoRegression(path="processed.csv", filetype="csv", target_column="target_column")
result = regression.train_model()
print(result)

```

### Models Available 

- Linear Regression
- Ridge Regression 
- Decision Tree
- Random Forest
- Gradiant Boosting

### Output Parameters

- best_model_name
- model
- model_params
- r2_score
- rmse
- mse

### Save and Use Trained Model

```bash

import joblib 
import numpy as np
import pandas as pd 
from sklearn.metrics import r2_score, mean_squared_error

## Store trained model to local system
model = result.get("model")
joblib.dump(model, "model.pkl")

## Load model
model = joblib.load("model.pkl")

## Import data and predict
df = pd.read_csv("processed.csv")
X = df.drop(columns=['target_column'])
y = df["target_column"]

y_pred = model.predict(X)

## Evaluate model 
print("r2_score : ", r2_score(y_pred, y))
print("mse : ", mean_squared_error(y_pred, y))
print("rmse : ", np.sqrt(mean_squared_error(y_pred, y)))

```

### Classification

```bash 
from ml_genius.ml.classification import AutoClassification

classification = AutoClassification(path="processed.csv", filetype="csv", target_column="target_column")
result = classification.train_model()
print(result)

```

### Models Available 

- Logistic Regression
- KNN 
- Naive Bayes
- Decision Tree
- Random Forest
- Gradiant Boosting
- ADA Boost

### Output Parameters

- best_model_name
- model
- model_params
- accuracy
- precision
- recall
- f1_score

### Save and Use Trained Model

```bash

import joblib 
import numpy as np
import pandas as pd 
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score

## Store trained model to local system
model = result.get("model")
joblib.dump(model, "model.pkl")

## Load model
model = joblib.load("model.pkl")

## Import data and predict
df = pd.read_csv("processed.csv")
X = df.drop(columns=['target_column'])
y = df["target_column"]

y_pred = model.predict(X)

## Evaluate model 
print("accuracy score : ", accuracy_score(y_pred, y))
print("precision score : ", precision_score(y_pred, y))
print("recall score : ", recall_score(y_pred, y))
print("f1 score : ", f1_score(y_pred, y))
```


## 🤝 Contributing

**Contributions are welcome! If you'd like to improve the code, add features, or fix bugs, please follow the steps below:**

1. Fork the repository.  
2. Create a new branch: git checkout -b feature-name  
3. Make your changes.  
4. Test your changes.   
5. Commit and push: git commit -m 'Add some feature' && git push origin feature-name  
6. Create a Pull Request.  

### Guidelines

- Follow PEP8 coding style.
- Write meaningful commit messages.
- Add docstrings and comments where necessary.

**If you add a new model or preprocessor, please update the documentation.**

### Issues & Discussions
- Use the GitHub Issues to report bugs or suggest features.
- You can also start a discussion if you're unsure about a change.

## 📄 License

This project is licensed under the MIT License – see the LICENSE file for details.