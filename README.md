
Deep vs Wide Neural Networks on Tabular Data
This repository presents a research-based comparison of Artificial Neural Network (ANN) architectures to solve a real-world environmental classification problem:

Does increasing depth or width improve performance in tabular data?

Using the Forest Cover Type dataset (581K samples), we compare:

🔵 Deep Network (10 layers)

🟢 Wide Network (2 layers)

Key Highlights
 Large-scale dataset (581,012 samples, 54 features)

 Severe class imbalance (103:1 ratio) handled with class weights

 Deep vs Wide ANN comparison

 Deep model suffers from gradient issues

 Wide model outperforms by +16.8% accuracy

 Model explainability using SHAP

 Dataset: Forest Cover Type
Samples: 581,012

Features: 54

10 continuous (Elevation, Slope, etc.)

44 binary (Soil & Wilderness types)

Target: 7 forest cover classes

Class Imbalance
Majority class: 48.8%

Minority class: 0.5%

Ratio: 103:1

 Solution: Class Weights (not SMOTE)

Model Architectures
Model	Layers	Neurons	Technique
Deep ANN	10	64 each	BatchNorm + Dropout
Wide ANN	2	512 each	Dropout
Training Configuration
Optimizer: Adam

Loss: Categorical Crossentropy

Batch Size: 512

Epochs: 30

Early Stopping (patience=5)

Class Weights: Balanced

Results
Metric	Deep ANN	Wide ANN
Accuracy	70.76%	87.53%
Macro F1-Score	0.60	0.81
Weighted F1-Score	0.72	0.88
Inference Time	7.84s	6.05s
Key Insights
1. Width > Depth (for Tabular Data)
Wide network outperforms by +16.8%

Learns better feature representations

2. Deep Networks Struggle
Gradient instability without BatchNorm

Slow convergence

Poor majority class prediction

3. Wide Network is Faster
Fewer sequential operations

Better parallelization

Handling Class Imbalance
Instead of SMOTE:

✔ Used Class Weights
✔ More efficient for large datasets
✔ Achieved strong minority recall (~0.97–1.00)

🔍 Model Explainability (SHAP)
We use SHAP (SHapley Additive Explanations) to interpret predictions.

Key Findings:
Elevation is the most important feature

Distance to roads & fire points also important

Model aligns with real ecological patterns

This confirms the model learned meaningful relationships, not noise.

 Model Behavior
✔️ Confusion Matrix
Deep → struggles with major classes

Wide → balanced performance across all classes

✔️ Learning Curves
Deep → slow, unstable learning

Wide → fast convergence

 Key Learnings
Tabular data prefers wide architectures

Deep models require BatchNorm

Class weights scale better than SMOTE for big data

Model interpretability is essential (use SHAP)

🧪 Tech Stack
Python

TensorFlow / Keras

Scikit-learn

NumPy / Pandas

SHAP

Matplotlib

How to Run
git clone https://github.com/your-repo-link
cd ANN_Covertype
pip install -r requirements.txt
jupyter notebook
 Future Work
Try XGBoost / LightGBM (strong for tabular data)

Experiment with TabNet / TabTransformer

Hyperparameter tuning

Deploy as ML API

 Ethical Considerations
🌍 Impacts environmental decision-making

⚖️ Misclassification may affect conservation

🔍 Transparency required for trust

Conclusion
Architecture matters more than size

Wide ANN → Best performance & efficiency

Deep ANN → Requires careful design (BatchNorm)

 Recommendation:

Start with wide models for tabular data, add depth only if necessary.
