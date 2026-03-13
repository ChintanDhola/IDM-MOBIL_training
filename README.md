# Driving Behavior Analysis & TTC Prediction using Deep Learning

This project analyzes naturalistic highway traffic data to classify driving behavior and predict Time-to-Collision (TTC) using supervised deep learning techniques.

The workflow follows a structured pipeline including data preprocessing, feature engineering, exploratory analysis, modeling, evaluation, and visualization.

## Project Structure

```text
├── data/                  # Raw highD CSV files (not uploaded due to size)
├── models/                # Saved trained Keras models for behavior classification
│   ├── aggr_model.h5      # Model for aggressive driving style
│   ├── def_model.h5       # Model for defensive driving style
│   └── norm_model.h5      # Model for normal driving style
├── Prjt1.py               # Data preprocessing, feature engineering & evaluation metrics
├── Prjt2.py               # Deep learning modeling (classification & regression)
├── IDM +MOBIL.ipynb       # Parameter tuning, risk score & deterministic traffic simulation 
├── feature_matrix.csv     # Aggregated vehicle-level features (e.g., df_behave.csv)
└── README.md              # Project documentation


## Dataset

**Dataset:** highD Dataset  
**Source:** Drone-based highway traffic recordings  
**Data type:** Vehicle trajectories and driving dynamics  

**Key parameters used:**

- DHW (Distance Headway)  
- TTC (Time-to-Collision)  
- yVelocity (Lateral velocity)  

## Project Workflow

### 1. Data Preparation (Prjt1.py)

- Cleaning raw CSV files  
- Handling missing values  
- Interpolation of time-series data  
- Normalization of units  
- Vehicle-level aggregation  
- Validation of data consistency  

### 2. Feature Engineering & Exploratory Analysis (Prjt1.py)

- Statistical features: mean, standard deviation  
- Dynamic features: gradients, temporal variations  

**Behavioral labeling:**

- Defensive  
- Normal  
- Aggressive  

**Visualizations:**

- Heatmaps  
- Correlation matrices  
- Distribution plots  

### 3. Feature Matrix Creation (Prjt1.py)

- Aggregated vehicle-level features  
- Final dataset for model training  
- Exported as feature_matrix.csv  

### 4. Deep Learning Modeling (Prjt2.py)

**Classification**

- Task: Driving behavior classification  
- Classes: Defensive, Normal, Aggressive  
- Loss function: Categorical Cross-Entropy  

**Regression**

- Task: TTC prediction  
- Loss function: Mean Squared Error (MSE)  

### 5. Model Training & Optimization
Part A: Deep Learning Training (Prjt2.py / Prjt2.ipynb)

Behavior-Specific Models: The neural networks are trained separately for distinct driving styles, resulting in dedicated Keras models saved in the /models directory (aggr_model.h5, def_model.h5, norm_model.h5).

Training Process: 80/20 train-test split with multi-epoch training.

Monitoring: Tracking training accuracy, validation accuracy, training loss (Categorical Cross-Entropy for behavior), and validation loss (MSE for TTC regression).

Part B: IDM + MOBIL Parameter Tuning (IDM +MOBIL.ipynb)

Behavioral Calibration: Adjusting the deterministic Intelligent Driver Model (IDM) parameters (target speed v0, time gap T, acceleration a, and comfortable deceleration b) dynamically based on the predicted driving style (Defensive, Normal, Aggressive).

MOBIL Safety Thresholding: Establishing the safe braking limit (b_safe = 10.0 m/s²) for lane-changing and cut-in scenarios based on naturalistic HighD trajectories.

Risk Score Aggregation: Calculating a hybrid Risk Score utilizing Inverse TTC, Distance Headway (DHW), and relative lateral velocity to define strict, physics-based safety boundaries (e.g., critical TTC < 1.5s) for crash prevention.

### 6. Model Evaluation (Prjt1.py)

**Classification metrics:**

- Accuracy  
- Precision  
- Recall  
- F1-score (manual multi-class implementation)  

**Regression metrics:**

- Mean Squared Error (MSE)  
- Root Mean Squared Error (RMSE)  
- Mean Relative Error (MRE)  
- Standard deviation of errors  
- Correlation between predicted and true TTC  

### 7. Visualization

- Regression scatter plots (predicted vs actual TTC)  
- Learning curves  
- Heatmaps for risk analysis  
- Confusion matrix interpretation  

**Example Visualization:**
python
plt.scatter(distance, lateral_velocity, c=minTTC, cmap=cm.RdYlGn) ```

Crash-critical scenarios are highlighted for safety analysis.

Key Findings

Low TTC combined with small headway indicates aggressive driving

Deep learning models outperform rule-based baselines

TTC prediction correlates strongly with real collision risk

Balanced Precision–Recall performance is crucial for safety-critical detection

Requirements

Python >= 3.8

numpy

pandas

matplotlib

seaborn

tensorflow

keras

Note: scikit-learn is optional and not required for core functionality.

How to Run
# Step 1: Feature engineering & evaluation
python Prjt1.py

# Step 2: Model training
python Prjt2.py

Future Work

Integration of additional traffic parameters

Cross-dataset validation

Scenario-based risk modeling

Real-time driving behavior detection

References

highD Dataset (Krajewski et al.)

Deep Learning (Goodfellow et al.)

Traffic Flow Dynamics (Treiber & Kesting)

Author

Khan,Mohammad Ahmad
Dhola, Chintankumar Jayantibhai 
Chauhan, Kartik 
Informatik Project – Driving Behavior Analysis & AI Modeling


