# Predicting Patient Length of Stay (LOS) for Efficient Hospital Management
---
# Problem Statement

Predicting a patient’s **length of stay (LOS)** at admission is critical for effective hospital management. Without reliable forecasts, hospitals face cascading inefficiencies that go far beyond mismatches in **staffing, bed turnover, and resource allocation**, ultimately undermining both care quality and financial stability.  

Without accurate LOS predictions, hospitals experience **systemic inefficiencies** that extend well beyond issues of staffing, bed turnover, and resource allocation, ultimately undermining both care quality and financial stability. 

Uncertainty in LOS contributes to **drug shortages or costly overstocking**, which increases pharmacy expenditures, while also disrupting supply chains for consumables such as diagnostic kits, intravenous fluids, and other logistics. This results in either waste from oversupply or treatment delays from under-supply. Inadequate LOS planning further produces **bottlenecks in discharge and admissions**, leading to overcrowding, prolonged waiting times, and patient dissatisfaction that damages hospital reputation and reduces retention.  

Prolonged or unanticipated stays also impose **opportunity costs**, as high-value beds remain occupied instead of being used for revenue-generating admissions, particularly elective procedures. Collectively, these inefficiencies elevate the risk of **hospital-acquired infections, insurance penalties, and legal claims**, compounding the financial burden faced by hospitals.  

This project addresses these challenges by developing **statistical and machine learning models** to predict LOS at admission, enabling data-driven operational and policy improvements.  

---

## Objectives

This study has four primary objectives:

1. **Statistical characterization of LOS predictors**  
The first stage of the analysis consists of performing exploratory data analysis (EDA) in order to summarize the distribution of length of stay (LOS), identify underlying patterns, and detect potential anomalies within the dataset. Since LOS is recorded in discrete units of whole days, it was modeled as a count variable rather than as a continuous outcome. To examine the association between predictor variables and LOS, statistical models suitable for count outcomes were applied. Poisson regression was initially considered, as it is the standard approach for modeling count data and assumes equality of the mean and variance. However, because LOS data in hospital settings frequently exhibit overdispersion, where the variance exceeds the mean, Negative Binomial regression was employed as a more appropriate alternative. In addition, in situations where a substantial proportion of patients experienced very short or zero-day stays, zero-inflated models were considered in order to account for the excess zeros in the distribution. To prevent overfitting and improve model interpretability, feature selection methods such as Least Absolute Shrinkage and Selection Operator (LASSO) and Elastic Net regularization were used to identify the most relevant predictors. Finally, model-independent interpretability techniques, such as SHapley Additive exPlanations (SHAP) values, were used to show how much each predictor contributed to the prediction of length of stay.

2. **Development and validation of predictive machine learning models**  
Following the statistical characterization of length of stay (LOS), a set of supervised machine learning algorithms was developed to better capture the complex and often nonlinear relationships between predictor variables and LOS. Healthcare data are generally structured in tabular form and often involve complex interactions and nonlinear effects among variables, which cannot always be adequately captured by traditional linear models. Random Forests and Gradient Boosting Machines (including XGBoost) were employed because they are well-suited to high-dimensional clinical datasets, can handle high-dimensional data effectively, manage missing values, and can model nonlinear relationships while also indicating which variables contribute most strongly to LOS prediction. Each model was trained and validated using k-fold cross-validation procedures and an independent hold-out set to minimize overfitting and to ensure that performance would generalize to unseen data. Model performance was evaluated using metrics appropriate to the nature of the prediction task. For continuous LOS prediction, metrics such as Root Mean Squared Error (RMSE), Mean Absolute Error (MAE), and the coefficient of determination (R²) were applied, as these quantify both the magnitude of prediction error and the proportion of variance explained by the model. While LOS was primarily modeled as a continuous outcome, the framework also accommodated categorical prediction (e.g., short, medium, or long stays), for which classification metrics such as the Area Under the Receiver Operating Characteristic curve (AUROC) and F1-score were used to assess discriminatory power and the balance between sensitivity and specificity. In addition, calibration analyses were conducted to verify that predicted values aligned with observed outcomes, which is particularly important when outputs are intended to support clinical or operational decision-making.Finally, subgroup analyses were performed to examine fairness and to test whether model performance was consistent across patient populations defined by demographic and clinical characteristics such as age, sex, and insurance status. This step ensured that the models did not systematically favor or disadvantage specific groups, an essential requirement for ethical application in public health and healthcare resource allocation.

