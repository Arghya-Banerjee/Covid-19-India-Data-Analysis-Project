# Covid-19 India Data Analysis Project

This is a practice **Data Analysis Project** by me in the field of **Covid-19 Virus** spreading in India. The Data/Datasets used in this is project are provided by **[Kaggle](https://www.kaggle.com/)**.

Following is the link to the Dataset in Kaggle's official website: **[Covid-19 India Datasets](https://www.kaggle.com/datasets/sudalairajkumar/covid19-in-india)**

The main motive behind this project was just practicing and learning new things in the field of Data Analysis for me. The whole project has been done in Jupyter Notebook `Covid19 Data Analysis Project.ipynb` provided in my Github Repository named **Covid-19-India-Data-Analysis-Project**.

### Modules used in this project are:

<ul>
    <li> [Pandas](https://pandas.pydata.org/) </li>
    <li> [Numpy](https://numpy.org/) </li>
    <li> [Matplotlib](https://matplotlib.org/) </li>
    <li> [Seaborn](https://seaborn.pydata.org/) </li>
    <li> [Plotly](https://plotly.com/python/) </li>
    <li> [Datetime](https://docs.python.org/3/library/datetime.html) </li>
</ul>

### Things I have done in this Project:

Firstly I imported all the downloaded datasets into the project using the `pd.read_csv("dataset.csv")` command into 3 different datasets. After that I used some data exploration commands like `df.head()`, `df.tail()`, `df.info()` as well as `df.describe()` to explore the data and see for NULL values and anomaly. 

After the data exploration part was over it was time to divide and sort the datasets into suitable form to draw insights and reprent it in graphical form for better usderstanding of the numbers.

At last I used a mixture of all graphical modules in python to draw graphs and pie charts to represent the data in a more cleaner and understandable way than a excel file or a csv file.


## Graphical Insights from the Data:

#### Confirmed vs Recovery Rate vs Mortality Rate Demographic according to States

```
statewise = pd.pivot_table(covid_df, values = ["Confirmed", "Deaths", "Cured"], index = "State/UnionTerritory", aggfunc = max)
statewise["Recovery_Rate"] = statewise["Cured"] * 100 / statewise["Confirmed"]
statewise["Mortality_Rate"] = statewise["Deaths"] * 100 / statewise["Confirmed"]
statewise = statewise.sort_values(by = "Confirmed", ascending = False)
statewise.style.background_gradient(cmap = "Blues")
```

![1](https://user-images.githubusercontent.com/72212592/174432024-6dd87313-1067-4e35-a0c9-547d97533ab2.jpg)

#### Top 10 States with Most Active Cases 

```
top_10_active_cases_statewise = covid_df.groupby(by = 'State/UnionTerritory').max()[['Active_Cases', 'Date']].sort_values(by = ['Active_Cases'], ascending = False).reset_index()

fig = plt.figure(figsize = (20, 11))

plt.title("Top 10 States with Most Active Cases", size = 25)

ax = sns.barplot(data = top_10_active_cases_statewise.iloc[:10], y = 'Active_Cases', x = 'State/UnionTerritory', linewidth = 2, edgecolor = 'red')

plt.xlabel("States")
plt.ylabel("Total Active Cases")
plt.show()
```

![2](https://user-images.githubusercontent.com/72212592/174432032-eecc2d1b-154a-45d2-bc91-a64413946106.png)

#### Top 10 States with Least Active Cases 

```
top_10_deaths_statewise = covid_df.groupby(by = 'State/UnionTerritory').max()[['Deaths', 'Date']].sort_values(by = ['Deaths'], ascending = False).reset_index()

fig = plt.figure(figsize = (18, 10))

plt.title("Top 10 States with Most Deaths", size = 25)

ax = sns.barplot(data = top_10_deaths_statewise.iloc[:12], y = 'Deaths', x = 'State/UnionTerritory', linewidth = 2, edgecolor = 'red')

plt.xlabel("States")
plt.ylabel("Total Deaths")
plt.show()
```

![3](https://user-images.githubusercontent.com/72212592/174432038-596c64ec-8949-4ee1-9a60-e4dda59e2aff.png)

#### Top 5 States Affected by Covid-19

```
fig = plt.figure(figsize = (20,6))

ax = sns.lineplot(data = covid_df[covid_df['State/UnionTerritory'].isin(['Maharashtra', 'Kerala', 'West Bengal', 'Madhya Pradesh', 'Delhi'])], x = 'Date', y = 'Active_Cases', hue = 'State/UnionTerritory')

ax.set_title("Top 5 Covid Affected States in India", size = 16)
```

![4](https://user-images.githubusercontent.com/72212592/174432048-878edadd-14de-4a18-a27d-968ab2996ef0.png)

#### Male vs Female Vaccination

```
male = vaccination['Male(Individuals Vaccinated)'].sum()
female = vaccination['Female(Individuals Vaccinated)'].sum()
px.pie(names = ['Male', 'Female'], values = [male, female], title = 'Male vs Female Vaccination')
```

![5](https://user-images.githubusercontent.com/72212592/174432054-f10a9ca9-af97-445a-a504-2d9b7ed6e0a6.png)

#### Top 5 States with Most Vaccinated Individuals

```
max_vaccine = vaccine_no_india_state.groupby('State')['Total'].sum().to_frame('Total')
max_vaccine = max_vaccine.sort_values('Total', ascending = False)[:5]

fig = plt.figure(figsize = (20,10))
plt.title('Top 5 States with Most number of Vaccinated Individuals', size = 30)
ax = sns.barplot(data = max_vaccine.iloc[:10], y = max_vaccine.Total, x = max_vaccine.index, linewidth = 2, edgecolor = 'blue')
plt.xlabel("State")
plt.ylabel("Vaccinated Individuals")
plt.show()
```

![6](https://user-images.githubusercontent.com/72212592/174432057-6bce08ca-13ff-4d3e-bc66-ed663113ac59.png)

#### Top 5 States with Least Vaccinated Individuals

```
min_vaccine = vaccine_no_india_state.groupby('State')['Total'].sum().to_frame('Total')
min_vaccine = min_vaccine.sort_values('Total', ascending = True)[:5]

fig = plt.figure(figsize = (20,10))
plt.title('Top 5 States with Least number of Vaccinated Individuals', size = 30)
ax = sns.barplot(data = min_vaccine.iloc[:10], y = min_vaccine.Total, x = min_vaccine.index, linewidth = 2, edgecolor = 'blue')
plt.xlabel("State")
plt.ylabel("Vaccinated Individuals")
plt.show()
```

![7](https://user-images.githubusercontent.com/72212592/174432062-875dec3c-e889-405c-a5e1-6dcabb5555c3.png)

