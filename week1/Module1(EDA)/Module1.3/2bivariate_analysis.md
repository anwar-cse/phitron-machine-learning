#  Bivariate Analysis in EDA

  Bivariate Analysis

  মানে:

    একসাথে ২টা variable/feature এর relationship analyse করা

  1. Bivariate Analysis কী?

    “Bi” = two

  মানে:

    দুইটা column এর relation বুঝা

  Example Questions
              Study Hour বাড়লে Marks বাড়ে?
              Salary এবং Experience related?
              Gender অনুযায়ী Salary change হয়?
              City অনুযায়ী Sales different?

  2. কেন Important?

  কারণ Machine Learning এ:

    Feature relation খুব important

  Bivariate analysis দিয়ে বুঝা যায়:

        Correlation
        Dependency
        Trend
        Pattern
        Interaction
        Note:
            | Term        | Simple Meaning                    |
            | ----------- | --------------------------------  |
            | Correlation | দুটো variable related কিনা         |
            | Dependency  | একটা অন্যটার উপর depend করে কিনা |
            | Trend       | সময়ের সাথে direction              |
            | Pattern     | repeated behavior                 |
            | Interaction | variables একসাথে effect করছে     |

  3. Main Goal
      Goal	              Example
      Relationship        detect	Height vs Weight
      Trend detect	      Experience vs Salary
      Dependency check	  Gender vs Purchase
      Correlation measure	Age vs Income

  4. Types of Bivariate Analysis
      Variable 1	Variable 2	Example
      Numerical	  Numerical	  Age vs Salary
      Numerical	  Categorical	Salary vs Gender
      Categorical	Categorical	Gender vs Purchased

  5. Numerical vs Numerical

  সবচেয়ে common type।

  Example:

    Height vs Weight
    Study hour vs Marks

  6. Scatter Plot 

  Numerical vs numerical relationship দেখার best graph।

  Example
    sns.scatterplot(x=df["Study_Hour"], y=df["Marks"])

  7. Scatter Plot কী দেখায়?
        Positive relation
        Negative relation
        No relation
        Outlier
        Clusters
              Note:
                Cluster মানে:

                একসাথে জড়ো হওয়া similar data points

                Scatter Plot এ যখন কিছু points group আকারে থাকে তখন তাকে cluster বলে।
                
  8. Positive Correlation

  একটা বাড়লে আরেকটাও বাড়ে।

  Example:

    Study hour ↑ → Marks ↑

        Visual idea:

              *
            *
          *
        *
        *
  9. Negative Correlation

  একটা বাড়লে আরেকটা কমে।

  Example:

    Price ↑ → Demand ↓

      Visual idea:

      *
        *
          *
            *
  10. No Correlation

  Random pattern।

  *    *
    *
  *      *

  11. Correlation

    Relationship strength measure করে।

  Range:

    −1≤r≤1

  12. Correlation Meaning
      Value	Meaning
      +1	  Perfect positive
      -1	  Perfect negative
       0	    No relation

  13. Correlation Calculate
    corr()
      df["Study_Hour"].corr(df["Marks"])
  14. Pearson Correlation Formula.........


  15. Correlation Matrix

  সব numerical column এর relation।

    df.corr()

  Example:

    Age	Salary

    Age	    1.0	0.7
    Salary	0.7	1.0

  16. Heatmap 

  Correlation visually দেখায়।

  Example
    sns.heatmap(df.corr(), annot=True)

  17. Heatmap কী দেখায়?
        Strong relation
        Weak relation
        Positive/negative relation

  18. Numerical vs Categorical

  Example:

    Salary vs Gender
    Marks vs Department

  19. Barplot

  Category অনুযায়ী average দেখায়।

  Example
    sns.barplot(x=df["Gender"], y=df["Salary"])

  20. Barplot কী দেখায়?

  Example:

    Male average salary বেশি?
    Female marks বেশি?

  21. Boxplot for Category Comparison
        sns.boxplot(x=df["Gender"], y=df["Salary"])

  এটা দেখায়:

      Spread
      Median
      Outlier
      Category comparison

  22. Categorical vs Categorical

  Example:

    Gender vs Purchased
    City vs Product

  23. Crosstab
        Crosstab হলো:

        দুইটা categorical variable এর frequency table
    Most important technique।

      pd.crosstab(df["Gender"], df["Purchased"])

  Example Output:

    Gender	Yes	No
    Male	  50	20
    Female	30	40

  24. Groupby 

  EDA তে extremely important।

  Example
    df.groupby("Gender")["Salary"].mean()

  Output:

    Gender	Avg Salary
    Male	  30000
    Female	25000

  25. Multiple Aggregation
      df.groupby("Department")["Salary"].agg(["mean","max","min"])

  26. Pairplot

            Pairplot হলো:

            সব numerical feature relation একসাথে দেখানো graph collection

            এটা automatically:

            scatterplot
            histogram
            relationship

            সব দেখায়।

  সব numerical feature relation একসাথে।

      sns.pairplot(df)

  27. Relationship vs Causation

  Correlation ≠ causation

  Example:

    Ice cream sales ↑
    Drowning ↑

  মানে এই না যে:

      Ice cream drowning cause করছে

      Actually:

      Summer season দুটাকেই increase করছে।

      Note:
              Relationship কী?

              Relationship মানে:

              দুইটা variable এর মধ্যে connection বা relation আছে
              Example
                Study Hour ↑ → Marks ↑

              মানে:

              পড়াশোনা বাড়লে marks বাড়ছে
              relation আছে

              2. Causation কী?

              Causation মানে:

              একটা variable সরাসরি আরেকটার কারণ
              Example
                 Smoking → Lung Cancer

              এখানে:

              smoking cause করছে
              এটা causation

  28. Outlier Effect on Correlation

    একটা extreme outlier পুরো correlation change করতে পারে।

  29. Real-world EDA Questions

  EDA expert জিজ্ঞেস করে:

      কোন feature target এর সাথে strongly related?
      কোন feature redundant?
      Multicollinearity আছে?
      Non-linear pattern আছে?

  30. Common Beginner Mistakes
  Mistake 1

    Correlation = causation ভাবা

  Mistake 2

    Only numeric relation দেখা

  Mistake 3

    Scatterplot ছাড়া correlation বুঝার চেষ্টা

  Mistake 4

    Outlier ignore করা

  31. Recommended Graphs
      Type	Best Graph
      Num vs Num	Scatterplot
      Num vs Cat	Barplot / Boxplot
      Cat vs Cat	Crosstab

  32. Full Practice Example
          import pandas as pd
          import seaborn as sns
          import matplotlib.pyplot as plt

          df = pd.read_csv("student.csv")

          # Scatterplot
          sns.scatterplot(x=df["Study_Hour"], y=df["Marks"])

          # Correlation
          df["Study_Hour"].corr(df["Marks"])

          # Heatmap
          sns.heatmap(df.corr(), annot=True)

          # Barplot
          sns.barplot(x=df["Gender"], y=df["Marks"])

          # Crosstab
          pd.crosstab(df["Gender"], df["Result"])

          plt.show()
  33. learn summary:

        Bivariate analysis
        Scatterplot
        Correlation
        Heatmap
        Barplot
        Crosstab
        Groupby
        Pairplot
        Relationship analysis