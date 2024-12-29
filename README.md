# Predicting-Online-News-Popularity

. PREDICTING ONLINE NEWS POPULARITY
1) Data Selection: The dataset is 58 feature items describing attributes of 39644 online news articles from Mashable
that predict the number of shares as the popularity measure.
The shares is associated with the popularity of article i.e
the social media engagement for it. The reasons why this
dataset is so useful for these tasks is this dataset’s highly
multivariate, highly diverse nature — it’s ideal for regression
and classification to discover what the key drivers of article
popularity are and how you can optimize content strategy to
impact.
2) Data Preprocessing: Visualizations of article categories
and their average shares make for interesting trends on how
content is engaged. The Tech channel is by far the most
popular category, with the highest average shares, with the
World and Entertainment channels being right behind. Articles
get the least number of average shares on weekends when
compared to weekends or perhaps signify low engagement of
the audience when is analyzed when the days and average
shares is visualized. A regplot is depicted which provide the
ability to visualize the relationship between the number of
shares and sentiment features by creating scatterplots as in
Fig.1.
Fig. 4. Analyzing Sentiment features and shares
3) Data Transformation:
• Correlation Matrix and Feature Importance A correlation
matrix was calculated, showing the relationship between
the features and the target variable, shares. The generated
heatmap of the matrix showed features that were highly
correlated with shares. The correlation values were sorted
in descending order to focus on the most influential
predictors. This will give insight into the variables most
likely to influence the target outcome.
• Feature Reduction The redundancy of the features and
their low variance were addressed:
Low-Variance Features: VarianceThreshold identified features with variance below 0.01 and dropped them since
such columns contribute little to predictive models.
Highly Correlated Features: Pairs of features were identified with a correlation coefficient greater than 0.9, and
one feature from each highly correlated pair was dropped
to reduce multicollinearity.
• Outlier and Skewness Detection The following steps were
taken in identifying and handling outliers and skewed
distributions:
Skewness Detection: Features with skewness more than
±1 were considered highly skewed. Outlier Detection:
IQR was used to identify outliers, and their respective
counts were recorded. The capping strategy was implemented through the clipping of values outside the bounds
defined by IQR. Skewness Handling: Log transformations
were performed on columns that had strong skewness,
normalizing distributions for better model performance.
• Feature Aggregation and Logical Grouping In order to
simplify the dataset and reduce dimensionality, related
features were logically aggregated. For example:
Weekday and Weekend Features: Seven columns for days
of the week were combined into total weekdays (sum of
Monday to Friday indicators) and is weekend (sum of
Saturday and Sunday indicators), reducing seven columns
to two.
Keyword Features: Eight keyword-related columns were
averaged into one column, kw min max avg. Topic Features (LDA): Five topic likelihood columns (LDA 00 to
LDA 04) were averaged into lda topic avg, summarizing
topic analysis in a single feature. Sentiment Features:
Sentiment polarity and subjectivity were binarized based
on thresholds to indicate positive sentiment and subjectivity, respectively. The original columns were then dropped.
• Target Transformation The distribution of the values in
the column ’shares’ was highly skewed. In order to
normalize it, a log transformation (log1p) was performed
and the transformed column, ’shares log’, became the
main target variable for predictive analysis.
• Feature Scaling StandardScaler was used to scale all the
numerical features of the dataset except for the target
column. This would normalize the features to have a
mean of 0 and a standard deviation of 1, thus preventing
features with large numeric ranges from dominating the
model.
• Dimensionality Reduction Using PCA The PCA transformation resulted in new components, which replaced the
original features. Each components’ explained variance
was examined, confirming the effectiveness of PCA in retaining critical information while simplifying the dataset.
• Final Prepared Dataset The final dataset consisted of PCA
components as features and the log-transformed shares
column as the target variable. The preprocessed dataset
was now ready for predictive modeling, providing a balanced, normalized, and simplified structure yet retaining
the essential information required for analysis.
4) Data Mining:
• Data Splitting The dataset was split into training and
testing set using train test split function from Scikitlearn. I chose an 80-20 split where I used 80% for training
and 20% for testing the models. Fixed the random state
to ensure the data split generated between runs was
reproducible.
• Hyperparameter Tuning Hyperparameter tuning was performed to maximize model performance by using GridSearchCV, a method which exhaustively tests hyperparameter combination for a given model. A dictionary
(model params) was created to define the models and
their corresponding hyperparameter grids:
Random Forest Regressor (rf): The hyperparameter
n estimators, the number of trees in the forest, was the
key one tuned. Numbers were tested with various values
until the best number was found. K-Nearest Neighbors
Regressor (knn): In this case the number of neighbors
to consider when predicting a data point were controlled using the n neighbors parameter. Decision Tree
Regressor (dt): The value of max depth was tuned to
stop the decision tree from becoming too complex thus
preventing overfitting. We evaluated these models using
cross validation (5 fold) to pick the best hyperparameter
combination. Based on the results, the optimal parameters
were found to be:
Random Forest: n estimators = 45 K-Nearest Neighbors:
n neighbors = 15 Decision Tree: max depth = 10
• Model Training After finishing the tuning, the models
were trained using the best hyper parameters found during
the tuning. For each model, training data (x train, y train)
is used to fit. Regression tasks are an essential evaluation
metric since it provides a clear indication of how well
explained the model is for data that we have not seen.
Linear Regression : It is used to supply a baseline model,
trained to contrast the performance of more elaborate
models.
Random Forest Regressor : Used with n estimators = 45
and shallow depth (max depth = 2) so that it don’t overfit.
Decision Tree Regressor : Max depth = 10 is trained to
make sure it captures the right complexity but not over
fitting.
K-Nearest Neighbors Regressor : We set with tag to take
an optimal number of nearest neighbors with n neighbors
= 15.
AdaBoost Regressor : A boosting ensemble method of
weak learners.
Gradient Boosting Regressor: A single method that advances strong predictive models by iteratively combining
strong weak learners.
XGBoost Regressor : A highly optimized gradient boosting model which often performs much better than other
models on structured data.
