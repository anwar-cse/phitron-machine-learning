Multivariate Analysis in EDA

EDA তে এখন আমরা শিখবো:

Multivariate Analysis

মানে:

একসাথে ৩টা বা তার বেশি feature analyse করা

1. Multivariate Analysis কী?

আগে আমরা দেখেছি:

Univariate → 1 variable
Bivariate → 2 variable

এখন:

Multivariate → Multiple variables together
2. কেন Important?

Real-world data এ relationship usually multiple feature এর উপর depend করে।

Example:

Salary শুধু experience এর উপর depend না
Education + Skill + Experience + City সব effect করতে পারে
3. Main Goals
Goal	Example
Complex pattern detect	Income vs Age vs City
Feature interaction বুঝা	Study hour + Attendance
Group behavior বুঝা	Gender + Department + Salary
Hidden relation detect	Multiple variables together
4. Multivariate Analysis Examples
Features
Age + Salary + Experience
Gender + Marks + Attendance
City + Product + Sales
5. Pairplot (VERY IMPORTANT)

সব numerical feature এর relationship একসাথে দেখায়।

Example
sns.pairplot(df)
6. Pairplot কী দেখায়?
Scatterplots
Distribution
Correlation pattern
Clusters
Outliers
7. Pairplot Structure

ধরো features:

Age
Salary
Experience

তাহলে pairplot:

Age vs Salary
Age vs Experience
Salary vs Experience
সব distribution

একসাথে দেখাবে।

8. Hue Concept (VERY IMPORTANT)

Category অনুযায়ী color separation।

Example
sns.pairplot(df, hue="Gender")
9. Hue কী help করে?

দেখতে:

Different groups আলাদা pattern follow করছে কিনা

Example:

Male vs Female clusters
10. Multivariate Scatterplot

৩টা variable একসাথে।

sns.scatterplot(
    x=df["Study_Hour"],
    y=df["Marks"],
    hue=df["Gender"]
)

এখানে:

X → Study hour
Y → Marks
Color → Gender
11. Size Parameter

আরেকটা dimension add করা যায়।

sns.scatterplot(
    x=df["Age"],
    y=df["Salary"],
    size=df["Experience"]
)
12. Style Parameter
sns.scatterplot(
    x=df["Age"],
    y=df["Salary"],
    style=df["Gender"]
)
13. Pivot Table (VERY IMPORTANT)

EDA তে extremely useful।

Example
pd.pivot_table(
    df,
    values="Salary",
    index="Department",
    columns="Gender",
    aggfunc="mean"
)
14. Pivot Table কী দেখায়?

Example:

Department	Male	Female
IT	40000	35000
HR	30000	28000
15. Groupby Deep Analysis

আগে basic দেখেছি।

এখন multiple grouping।

Example
df.groupby(
    ["Department", "Gender"]
)["Salary"].mean()
16. Multiple Aggregation
df.groupby(
    ["Department"]
)["Salary"].agg(
    ["mean","max","min","std"]
)
17. Heatmap with Pivot Table
pivot = pd.pivot_table(
    df,
    values="Salary",
    index="Department",
    columns="Gender"
)

sns.heatmap(pivot, annot=True)
18. FacetGrid

Category অনুযায়ী separate plots।

Example
g = sns.FacetGrid(df, col="Gender")
g.map(sns.histplot, "Salary")
19. Multivariate Outlier Detection

কখনো single feature normal লাগে
কিন্তু multiple feature relation abnormal হতে পারে।

Example:

Low experience but huge salary
20. Feature Interaction

VERY IMPORTANT

কখনো:

Single feature weak
Combined features strong

Example:

Study hour alone weak
Study hour + attendance together strong
21. Interaction Example
Study Hour	Attendance	Result
High	High	Pass
High	Low	Fail

এখানে:

Interaction effect আছে
22. Crosstab Advanced
pd.crosstab(
    df["Gender"],
    df["Department"],
    margins=True
)
23. Correlation Matrix Deep Analysis
corr = df.corr()

sns.heatmap(corr, annot=True)

EDA expert এখানে খুঁজে:

Strong correlation
Negative relation
Multicollinearity
24. Multicollinearity (Basic Idea)

দুইটা feature খুব similar হলে।

Example:

Height in cm
Height in meter

দুটাই same information carry করে।

25. Real-world Example
Sales Dataset

Features:

Product
City
Season
Discount
Sales

Multivariate analysis detect করতে পারে:

কোন city তে কোন season এ sales বেশি
Discount effect কোথায় strongest
26. Common Beginner Mistakes
Mistake 1

Too many variables একসাথে দেখে confused হওয়া

Mistake 2

Only correlation দেখে decision নেওয়া

Mistake 3

Hue use না করা

Mistake 4

Pivot table ignore করা

27. Recommended Techniques
Situation	Best Tool
Many numerical features	Pairplot
Group comparison	Pivot table
Multi-category analysis	Groupby
Complex visualization	Hue
28. Full Practice Example
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

df = pd.read_csv("student.csv")

# Pairplot
sns.pairplot(df, hue="Gender")

# Pivot table
pd.pivot_table(
    df,
    values="Marks",
    index="Department",
    columns="Gender",
    aggfunc="mean"
)

# Advanced groupby
df.groupby(
    ["Department","Gender"]
)["Marks"].mean()

# Heatmap
sns.heatmap(df.corr(), annot=True)

plt.show()
29. EDA Expert Mindset

EDA expert multiple features দেখে:

Hidden pattern
Interaction
Group behavior
Segment differences
Feature redundancy
30. এই Step শেষে যা Clear হওয়া উচিত

তুমি এখন জানো:

Multivariate analysis
Pairplot
Hue
Pivot table
Advanced groupby
Feature interaction
Multi-dimensional analysis
Multicollinearity basics