# Market analyzing in python

## Analyzing marketing campaigns with pandas

### pandas

1. data convert

    ```{python}
    print(marketing['is_retained'].dtype)
    marketing['is_retained'] = marketing['is_retained'].astype('bool')
    ```

2. map columns with dictionary.

    ```{python}
    # Mapping for channels
    channel_dict = {"House Ads": 1, "Instagram": 2, 
                    "Facebook": 3, "Email": 4, "Push": 5}
    # Map the channel to a channel code
    marketing['channel_code'] = marketing['subscribing_channel'].map(channel_dict)
    ```

3. `np.where` create a new column

    ```{python}
    #import numpy as np

    # Add the new column is_correct_lang
    marketing['is_correct_lang'] = np.where(marketing['language_displayed'] == marketing['language_preferred'], 'Yes', 'No')
    ```

4. `read_csv()` date

    ```{python}
    # Import marketing.csv with date columns
    marketing = pd.read_csv('marketing.csv', parse_dates = ['date_served','date_subscribed', 'date_canceled'])

    # Add a DoW column
    marketing['DoW'] = marketing['date_subscribed'].dt.dayofweek
    ```

5. `.groupby()` and `.nunique()`

    ```{python}
    # Group by date_served and count number of unique user_id's
    ```

6. plot 

    ```{python}
    # Plot daily_subscribers
    daily_users.plot()
    #daily_users.plot(kind = 'bar')
    # Include a title and y-axis label
    plt.title('Daily users')
    plt.ylabel('Number of users')
    # Rotate the x-axis labels by 45 degrees
    plt.xticks(rotation = 45)
    # Display the plot
    plt.show()
    ```

### Introduction to common marketing metrics

1. common metrics:

  - Conversion rate 转化率
  - Retention rate 留存

    ```{python}
    # Group by language_displayed and count unique users
    total = marketing.groupby(['language_displayed'])['user_id'].nunique()

    # Group by language_displayed and count unique conversions
    subscribers = marketing[marketing['converted']].groupby(['language_displayed'])['user_id'].nunique()

    # Calculate the conversion rate for all languages

    print(language_conversion_rate)
    ```

2. `unstack(level = '')` Level of index to unstack, can pass level names

  After unstack the output is a pd.Series, with multiindex. 


    ```{python}
    channel_age = marketing.groupby(['marketing_channel', 'age_group'])\
                                    ['user_id'].count()

    # Unstack channel_age and transform it into a DataFrame
    channel_age_df = pd.DataFrame(channel_age.unstack(level = 1))

    # Plot channel_age
    channel_age_df.plot(kind = 'bar')
    plt.title('Marketing channels by age group')
    plt.xlabel('Age Group')
    plt.ylabel('Users')
    # Add a legend to the plot
    plt.legend(loc = 'upper right', labels = channel_age_df.columns.values)
    plt.show()
    ```
3. plot for columns in dataframe

  ```{python}
  def plotting_conv(dataframe):
    for column in dataframe:
        # Plot column by dataframe's index
        plt.plot(dataframe.index, dataframe[column])
        plt.title('Daily ' + str(column) + ' conversion rate\n', 
                  size = 16)
        plt.ylabel('Conversion rate', size = 14)
        plt.xlabel('Date', size = 14)
        # Show plot
        plt.show()  
        plt.clf()
  ```

4. 

  ```{python}
      # Create English conversion rate column for affected period 
      converted['english_conv_rate'] = converted.loc['2018-01-11':'2018-01-31'][('converted','English')]
  ```

