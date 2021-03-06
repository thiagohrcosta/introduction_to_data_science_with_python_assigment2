
# Assignment 2 - Pandas Introduction

Todas as questões são ponderadas da mesma forma para a presente tarefa. Para responder estas questões utilizou-se o Jupyter
Notebook integrando Python e Pandas.
<hr>
All questions are weighted the same in this assignment. To answer this questions, was used Jupyter Notebok to integrate Python
and Pandas.

## Part 1

O código abaixo carrega o *Olympics dataset (olympic.csv)*, que foi extraído do Wikipedia no seguinte caminho [All Time Olympic Games Medals](https://en.wikipedia.org/wiki/All-time_Olympic_Games_medal_table), e realiza tratamento básico de dados.

As colunnas são organizadas como # of Sumer games, Summer medals, # of Winter games, Winter medals, total # number of games, total # of medals. Utilize estas par/ãmetros para responder as questões abaixo. 
<hr>
The following code loads the olympics dataset (olympics.csv), which was derrived from the Wikipedia entry on [All Time Olympic Games Medals](https://en.wikipedia.org/wiki/All-time_Olympic_Games_medal_table), and does some basic data cleaning. 

The columns are organized as # of Summer games, Summer medals, # of Winter games, Winter medals, total # number of games, total # of medals. Use this dataset to answer the questions below.


```python
import pandas as pd

df = pd.read_csv('olympics.csv', index_col=0, skiprows=1)

for col in df.columns:
    if col[:2]=='01':
        df.rename(columns={col:'Gold'+col[4:]}, inplace=True)
    if col[:2]=='02':
        df.rename(columns={col:'Silver'+col[4:]}, inplace=True)
    if col[:2]=='03':
        df.rename(columns={col:'Bronze'+col[4:]}, inplace=True)
    if col[:1]=='№':
        df.rename(columns={col:'#'+col[1:]}, inplace=True)

names_ids = df.index.str.split('\s\(') # split the index by '('

df.index = names_ids.str[0] # the [0] element is the country name (new index) 
df['ID'] = names_ids.str[1].str[:3] # the [1] element is the abbreviation or ID (take first 3 characters from that)

df = df.drop('Totals')
df.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th># Summer</th>
      <th>Gold</th>
      <th>Silver</th>
      <th>Bronze</th>
      <th>Total</th>
      <th># Winter</th>
      <th>Gold.1</th>
      <th>Silver.1</th>
      <th>Bronze.1</th>
      <th>Total.1</th>
      <th># Games</th>
      <th>Gold.2</th>
      <th>Silver.2</th>
      <th>Bronze.2</th>
      <th>Combined total</th>
      <th>ID</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Afghanistan</th>
      <td>13</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>13</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>2</td>
      <td>AFG</td>
    </tr>
    <tr>
      <th>Algeria</th>
      <td>12</td>
      <td>5</td>
      <td>2</td>
      <td>8</td>
      <td>15</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>15</td>
      <td>5</td>
      <td>2</td>
      <td>8</td>
      <td>15</td>
      <td>ALG</td>
    </tr>
    <tr>
      <th>Argentina</th>
      <td>23</td>
      <td>18</td>
      <td>24</td>
      <td>28</td>
      <td>70</td>
      <td>18</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>41</td>
      <td>18</td>
      <td>24</td>
      <td>28</td>
      <td>70</td>
      <td>ARG</td>
    </tr>
    <tr>
      <th>Armenia</th>
      <td>5</td>
      <td>1</td>
      <td>2</td>
      <td>9</td>
      <td>12</td>
      <td>6</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>11</td>
      <td>1</td>
      <td>2</td>
      <td>9</td>
      <td>12</td>
      <td>ARM</td>
    </tr>
    <tr>
      <th>Australasia</th>
      <td>2</td>
      <td>3</td>
      <td>4</td>
      <td>5</td>
      <td>12</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>3</td>
      <td>4</td>
      <td>5</td>
      <td>12</td>
      <td>ANZ</td>
    </tr>
  </tbody>
</table>
</div>



### Question 0 (Example)

What is the first country in df?

*This function should return a Series.*


```python
# You should write your whole answer within the function provided. The autograder will call
# this function and compare the return value against the correct solution value
def answer_zero():
    # This function returns the row for Afghanistan, which is a Series object. The assignment
    # question description will tell you the general format the autograder is expecting
    return df.iloc[0]

# You can examine what your function returns by calling it in the cell. If you have questions
# about the assignment formats, check out the discussion forums for any FAQs
answer_zero() 
```




    # Summer           13
    Gold                0
    Silver              0
    Bronze              2
    Total               2
    # Winter            0
    Gold.1              0
    Silver.1            0
    Bronze.1            0
    Total.1             0
    # Games            13
    Gold.2              0
    Silver.2            0
    Bronze.2            2
    Combined total      2
    ID                AFG
    Name: Afghanistan, dtype: object

### Question 1
Which country has won the most gold medals in summer games?

*This function should return a single string value.*


```python
# First Answer #############################################################################################
# Building using a FullSpeed HtDF Recipe style - Learned from the discipline **How To Code Simple Data**,
# belonged from the MicroMaster Software Developer created by **University of British Columbia** and offer
# on **Edx plataform**.
# Call Function: def answer_one; than call the 'df' set to gold medals ; return;
# Prototype: return(df['Gold'])  than apply the Pandas function to get the first occurrence of max value;
# PANDAS = argmax: Index of first occurrence of maximum of values;
# Prototype finished: return(df['Gold].argmax()
# Expected out result: 'Single String value'.

def answer_one():
    return (df['Gold'].argmax())
answer_one()
```




    'United States'


### Question 2
Which country had the biggest difference between their summer and winter gold medal counts?

*This function should return a single string value.*


```python
# Second Answer ######################################################################################
# Building using a FullSpeed HtDF Recipe style - Learned from the discipline **How To Code Simple Data**,
# belonged from the MicroMaster Software Developer created by **University of British Columbia** and offer
# on **Edx plataform**.
# Call Function: def answer_two; return; than call df for max gold medals on summer winter gold medals
# than calculate the difference between this medals;
# Prototype: def answer_two; summer df['Gold'] - winter df['Gold.1']; difference = summer - winter
# Pandas argmax: Index of first occurrence of maximum of values.
# Prototype finished: return (df['Gold]  - df['Gold.1]).argmax()

def answer_two():
    return (df['Gold'] - df['Gold.1']).argmax()
answer_two()

```




    'United States'
    
    
    ### Question 3
Which country has the biggest difference between their summer gold medal counts and winter gold medal counts relative to their total gold medal count **{Summer~Gold - Winter~Gold}{Total~Gold}**. Only include countries that have won at least 1 gold in both summer and winter.

*This function should return a single string value.*


```python
# Third Answer ######################################################################################
# Building using a FullSpeed HtDF Recipe style - Learned from the discipline **How To Code Simple Data**,
# belonged from the MicroMaster Software Developer created by **University of British Columbia** and offer
# on **Edx plataform**.
# I used PEP8 style to format the code to a easier way to read - The Pep8 Style was teach on course
# **FullStack Web Developer** offer by **Udacity**.
# Call Function: def answer_three; return; named goldMedals and call df[(df['Gold.1']) & (df['Gold])]
# The question ask for country who has 1 or more, so need to add ''>0'' or ">=1" in the function
# Prototype: Function with 1 or more:  df[(df['Gold.1]>=1 & (df['Gold])>=1)]
# Then calculate the difference between Gold - Gold.1 / TotalMedals
# Pandas ABS = Return a Series/DataFrame with absolute numeric value of each element.
# Prototype: goldMedals['biggestDifference'] = (abs(goldMedals['Gold] - goldMedals['Gold.1]))/goldMedals['Gold.2']
# Pandas argmax: Index of first occurrence of maximum of values.
# Finally, the return result with .argmax:  goldMedals['biggestDifference'].argmax()

def answer_three():
    goldMedals = df[(df['Gold.1'] >= 1) & (df['Gold'] >=1)]
    goldMedals['biggestDifference'] = (abs(goldMedals['Gold'] - 
                                           goldMedals['Gold.1'])) / goldMedals['Gold.2']
    return goldMedals['biggestDifference'].argmax()

answer_three()

```
