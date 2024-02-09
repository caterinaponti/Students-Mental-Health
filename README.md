import numpy as np # linear algebra
import pandas as pd # data processing, CSV file I/O (e.g. pd.read_csv)
import matplotlib.pyplot as plt
from scipy import stats
import seaborn as sns

data = pd.read_csv("Student Mental health.csv")
data.head()

data.shape

#Rename columns
data.columns = ['Timestamp', 'Gender', 'Age', 'Course', 
                'Year of Study', 'CGPA', 'Marital Status', 
                'Depression', 'Anxiety', 'Panic Attack', 'Treatment']
data.head()

# No need for the timestamp column, a few hour difference has insignificant impact
data.drop("Timestamp",axis=1,inplace=True)

# checking missing data
data.isnull().sum()

data.describe()
data.isna().sum()

data['Course'].unique()

#since multiple entries of the same courses exist
#yet only differ in lettercase

course_mapping = {
    'engineering': 'Engineering',
    'islamic education': 'Islamic Education',
    'bit': 'BIT',
    'laws': 'Law',
    'mathemathics': 'Mathematics',
    'pendidikan islam': 'Islamic Education',
    'bcs': 'BCS',
    'human resources': 'Human Resources',
    'irkhs': 'IRKHS',
    'psychology': 'Psychology',
    'kenms': 'KENMS',
    'accounting': 'Accounting',
    'enm': 'ENM',
    'marine science': 'Marine Science',
    'koe': 'KOE',
    'banking studies': 'Banking Studies',
    'business administration': 'Business Administration',
    'kirkhs': 'KIRKHS',
    'usuluddin': 'Usuluddin',
    'taasl': 'TAASL',
    'engine': 'Engineering',
    'ala': 'ALA',
    'biomedical science': 'Biomedical Science',
    'benl': 'BENL',
    'it': 'IT',
    'cts': 'CTS',
    'econs': 'Economics',
    'mhsc': 'MHSC',
    'malcom': 'MALCOM',
    'kop': 'KOP',
    'human sciences': 'Human Sciences',
    'biotechnology': 'Biotechnology',
    'communication': 'Communication',
    'diploma nursing': 'Diploma Nursing',
    'pendidikan islam': 'Islamic Education',
    'radiography': 'Radiography',
    'fiqh fatwa': 'Fiqh Fatwa',
    'diploma tesl': 'Diploma TESL',
    'fiqh': 'Fiqh',
    'nursing': 'Nursing',
}
data['Course'] = data['Course'].str.lower().str.strip().map(course_mapping)
data.Course.unique()



#Gender Distribution
gender_counts = data['Gender'].value_counts()

#Plotting a bar chart
plt.figure(figsize=(8,6))
gender_counts.plot(kind='bar', color=['red', 'orange'], alpha = 0.7)

#Addign labels and title
plt.xlabel('Gender')
plt.ylabel('Count')
plt.title('Gender Distribution')



# Plotting a histogram for age distribution
plt.figure(figsize=(8,4))
plt.hist(data['Age'], bins = 15, color = 'skyblue', edgecolor ='blue')

# Adding labels and title
plt.xlabel('Age')
plt.ylabel('Frequency')
plt.title('Age Distribution')


# Create a DataFrame with counts for each mental health condition
mental_health_issues = data[['Depression', 'Anxiety', 'Panic Attack']].apply(pd.Series.value_counts).transpose()

#plotting bar chart
plt.figure(figsize=(8,4))
mental_health_issues.plot(kind = 'bar', stacked=True, colormap='viridis', alpha = 0.7)


#Percentage of individuals who sought specialist treatment using a pie chart. 
treatment_counts = data['Treatment'].value_counts()

plt.figure(figsize=(5,5))
plt.pie(treatment_counts, labels=treatment_counts.index, autopct='%1.1f%%', colors=['blue', 'pink'])

plt.title('Percentage of individuals who sought specialist treatment')


data['CGPA'].unique()
data['CGPA'] = data['CGPA'].replace('3.50 - 4.00 ', '3.50 - 4.00')
data['CGPA'].value_counts()
data['CGPA'].value_counts().plot(kind='bar', color='green', figsize=(5,3))


data['Year of Study'].unique()
data['Year of Study'] = data['Year of Study'].replace('year 1', 'Year 1')
data['Year of Study'] = data['Year of Study'].replace('year 2', 'Year 2')
data['Year of Study'] = data['Year of Study'].replace('year 3', 'Year 3')
data['Year of Study'].value_counts()

data['Year of Study'].value_counts().plot(kind='bar', color = 'lightblue', figsize=(4,3))


data['Course'].value_counts().plot(kind='bar', color = 'orange', figsize=(9,3))

data['Marital Status'].value_counts().plot(kind='pie', radius=1, center= (3,3), autopct='%1.1f%%', shadow=True, colors=(['green', 'blue']))