3. **Derivation of operational insights and policy implications**  
The next phase of the project focused on comparing machine learning models and identifying those that provided the most accurate predictions of length of stay (LOS). Model outputs were evaluated using performance metrics such as RMSE, MAE, and R² to determine their reliability and generalizability. While the current implementation is limited to assessing predictive accuracy, the broader aim of the project is to translate LOS predictions into actionable strategies for hospital operations and policy development. In practice, accurate LOS predictions could be used to inform staff scheduling, bed allocation, supply chain management of consumables, and discharge planning. Such models could also support the early identification of patients at elevated risk of prolonged stays, enabling timely interventions that improve efficiency and outcomes. Future extensions of this framework will incorporate scenario analyses to quantify benefits such as reduced unnecessary expenditures, decreased incidence of hospital-acquired infections, improved patient throughput, and enhanced utilization of healthcare resources. These insights would ultimately provide guidance for policy recommendations aimed at strengthening operational efficiency, reducing financial losses, and improving the overall quality of hospital management.

4. **Deployment readiness and integration**  
In the final stage, the best-performing models were prepared for deployment in real-world hospital environments. Serialization techniques such as pickle and joblib were applied to store trained models in formats suitable for integration into hospital information systems, thereby enabling automated LOS prediction at the time of admission. To enhance transparency and build trust among clinical and administrative stakeholders, explainability was incorporated using SHapley Additive exPlanations (SHAP), which makes model predictions interpretable by showing how much each variable (like age, comorbidities, admission type) contributed to the predicted LOS. While the current implementation includes SHAP, future enhancements may incorporate Local Interpretable Model-Agnostic Explanations (LIME) to provide additional, patient-level explanations in simpler terms. Similarly, prediction intervals may be added to present a range of likely LOS values (for example, 5–10 days) instead of a single number, giving decision-makers greater clarity about uncertainty and enabling more risk-sensitive planning. This deployment-oriented approach ensures that the models are not only technically robust but also practical, interpretable, and adaptable to the dynamic requirements of hospital operations.

---

## Approach

The project was implemented in six sequential stages:

1. **Data Collection and Preprocessing**  
Electronic health record (EHR) and administrative datasets were assembled, incorporating demographic, clinical, and admission-related variables. Missing values were imputed, outliers were examined, and categorical features were encoded to prepare the dataset for analysis.

2. **Statistical Modeling**  
Baseline models were constructed using generalized linear and count-data approaches (Poisson, Negative Binomial, and zero-inflated variants) to establish statistical associations between predictors and LOS. Feature selection methods such as LASSO and Elastic Net were applied to improve interpretability and reduce overfitting.

3. **Machine Learning Development**  
Supervised machine learning models, including Random Forests, Gradient Boosting, and XGBoost, were trained and optimized using hyperparameter tuning techniques such as grid search and randomized search. Model performance was evaluated using regression metrics (RMSE, MAE, R²) for continuous outcomes. While the implemented analysis treated LOS as a continuous variable, the framework was designed to be extendable to categorical prediction.

4. **Model Explainability and Fairness**  
Explainability techniques were incorporated using SHapley Additive exPlanations (SHAP) to quantify the contribution of predictors to LOS predictions. Fairness was considered by outlining subgroup analyses across patient demographics. Calibration was examined to ensure that predicted values were consistent with observed outcomes.

5. **Deployment and Evaluation**  
The best-performing models were serialized using pickle and joblib for integration into hospital information systems. Provisions for prototype dashboards were considered to demonstrate real-time LOS prediction. While scenario-based simulations were not implemented in the notebooks, the framework was designed to allow evaluation of operational impacts such as bed turnover, consumable utilization, and prolonged stays.

6. **Monitoring and Continuous Learning**  
Post-deployment monitoring was outlined, whereby predicted values would be compared with observed LOS to assess accuracy. Feedback mechanisms were proposed to enable model retraining and recalibration as new data become available, ensuring stability and adaptability to dynamic hospital contexts.

---


