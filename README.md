# **Overview**

Welcome to my exploration of the data job market, with a focus on data analyst roles. This project stemmed from a desire to better understand and navigate job opportunities in this field. It examines the most in-demand and highest-paying skills, aiming to identify the best prospects for data analysts. The analysis is based on data from Luke Barousse's Python Course, which offers comprehensive insights into job titles, salaries, locations, and key skills. Using Python scripts, I investigate critical questions such as the most sought-after skills, salary trends, and the relationship between demand and compensation in data analytics.

# **The Questions**

Below are the questions I want to answer in my project:
1. What are the skills most in demand for the top 3 most popular data roles in United States?
2. How are in-demand skills trending for Data Analysts?
3. How well do jobs and skills pay for Data Analysts?
4. What are the optimal skills for data analysts to learn? (High Demand AND High Paying)

# **Tools I Used**

For my deep dive into the data analyst job market, I harnessed the power of several key tools:
• Python: The backbone of my analysis, allowing me to analyze the data and find critical insights.

-  Pandas Library: The Python library used to analyze the data.
-  Matplotlib Library: The library I used to visualize my data.    
-  Seaborn Library: The library I used to create more advanced visuals.
      
• Google Colab: The tool I used to run my Python scripts which let me easily include my notes and analysis.
• GitHub: Essential for version control and sharing my Python code and analysis, ensuring collaboration and project tracking.

# **Data Preparation and Cleanup**
This section outlines the steps taken to prepare the data for analysis, ensuring accuracy and usability.

## **Import & Clean Up Data**
I begin by importing the required libraries and loading the dataset. Next, I perform initial data cleaning to maintain data quality and ensure accuracy in the analysis.

```python
#Importing Libraries
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from datasets import load_dataset
import ast
      
#Loading the data and assigning it to a variable
dataset = load_dataset('lukebarousse/data_jobs')
df = dataset['train'].to_pandas()
      
#cleaning the data
df['job_posted_date'] = pd.to_datetime(df['job_posted_date'])
df['job_skills'] = df['job_skills'].apply(lambda x: ast.literal_eval(x) if pd.notna(x) else x)
```

## **Filter for US Jobs**
```python
#Filtering for Data in United States
df_US = df[df['job_country'] == 'United States']
```

# **The Analysis**

Each Google Colab Notebook in this project is designed to explore a specific aspect of the data job market. Here's how I approached each question:

## **1. What are the most demanded skills for the top 3 most popular data roles?**
To identify the most in-demand skills for the top three most popular data roles, I first filtered the dataset to determine the most common job titles. Then, I extracted the top five skills associated with these roles. This analysis highlights the most sought-after job titles and their key skills, helping me understand which skills to prioritize based on my target role.

View my notebook with detailed steps here: [Skills Analysis](Skills_Analysis.ipynb)

### **Vizualizing the data**
```python
fig, ax = plt.subplots(len(job_titles), 1)

for i, job_title in enumerate(job_titles):
  df_perc_plot = df_merged[df_merged['job_title_short'] == job_title].head(5)
  sns.barplot(data = df_perc_plot, x = 'skill_percentage', y = 'job_skills', ax = ax[i], hue = 'job_skills', palette = 'dark:blue')
  ax[i].set_title(job_title)
  ax[i].set_ylabel('')
  ax[i].set_xlabel('')

  #Adding the percentages as text beside the bars
  for n, v in enumerate(df_perc_plot['skill_percentage']):
    ax[i].text(v+1, n, f'{v:.0f}%', va='center')

  ax[0].set_xlim(0, 68)
  ax[1].set_xlim(0, 80)
  ax[2].set_xlim(0, 90)

  if i != len(job_title) - 1:
    ax[i].set_xticks([])

fig.suptitle('Likelhood of skills requested in US job postings', fontsize = 15)
fig.tight_layout()
```

### **Results**

