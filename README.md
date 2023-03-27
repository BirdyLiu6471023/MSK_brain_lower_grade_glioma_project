# MSK_brain_lower_grade_glioma_project

<img src="images/dna_repo.jpg" width="400" height="200"/>


# Prediction for Subtype of LGG: 

In 2016, WHO changed the classification of Brain Lower Grade Glioma by the presence or absense of iscocitrate dehydrogenase (IDH) mutation and chromosome 1p/19q codeletion instead of from histology diagnosis, so now there are 3 categories: 

1) IDH mutation with 1p/19q codeletion (oligodendroglioma); 

2) IDH mutation without 1p/19q codeletion (most grades II and III astrocytoma)

3) IDH wildtype (most glioblastoma)

The classification provides better prognostications according to TCGA's description, and this would be discussed in **Emile's part, Overall Survival (OS) Analysis**.

THIS part is to **predict the 1p/19q codeletion status using gene expression matrix (RNA-Seq)**. The supervised learning model, random forest classifier was used with future selection by f_regression score function, which give a high accuracy score, around **98%**. Using Non-negative Matrix Factorization A = WH with rank = 20, the accuracy score of random forest model with H as features is **97%**, and metagene 10, 2 and 1 are the most important features.

**The model's top features, here genes might be not the "real" top features:**
After training the random forest model 50 times, I find that top genes are totally different, and if we using the genes that never has feature importance (feature_importance_val = 0) as features to train the RF model, it still could get 97% accuracy. If there is not data leakage (in most paper about BLGG, they all have around 97% accuracy), then it would means the genes has highly correlations between each other. I would say gene is an environment for tumor, so we could not see gene one by one and need to group them and cluster in some ways that could be measured and reversed. There are 3 methods I could come up to solve this: 

**Method 1: Non-Negative Matrix Factorization**

This method has already be implemented (with 97% accuracy score) and need to do more to scale the data using Max-Min scaler; and also might need to use some NLP method to find the functionality of the metagenes (gene group). 

**Method 2: Correlation Matrix** 

Remove the highly correlated genes (similarity) in the features. 

**Method 3: NLP for Gene Description** 

Firstly, cluster the genes with NLP methods using data from gene library (gene description, GO terms, etc.) and then use this clustered gene groups as features to predict the subtype of tumor or to do OS analysis.



# Jin

## **Mutation Count Analyst** - Gene Expression and Clinical Data Analysis

This project aims to identify potential therapeutic targets for new cancer treatments by analyzing gene expression and clinical data and exploring the relationship between different genes, proteins, and cancer mutation count.

### Literature Review
Genetic mutations can cause cancer by altering protein function, affecting crucial cellular processes such as cell growth.

### Data
The analysis used gene expression data generated from RNA sequencing (RNA-seq) experiments and clinical data associated with cancer samples from cBioPortal. The dataset included 20,532 genes and 514 patients, along with 31 clinical attributes for each patient, including neoplasm cancer status, diagnosis age, sex, and survival status.

### Models
**Lasso regression, ElasticNetCV** models were used to predict feature importance ranking and corresponding coefficients. The RFE method was not used due to discrepancies in feature importance ranking compared to the other two models.

### Gene Interpretation
The following genes were identified as the most important by the Lasso regression and ElasticNetCV models:

HOXB9: Prognostic marker in head and neck cancer and endometrial cancer (unfavorable)
PCDHB6: Prognostic marker in renal cancer (unfavorable)
HNRNPCL1: Gene product is not prognostic
HOXB8: Prognostic marker in renal cancer (favorable)
PRAMEF2: Gene product is not prognostic

### Conclusion: 
The above five features are the top most important gene and protein features correspond to mutation count and cancer. From the literature review, The analysis of gene expression and clinical data identified HOXB9 and PCDHB6 as unfavorable prognostic markers for certain types of cancer, while HOXB8 was identified as a favorable prognostic marker for renal cancer. The expression of HNRNPCL1 and PRAMEF2 was not found to be associated with patient survival or disease outcome.Based on the results of this project, we were able to identify these genes and proteins strongly associated with increased cancer mutation count using machine learning models. These variables may indicate potential therapeutic targets for new cancer treatments. Further research is needed to determine the precise role of these variables in cancer development and to validate their potential as therapeutic targets. 

# Emile

### I focused on predicting the **Survival Rate**. 

#### The features I use are
- Gene expression
- Clinical data (age, sex, race, prior diagnosis, radiation therapy...)

#### The models I used:

- LASSO
- Random Forest
- GradientBoosting
- SVM
- Cox Survival Model Elastic Net

#### Results
- Cox Elastic Net is the only decent model, with **87%** R2 on testing data
- Feature importance and explainability: Diagnosis Age plays an important role, as well as genes 118430, 55970, 406, 4214

#### Using Zscores

- Cox Elastic Net gives 94% training R2, 81% test R2
