# Kaggle Exercise: Regression Model

## 1. Introduction
Regression is a method of modelling a target value based on independent predictors. This method is mostly used for forecasting and finding out cause and effect relationship between variables. Regression techniques mostly differ based on the number of independent variables and the type of relationship between the independent and dependent variables.
In this project, I want to practice how to use regression model and find out how to improve the regression model. On the first run, I would like to use all numerical data without linearity assessment. I assume the R-squared and RMSE for this model could be the baseline.
In the next move, I would like to implement some assumptions on regression model:
- Data is free of missing values and outliers
- All variables are continuous numeric, not categorical
- There is a linear relationship between predictors and predictant
- All predictors are independent of each other
- Residuals (aka prediction errors) are normally distributed
- No heteroscedacity
- Absence of multicollinearity abd auto-correlation

The linear regression model can be represented by the equation below.
> h<sub>&theta;</sub>(x) = &theta;<sub>o</sub> + &theta;<sub>1</sub>x<sub>1</sub> + &theta;<sub>2</sub>x<sub>2</sub> + ... + + &theta;<sub>n</sub>x<sub>n</sub>

## 2. The Data: House Prices
I got the data from the Kaggle Competition. The goal from this competition is to predict sales price for each house. Ask a home buyer to describe their dream house, and they probably won't begin with the height of the basement ceiling or the proximity to an east-west railroad. But this playground competition's dataset proves that much more influences price negotiations than the number of bedrooms or a white-picket fence. With 79 explanatory variables describing (almost) every aspect of residential homes in Ames, Iowa.
Dataset has been splitted into train and test. Not like train-dataset, test-dataset didn't have complete data, it's miss the SalePrice column. To complete test-dataset, we merged it with submission.csv.

### 2.1. Data Processing
The data downloaded, as mentioned above, was cleaned up and processed before using it for model fitting. There was missing value in the data that we need to handle. The data with more than 90% missing value were utterly removed. For data with less than 50%, the missing value was imputed by their median (numeric) or mode (categoric). There was a particular case for correlation in missing value, which means the data was null because data in another column was null. The data after this initial cleanup is shown in Fig 2.
![alt text](miss_before.png "Fig. 1. Missing values matrix for all features")

![alt text](miss_after.png "Fig. 2. Missing values matrix after initial cleanup")

After initial cleanup, next step was to check variation in categorical data. I used a simple matrix by compared number of each value and their average. The higher result means that column almost contains one value and not fairly distributed. So it can be completely removed when the result more than 70.
![alt text](variations.png "Fig. 3. Categorical variations matrix")

![alt text](miss_total_cleanup.png "Fig. 4. Missing value matrix after total cleanup")

### 2.2. Feature Selection and Engineering
First step of feature engineering would be based on regression's assumptions. I would like to compare each assumption.

#### 2.2.1. Numeric Value Only
Regression model assume that all features are numeric, more specific conitnuous numeric. For baseline purpose, all numeric value were selected, without scaling process.

> ['MSSubClass', 'LotFrontage', 'LotArea', 'OverallQual', 'OverallCond', 'YearBuilt', 'YearRemodAdd', 'MasVnrArea', 'BsmtFinSF1', 'BsmtFinSF2', 'BsmtUnfSF', 'TotalBsmtSF', '1stFlrSF', '2ndFlrSF', 'GrLivArea','BsmtFullBath', 'FullBath', 'HalfBath', 'BedroomAbvGr', 'TotRmsAbvGrd', 'Fireplaces', 'GarageYrBlt', 'GarageCars', 'GarageArea', 'WoodDeckSF', 'OpenPorchSF', 'MoSold', 'YrSold']

## 3. Training of Regression Model
Using the dataset with features selection in previous section, various models were trained and compared.  The description and results from these models are shown below.

### 3.1. Training Result for Section 2.2.1. Numeric Values Only
The regression model performs prediction by combining all numeric value without scaling/standardisation. This model would be a baseline for next feature engineering model.