![image](https://github.com/user-attachments/assets/4de5d84e-8f2e-4137-a3b0-4dda6c51b28c)

*Bar graph visualizing the Likelhood of skills requested in US job posting in the top 3 roles.*

### **Insights**

1. SQL is a crucial skill across all three roles – It appears in the top skills for Data Analysts (60%), Data Engineers (72%), and Data Scientists (58%), emphasizing its importance in data-related job postings.

2. Python is highly sought after, especially for Data Scientists (82%) and Data Engineers (68%) – While it is also relevant for Data Analysts (32%), it is more dominant in roles like Data Science and Data Engineering.

3. Role-specific tools vary – Excel (48%) and Tableau (34%) are more relevant for Data Analysts, AWS (45%) and Spark (34%) are key for Data Engineers, while R (50%) is a notable requirement for Data Scientists. This highlights how different roles prioritize distinct skill sets.

# **2. How are in-demand skills trending for Data Analysts?**

To analyze skill trends for Data Analysts, I filtered job postings for data analyst roles and grouped the required skills by the month they were listed. This allowed me to identify the top five skills for each month, providing insights into how skill demand evolved throughout the year.

View my notebook with detailed steps here: [Skills Trends](Skills_Trends.ipynb)

### **Vizualizing the data**

```python
df_plot = df_DA_perc.iloc[:, :5]

sns.lineplot(data = df_plot, dashes = False, palette='tab10')
plt.title('Top trending skills for Data Analysts')
plt.xlabel('2024')
plt.ylabel('Likelihood in job postings')
plt.legend().remove()

from matplotlib.ticker import PercentFormatter
ax=plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals = 0))
for i in range(5):
  plt.text(11.2, df_plot.iloc[-1, i], df_plot.columns[i])

sns.despine()
```
### **Results**

![image](https://github.com/user-attachments/assets/952e4495-bded-461a-af1d-2dd7eb2918f7)

*Bar graph visualizing the trending top skills for data analysts*

### **Insights**

1. SQL remains the most in-demand skill throughout the year – It consistently holds the highest percentage of mentions in job postings, reinforcing its importance for Data Analysts.

2. Python and Excel show fluctuating trends – Python sees a slight increase toward the end of the year, while Excel experiences a decline after mid-year, suggesting a possible shift toward programming-based skills.

3. Tableau and Power BI remain stable but less dominant – Both visualization tools maintain a steady demand, though at a lower percentage compared to SQL and Python and Excel. Power BI shows a shows a slight upward trend after the 1st Quarter. 

## **3. How well do jobs and skills pay for Data Analysts?**
To determine the highest-paying roles and skills, I focused on jobs in the United States and examined their median salaries. Before that, I reviewed the salary distributions of common data jobs such as Data Scientist, Data Engineer, and Data Analyst to understand which positions offer the highest pay.

View my notebook with detailed steps here: [Skills Trends](Skills_Analysis.ipynb)

### **Vizualizing the data**
```python
#Plotting
sns.boxplot(data=df_US_6, x='salary_year_avg', y='job_title_short', hue = 'job_title_short', palette='dark:blue', order = job_order['job_title_short'])
plt.title('Salary distribution of data jobs in US')
plt.xlim(0, 420000)
plt.ylabel('Job Title')
plt.xlabel('Yearly salary average')
ax = plt.gca()
ax.xaxis.set_major_formatter(plt.FuncFormatter(lambda x, pos: f'${int(x/1000)}k'))
plt.show()
```

### **Results**
![image](https://github.com/user-attachments/assets/475386f1-bc5f-44a9-b99c-b557709e3989)

Box plot visualizing the salary distributions for the top 6 data job titles.

### **Insights**
1. Senior Data Scientists and Senior Data Engineers have the highest median salaries, while Data Analysts earn the lowest. The salary gap between junior and senior roles is substantial.

2. Senior Data Scientists and Senior Data Engineers have multiple high-end outliers. This indicates that top professionals in these roles can earn exceptionally high compensation.

3. The median salaries increase with the seniority and specialization of the roles. Senior roles (Senior Data Scientist, Senior Data Engineer) not only have higher median salaries but also larger differences in typical salaries, reflecting greater variance in compensation as responsibilities increase.
