
CRISP-DM

Cross-industry Standard Process For Data Mining

1. Business Understanding

the problem 

2. Data Understanding

what kind of data you need


`sns.heatmap(df.corr(), annot = True, fmt = ".2f")`

Drop missing values:
 
- Data entry errors
- Mechanical errors
- didn't need the data

90% of the columns is missing ,should be removed
50% of the column is missing, create a dummy variable for missing

```python
small_dataset = pd.DataFrame({'col1': [1, 2, np.nan, np.nan, 5, 6], 
                              'col2': [7, 8, np.nan, 10, 11, 12],
                              'col3': [np.nan, 14, np.nan, 16, 17, 18]})
all_drop  = small_dataset.dropna()
all_row = small_dataset.dropna(how = 'all')
only3_drop = small_dataset.dropna(axis = 0, subset= ['col3'])
only3or1_drop = small_dataset.dropna(how = 'any', axis = 0, subset= ['col1', 'col3'])
```

```python
    # Drop rows with missing salary values
    df = df.dropna(subset=['Salary'], axis=0)
    y = df['Salary']
    
    #Drop respondent and expected salary columns
    df = df.drop(['Respondent', 'ExpectedSalary', 'Salary'], axis=1)
    
    # Fill numeric columns with the mean
    num_vars = df.select_dtypes(include=['float', 'int']).columns
    for col in num_vars:
        df[col].fillna((df[col].mean()), inplace=True)
        
    # Dummy the categorical variables
    cat_vars = df.select_dtypes(include=['object']).copy().columns
    for var in  cat_vars:
        # for each cat add dummy var, drop original column
        df = pd.concat([df.drop(var, axis=1), pd.get_dummies(df[var], prefix=var, prefix_sep='_', drop_first=True)], axis=1)
    
    X = df
    return X, y
```



```python
def clean_data(df):
    '''
    INPUT
    df - pandas dataframe 
    
    OUTPUT
    X - A matrix holding all of the variables you want to consider when predicting the response
    y - the corresponding response vector
    
    Perform to obtain the correct X and y objects
    This function cleans df using the following steps to produce X and y:
    1. Drop all the rows with no salaries
    2. Create X as all the columns that are not the Salary column
    3. Create y as the Salary column
    4. Drop the Salary, Respondent, and the ExpectedSalary columns from X
    5. For each numeric variable in X, fill the column with the mean value of the column.
    6. Create dummy columns for all the categorical variables in X, drop the original columns
    '''
    df = df.dropna(subset = ['Salary'], axis = 0)
    
    X = df.drop(['Salary','Respondent', 'ExpectedSalary'], axis = 1)
    
    
    num_col = X.select_dtypes(include = ['float','int']).copy().columns
    cat_col = X.select_dtypes(include = ['object']).copy().columns
    
    for ncol in num_col:
        X[ncol].fillna(X[ncol].mean(),inplace = True)

  
    for ccol in cat_col:
        X=  pd.concat([X.drop(ccol, axis = 1), pd.get_dummies(X[ccol],prefix = ccol, drop_first = True,prefix_sep= "_" ,dummy_na = True)],axis = 1)
    
    y = df['Salary']
    return X, y
    
#Use the function to create X and y
X, y = clean_data(df)    
```
