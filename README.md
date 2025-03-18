# **OVERVIEW**

Welcome to my exploration of the data job market, with a focus on data analyst roles. This project stemmed from a desire to better understand and navigate job opportunities in this field. It examines the most in-demand and highest-paying skills, aiming to identify the best prospects for data analysts. The analysis is based on data from Luke Barousse's Python Course, which offers comprehensive insights into job titles, salaries, locations, and key skills. Using Python scripts, I investigate critical questions such as the most sought-after skills, salary trends, and the relationship between demand and compensation in data analytics.

# **THE QUESTIONS**

Below are the questions I want to answer in my project:
1. What are the skills most in demand for the top 3 most popular data roles in United States?
2. How are in-demand skills trending for Data Analysts?
3. How well do jobs and skills pay for Data Analysts?
4. What are the optimal skills for data analysts to learn? (High Demand AND High Paying)

# **TOOLS I USED**

For my deep dive into the data analyst job market, I harnessed the power of several key tools:
• Python: The backbone of my analysis, allowing me to analyze the data and find critical insights.

-  Pandas Library: The Python library used to analyze the data.
-  Matplotlib Library: The library I used to visualize my data.    
-  Seaborn Library: The library I used to create more advanced visuals.
      
• Google Colab: The tool I used to run my Python scripts which let me easily include my notes and analysis.
• GitHub: Essential for version control and sharing my Python code and analysis, ensuring collaboration and project tracking.

# **DATA PREPERATION AND CLEANUP**
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

# **THE ANALYSIS**

Each Google Colab Notebook in this project is designed to explore a specific aspect of the data job market. Here's how I approached each question:

## **1. What are the most demanded skills for the top 3 most popular data roles?**
To identify the most in-demand skills for the top three most popular data roles, I first filtered the dataset to determine the most common job titles. Then, I extracted the top five skills associated with these roles. This analysis highlights the most sought-after job titles and their key skills, helping me understand which skills to prioritize based on my target role.

View my notebook with detailed steps here: [Skills Analysis](Skills_Analysis.ipynb)










