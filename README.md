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

#### 2.2.1. Numeric Values Only
Regression model assume that all features are numeric, more specific conitnuous numeric. For baseline purpose, all numeric value were selected, without scaling process.

> ['MSSubClass', 'LotFrontage', 'LotArea', 'OverallQual', 'OverallCond', 'YearBuilt', 'YearRemodAdd', 'MasVnrArea', 'BsmtFinSF1', 'BsmtFinSF2', 'BsmtUnfSF', 'TotalBsmtSF', '1stFlrSF', '2ndFlrSF', 'GrLivArea','BsmtFullBath', 'FullBath', 'HalfBath', 'BedroomAbvGr', 'TotRmsAbvGrd', 'Fireplaces', 'GarageYrBlt', 'GarageCars', 'GarageArea', 'WoodDeckSF', 'OpenPorchSF', 'MoSold', 'YrSold']

#### 2.2.2. Numeric Values Only with StandardScaler
The next step is standardization scaling using standardscaler. It was not only to improve score but also to make easier model interpretation.

## 3. Training of Regression Model
Using the dataset with features selection in previous section, various models were trained and compared.  The description and results from these models are shown below.

### 3.1. Training Result for Section 2.2.1. Numeric Values Only
The regression model performs prediction by combining all numeric value without scaling/standardisation. This model would be a baseline for next feature engineering model.
Intercept:
> 411780.8240664884

Coefficient:
> [-2.09665894e+02, -7.70098616e+01,  4.34117749e-01,  1.80732818e+04, 5.12955066e+03,  2.43820188e+02,  1.19090279e+02,  3.20337074e+01, 9.90873289e+00,  1.43098504e+00, -8.23605447e-01,  1.05161125e+01, 2.12458809e+01,  2.37681600e+01,  2.68109637e+01,  8.57148052e+03, 1.97965513e+03, -1.55984055e+03, -9.63530530e+03,  4.02416519e+03, 5.63014201e+03,  1.73565734e+02,  1.27677216e+04, -4.81269106e+00, 2.06707347e+01, -1.84572283e+00, -4.71000321e+01, -7.66864445e+02]

### 3.2. Training Result for Section 2.2.2. Numeric Values Only with StandardScaler
When all features in the same scale, it's easier to interpret. From these coefficient we could take short conclusion that OverallQual have the most positive impact when MSSubClass have the most negative impact. They means higher OverallQuall will increase SalePrice, but higher MSSubClass will decrease SalePrice. Perhaps it doesn't make sense for higher class will get cheaper sales, or it should remind me that MSSubClass even in numeric, it is still categorical and should get another handling.
Intercept:
> 180921.19589041095

Coefficient:
> [-8865.9491972 , -1695.76732218,  4331.56009023, 24986.72482286, 5706.20539294,  7361.55537745,  2457.82509304,  5787.51288932, 4581.05657485,   253.13770241,  -302.52250405,  4551.05588833, 8210.58374253, 10371.92384808, 14083.80977611,  4446.30866026, 1090.24972779,  -784.15232517, -7857.57817491,  6538.61069285, 3628.32009093,  4347.1917959 ,  9538.24180844, -1028.62419943, 2589.95753742,  -122.2483754 ,  -127.29726391, -1018.12007687]

## 4. Results
Observations and additional results obtained after training the models described in the previous section are shown below. Just did standardization in features could made a little improvement.
![alt text](result.png "Fig. 5. Scatter plot")

| Model | R^2 | RSME | Kaggle Score |
|-------|--------------|--------------|-------------|
| Numeric values only | 0.845 | 31671.964 | 0.452 |
| Numeric values only - standarscaler | 0.846 | 31556.481 | 0.254 |

## 5. Conclusion
Standardization could make good interpretation and good improvement. For the next submission, we should use all data.