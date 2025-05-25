# RESTAURANT TIPS ANALYSIS

![](images/Restaurant.jpeg)

## Project description
This project aims to use the restaurant tips dataset to practice creating composition plots and visualizations. We will examine the relationship between different variables and the tips given.
## Source of the data
The dataset consists of information from 244 restaurant bills, collected in the US in 1987.
It includes details about the tips given to restaurant staff, such as the total bill, tip amount, gender of the person paying, smoking status, day of the week, time of day, and party size.
You can load the data from the following link: https://raw.githubusercontent.com/RusAbk/sca_datasets/main/tips.csv
## The main goals
Provide insights by comparing tip amount among different dimensional variables such as: smoker vs non-smoker, gender, day and time in day.
## Data overview

|    |   id |   total_bill |   tip | sex    | smoker   | day   | time   |   size |
|---:|-----:|-------------:|------:|:-------|:---------|:------|:-------|-------:|
|  0 |    0 |        16.99 |  1.01 | Female | No       | Sun   | Dinner |      2 |
|  1 |    1 |        10.34 |  1.66 | Male   | No       | Sun   | Dinner |      3 |
|  2 |    2 |        21.01 |  3.5  | Male   | No       | Sun   | Dinner |      3 |
|  3 |    3 |        23.68 |  3.31 | Male   | No       | Sun   | Dinner |      2 |
|  4 |    4 |        24.59 |  3.61 | Female | No       | Sun   | Dinner |      4 |

## Basic descriptive statistics

|       |       id |   total_bill |       tip |      size |
|:------|---------:|-------------:|----------:|----------:|
| count | 244      |    244       | 244       | 244       |
| mean  | 121.5    |     19.7859  |   2.99828 |   2.56967 |
| std   |  70.5809 |      8.90241 |   1.38364 |   0.9511  |
| min   |   0      |      3.07    |   1       |   1       |
| 25%   |  60.75   |     13.3475  |   2       |   2       |
| 50%   | 121.5    |     17.795   |   2.9     |   2       |
| 75%   | 182.25   |     24.1275  |   3.5625  |   3       |
| max   | 243      |     50.81    |  10       |   6       |

## Tip value influencers
### 🚬 Do people who smoke give more tips?

**The function compare_tip_dynamic_dimension(input_dimension) compares tip statistics by a specific group with the overall values in the dataset**
```python
 def compare_tip_dynamic_dimension (input_dimension):
  ## agg by dimension
  df_agg_detail = df.groupby(input_dimension).agg(tip_min = ('tip','min'),
                                                  tip_max = ('tip','max'),
                                                  tip_mean = ('tip','mean'),
                                                  tip_median = ('tip','median')
                                                  )
  df_agg_detail = df_agg_detail.T
  df_agg_detail = df_agg_detail.reset_index()
  ## agg all df
  df_agg = df.agg(tip_min = ('tip','min'),
                  tip_max = ('tip','max'),
                  tip_mean = ('tip','mean'),
                  tip_median = ('tip','median')
                  )
  df_agg.columns = ["common"]
  df_agg = df_agg.reset_index()
  ## merge
  df_compare = df_agg.merge(df_agg_detail,"inner",on = "index")
  return df_compare
```
```python
compare_tip_dynamic_dimension('smoker')
```
|    | index      |   common |      No |      Yes |
|---:|:-----------|---------:|--------:|---------:|
|  0 | tip_min    |  1       | 1       |  1       |
|  1 | tip_max    | 10       | 9       | 10       |
|  2 | tip_mean   |  2.99828 | 2.99185 |  3.00871 |
|  3 | tip_median |  2.9     | 2.74    |  3       |

**Insights**
- Smorkers tend to tip more than Non-smokers. Because the median tip of Smokers is about 8% higher than the median tip of Non-smokers. The mean tip of Smoker is greater the mean tip of Non_smokers.
- All customers who visited the restaurant at the time of data collection tipped the staff. The min tip is 1 USD and the max tip is 10 USD.
  
**General conclusion:** Smokers tips more than Non-smokers
**Look at histograms**



  
