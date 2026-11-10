<!-- Dorian Nowacki | C00288163 -->
# Portfolio Presentation Guide — Used-Car Price Analysis

**Student:** Dorian Nowacki | **ID:** C00288163

Use these notes to practise explaining the code, not as a substitute for independently understanding it. Numbers are approximate values from the verified run; Jupyter calculates the authoritative current results.

## Suggested 5–7 minute walkthrough

**1. The question (30–45 seconds).** I analysed a file of 30,824 used-car listings to find what is related to price, predict prices, classify prices into two bands, and group vehicles without labels.

**2. Preparing the data (45–60 seconds).** The file has 26 columns. I removed 36 duplicate records and 8 listings below $100 as potentially nonrepresentative placeholder prices; this left 30,780 records. There were 8 missing values in engine capacity. For supervised models, missing values were filled by a median fitted on the *training* set only. This matters because fitting preprocessing on test data introduces leakage.

**3. Exploration (45–60 seconds).** I plotted price distributions, price against model year and odometer, manufacturers' average listed prices and numeric correlations. Newer listings typically have higher prices, higher-mileage vehicles tend to cost less, and the price distribution is right-skewed. These are associations, not proof of causality.

**4. Predicting a numerical price (60 seconds).** Linear Regression fits a linear combination of the input features. Random Forest averages predictions from many decision trees, capturing non-linear patterns. Both use the same 80/20 split and features, with one-hot encoding for text categories. Results: Linear Regression R² ~0.797, MAE ~$1,741; Random Forest R² ~0.898, MAE ~$1,154, so Random Forest is better on this test set.

**5. Classifying prices (60 seconds).** Logistic Regression predicts whether a listing is *below $15,000* or *at least $15,000*. It outputs a probability and predicts class 1 when that probability passes the default 0.5 cutoff. The $15k boundary defines the target and is not the same thing as the probability cutoff. The high-price group contains only ~9% of listings: a model predicting all cars as below $15k would already get ~91% accuracy. My model gets ~97% accuracy, ROC AUC ~0.988 and class-1 F1 ~0.835; I also evaluate precision, recall and the confusion matrix to account for class imbalance.

**6. Discovering car groups (60 seconds).** K-Means is unsupervised. It groups listings by production year, mileage and engine capacity, **not by price**. I standardised the inputs so mileage does not dominate the distance calculation. I tested 2–6 clusters and chose 3 based on the highest sampled silhouette score (~0.384). The groups differ in year, mileage, engine capacity and median listed price; this is descriptive and exploratory.

**7. Conclusions (30–45 seconds).** Different methods answer different questions. Random Forest performed best at numerical prediction; Logistic Regression separated the two price bands well on the tested data; K-Means found useful groupings. The dataset represents listings rather than confirmed sale prices, and results would need further validation before real-world use.

## Questions the lecturer may ask

**Why is Logistic Regression called regression if it classifies?** It uses a linear combination of inputs inside a logistic function to estimate the probability of a class; the task is classification, not prediction of a continuous price.

**What is a pipeline?** A sequence that fits preprocessing and then the estimator. It makes it easier to reproduce training and ensures transforms learned from the training split are applied consistently to test data.

**Why one-hot encoding?** Text labels like manufacturer and fuel type are categories, not continuous numeric measurements. One-hot encoding creates binary indicator columns without assigning an artificial order.

**Why not evaluate Logistic Regression with R²?** R² is designed for numerical regression targets. Classification evaluation uses confusion matrices, precision, recall, F1, ROC AUC and related metrics.

**Why stratify the classification split?** Only ~9% are in the $15k+ class. Stratification helps keep the class proportions similar in training and test partitions.

**Why is 97% accuracy not the whole story?** Always predicting the much larger class would already be ~91% accurate. We need class-1 recall and precision to evaluate whether the minority cases are recognised.

**What does an F1-score of 0.835 mean?** It is the harmonic mean of precision and recall for the selected class; it summarises both kinds of performance and is more informative than accuracy when classes are imbalanced.

**How did you choose k?** I compared candidate values 2 through 6 using a silhouette score on a reproducible sample of 1,500 records and inspected inertia. k=3 scored highest among those tested; this is a heuristic, not an objectively correct number of natural groups.

**Why was price excluded from K-Means inputs?** I wanted groups based on car features and then to examine whether their listed prices differ. If price had been included, price differences between clusters would partly be built into the grouping.

**What would you improve next?** Cross-validation and sensitivity analysis for supervised models; more careful identification of suspicious listings; class-threshold experiments; tuning with validation data; evaluating clusters' stability.

**Can we trust the dataset source?** The CSV is supplied within the project. A publicly listed Kaggle dataset appears to match the schema, but the exact original download provenance still needs confirmation. Do not claim a verified source you have not checked.

## Definitions to know

- **MAE:** average absolute difference between actual and predicted dollar prices. Lower is better.
- **RMSE:** square root of average squared prediction error; penalises large misses more than MAE.
- **R²:** how much better the predictions are at explaining test-set variation than predicting a constant test-set average.
- **Precision (class 1):** of listings predicted to be $15k+, the proportion actually in that class.
- **Recall (class 1):** of all listings actually $15k+, the proportion the model found.
- **ROC AUC:** how well the classifier generally ranks higher-priced listings over lower-priced listings across probability thresholds.
- **Silhouette:** separation between clusters relative to within-cluster cohesion, usually between -1 and 1; higher is generally better.
- **Inertia:** sum of squared distances to K-Means cluster centres. It always tends to fall as k rises, so minimising it by itself favours too many clusters.

**Final preparation:** Open the actual notebook, run all cells, and practise explaining the plotted outputs, data columns and code lines without reading this guide verbatim.
