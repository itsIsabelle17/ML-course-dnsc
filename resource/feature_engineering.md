Problem | Symptoms | Solution
--- | --- | ---
**[Incomplete data](https://github.com/jphall663/GWU_ML/blob/main/resource/feature_engeering.md#incomplete-data)** | Useless models and meaningless results. | Get more data. Get better data. [Design of Experiment](https://en.wikipedia.org/wiki/Design_of_experiments) approaches.
**[Biased Data](https://github.com/jphall663/GWU_ML/blob/main/resource/feature_engeering.md#biased-data)** | Biased models and biased, inaccurate results. | Get more data. Get better data. [Design of Experiment](https://en.wikipedia.org/wiki/Design_of_experiments) approaches.
**Wide Data** | Long, intolerable compute times. Meaningless results due to curse of dimensionality. | [Feature selection](https://github.com/jphall663/GWU_ML/blob/main/resource/feature_engeering.md#feature-selection---view-notebook). [Feature extraction](https://github.com/jphall663/GWU_ML/blob/main/resource/feature_engeering.md#feature-extraction---view-notebook). L1 Regularization.
**Sparse data<sup>&#10013;</sup>** | Long, intolerable compute times. Meaningless results due to curse of dimensionality. | [Feature extraction](https://github.com/jphall663/GWU_ML/blob/main/resource/feature_engeering.md#feature-extraction---view-notebook). Appropriate data representation, i.e. COO, CSR. Appropriate algorithm selection, e.g. factorization  machines.
**Imbalanced Target Variable** | Single class model predictions. Biased model predictions. | [Proportional over- and under-sampling](https://github.com/jphall663/GWU_ML/blob/main/resource/feature_engeering.md#over--and-under-sampling---view-notebook). Inverse prior probability weighting. Mixture models, e.g. zero-inflated regression methods.
**Outliers** | Biased models and biased, inaccurate results. Unstable parameter estimates and rule generation. Unreliable out-of-domain predictions. | [Discretization](https://github.com/jphall663/GWU_ML/blob/main/resource/feature_engeering.md#discretization---view-notebook). [Winsorizing](https://github.com/jphall663/GWU_ML/blob/main/resource/feature_engeering.md#winsorizing---view-notebook). Appropriate algorithm selection, e.g. Huber loss functions.
**Missing Values** | Information loss. Biased models and biased, inaccurate results. | [Imputation](https://github.com/jphall663/GWU_ML/blob/main/resource/feature_engeering.md#imputation---view-notebook). [Discretization](https://github.com/jphall663/GWU_ML/blob/main/resource/feature_engeering.md#discretization---view-notebook). Appropriate algorithm selection, e.g. Tree-based models, naive Bayes classification.
**Character Variables<sup>&#10013;</sup>** | Information loss. Biased models and biased, inaccurate results. Computational errors. | [Encoding](https://github.com/jphall663/GWU_ML/blob/main/resource/feature_engeering.md#encoding---view-notebook). Appropriate algorithm selection, e.g. Tree-based models, naive Bayes classification.
**High Cardinality Categorical Variables** | Over-fit models and inaccurate results. Long, intolerable compute times. Unreliable out-of-domain predictions. | [Target Encoding (categorical)](https://github.com/jphall663/GWU_ML/blob/main/resource/feature_engeering.md#target-encoding-categorical---view-notebook) or variants e.g. perturbed rate-by-level or [Weight of Evidence](http://support.sas.com/documentation/cdl/en/prochp/66409/HTML/default/viewer.htm#prochp_hpbin_details02.htm). [Target Encoding (numeric)](https://github.com/jphall663/GWU_ML/blob/main/resource/feature_engeering.md#target-encoding-numeric---view-notebook) or variants average-, median, BLUP-by-level. [Discretization](https://github.com/jphall663/GWU_ML/blob/main/resource/feature_engeering.md#discretization---view-notebook). Embedding approaches, e.g. entity embedding neural networks, factorization machines.
**Disparate Variable Scales** | Unreliable parameter estimates, biased models, and biased, inaccurate results. | [Standardization](https://github.com/jphall663/GWU_ML/blob/main/resource/feature_engeering.md#standardization---view-notebook), Appropriate algorithm selection, e.g. Tree-based models.
**Strong Multicollinearity (correlation)** | Unstable parameter estimates, unstable rule generation, and unstable predictions. | [Feature selection](https://github.com/jphall663/GWU_ML/blob/main/resource/feature_engeering.md#feature-selection---view-notebook). [Feature extraction](https://github.com/jphall663/GWU_ML/blob/main/resource/feature_engeering.md#feature-extraction---view-notebook). L2 Regularization.
**Dirty Data** | Information loss. Biased models and biased, inaccurate results. Long, intolerable compute times. Unstable parameter estimates and rule generation. Unreliable out-of-domain predictions. | Combination of solution strategies.

<sup>&#10013;</sup> In some cases this is not a problem at all. Some algorithms and software packages handle this automatically and elegantly ... some don't.

#### Incomplete data
When a data set simply does not contain information about the phenomenon of interest. There is no analytical remedy for incomplete data. You must collect more and better data, and probably dispose of the original incomplete set.

#### Biased data
When a data set contains information about the phenomenon of interest, but that information is consistently and systematically wrong. There is no analytical remedy for biased data. You must collect more and better data, and probably dispose of the original biased set.

#### Feature selection - [view notebook](https://drive.google.com/file/d/1goBhzXLqjagd8EDyvQwgAtOYBIykIIr_/view?usp=sharing)
Finding the best subset of original variables from a data set, typically by measuring the original variable's relationship to the target variable and taking the subset of original variables with the strongest relationships with the target. Feature selection decreases the impact of the curse of dimensionality and usually increases the signal-to-noise ratio in a data set, resulting in faster training times and more accurate models. Because feature selection uses original variables from a data set, its results are usually more interpretable than feature extraction techniques.

#### Feature extraction - [view notebook](https://drive.google.com/file/d/1e_-015Zfx5sRdWXPR_6qFAC70rJuxFup/view?usp=sharing)
Combining the original variables in a data set into a new, smaller set of more representative variables, very often using unsupervised learning methods. Feature extraction may also be referred to as 'dimension reduction'. Feature extraction is the unsupervised analog of feature selection, i.e. it tends to decreases the impact of the curse of dimensionality and usually increases the signal-to-noise ratio in a data set. Feature extraction techniques combine the original variables in the data set in complex ways, usually creating uninterpretable new variables.

#### Over- and under-sampling - [view notebook](https://drive.google.com/file/d/1fhat_dZhhqjAtPs2IJ5USA9wTVP5dJ2e/view?usp=sharing)
Taking all the rows containing rare events in a data set and increasing them proportionally to the number of rows not containing rare values. 'Undersampling' is the opposite and equally valid approach where the rows not containing rare events are decreased proportionally to the number of rows containing rare events. With rare events, models will often find that the most accurate possible outcome is to predict the rare event never happens. Both oversampling and undersampling artificially inflate the frequency of rare events, which helps models learn to predict rare events. Unfortunately, over- and under-sampling tends to result in over-prediction of rare events, a bias that must be addressed before deployment. 

#### Encoding - [view notebook](https://drive.google.com/file/d/16anwAZt38Sr8j7Tl1gSSjBgV_e5bs8HA/view?usp=sharing)
Changing the representation of a variable. Very often in data mining applications categorical, character variables are encoded to numeric variables to be used with algorithms that cannot accept character or categorical variables.

#### Target Encoding (Categorical) - [view notebook](https://drive.google.com/file/d/1HgBWhmryQwHtReaweoZdlJGMwtdqtu_M/view?usp=sharing)
An encoding method for changing categorical variables into numeric variables when the target is a binary categorical variable. Particularly helpful when a categorical variable has many levels.

#### Target Encoding (Numeric) - [view notebook](https://drive.google.com/file/d/1Dg0YP1tgFs_ILMTLN6NywX-MP7vEOYPF/view?usp=sharing)
An encoding method for changing categorical variables into numeric variables when the target is a numeric variable. Particularly helpful when a categorical variable has many levels.

#### Discretization - [view notebook](https://drive.google.com/file/d/1jSq65mivctrmu91rps3GoggLwoHoUM5P/view?usp=sharing)
Changing a numeric variable into an ordinal or nominal categorical variable based on value ranges of the original numeric variable. Discretization can also be referred to as 'binning'. Discretization has many benefits:
* When restricted to using linear models, binning helps introduce nonlinearity because each bin in a variable gets its own parameter.
* Binning smoothes complex signals in training data, often decreasing overfitting.
* Binning deals with missing values elegantly by assigning them to their own bin.
* Binning handles outliers elegantly by assigning all outlying values, in training and new data, to the 'high' or 'low' bin. (Outliers damage predictive models that seek to minimize squared error because they create disproportionately large, i.e. squared, residuals which optimization routines will try to minimize at the expense of minimizing the error for more reliable data points.)

#### Winsorizing - [view notebook](https://drive.google.com/file/d/1SmGe_k1s0aRrzvP6mb4a7k8lbXoWEJg2/view?usp=sharing)
Removing outliers in a variable's value and replacing them with more central values of that variable. (Outliers damage predictive models that seek to minimize squared error because they create disproportionately large, i.e. squared, residuals which optimization routines will try to minimize at the expense of minimizing the error for more reliable data points.)

#### Imputation - [view notebook](https://drive.google.com/file/d/1F57RnBa7x9fm_K9eEOaYEJqmyjrwA_Jq/view?usp=sharing)
Replacing missing data with an appropriate, non-missing value. In predictive modeling imputing should be used with care. Missingness is often predictive. Also imputation changes the distribution of the input variable learned by the model.

#### Standardization - [view notebook](https://drive.google.com/file/d/16uBhnFgU3NLO_hcAAGhF1e9TcsFq1lIe/view?usp=sharing)
Enforcing similar scales on a set of variables. For distance-based algorithms (e.g. k-means) and algorithms that use gradient-related methods to create model parameters (e.g. regression, artificial neural networks) variables must be on the same scale, or variables with large values will incorrectly dominate the training process.
