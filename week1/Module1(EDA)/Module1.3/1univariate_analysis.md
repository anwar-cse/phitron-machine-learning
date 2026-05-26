# Univariate Analysis in EDA

    Univariate Analysis

    মানে:

        একবারে শুধুমাত্র ১টা feature/column analyse করা

    1. Univariate Analysis কী?

    “Uni” = one
        মানে:

        Single variable analysis

    Example:

        শুধু Age column analyse
        শুধু Salary column analyse

    2. কেন Important?

    কারণ এটা দিয়ে বুঝা যায়:

        Distribution কেমন
        Outlier আছে কিনা
        Missing আছে কিনা
        Skewed কিনা
        Feature useful কিনা

    3. Univariate Analysis এর Main Goals
        Goal	            Example
        Distribution বুঝা	    Salary spread
        Outlier detect	       Extremely high value
        Frequency বুঝা	        Gender count
        Pattern detect	       Common ranges

    4. দুই ধরনের Univariate Analysis
        Type	        Example
        Numerical	    Age, Salary
        Categorical	    Gender, City

    5. Numerical Column Analysis

    ধরো:
        Age
        20
        22
        25
        60

    আমরা জানতে চাই:

        Average কত
        Spread কেমন
        Outlier আছে কিনা

    6. Categorical Column Analysis

    ধরো:
        Gender
        Male
        Female
        Male

    আমরা জানতে চাই:

        কোন category বেশি
        Imbalance আছে কিনা

    7. Univariate Analysis Workflow
                        Select Column
                            ↓
                        Check Datatype
                            ↓
                        Check Missing
                            ↓
                        Check Statistics
                            ↓
                        Visualize
                            ↓
                        Find Insights

    8. Histogram 

        Histogram numerical data distribution দেখায়।

    Example
        import seaborn as sns

        sns.histplot(df["Age"])

    9. Histogram কী দেখায়?
            কোন range এ বেশি data
            Distribution symmetric কিনা
            Skew আছে কিনা
            Multiple peaks আছে কিনা

    10. Histogram Intuition
        Symmetric Distribution
                *
                *****
            *********
                *****
                *

    Mean ≈ Median

    Right Skew
        *******
        *****
        ***
        **
        *

    Large values ডানদিকে tail তৈরি করে।

    11. Bins কী?

    Histogram এ bins মানে:

        Group/range

    Example:

        0–10
        10–20
        20–30

    Custom bins
        sns.histplot(df["Age"], bins=20)

    12. KDE Plot

        Distribution smooth curve দিয়ে দেখায়।

    KDE = Kernel Density Estimation
        sns.kdeplot(df["Age"])

    13. Histogram + KDE

    সবচেয়ে common combination।

        sns.histplot(df["Age"], kde=True)

    14. Countplot

        Categorical column analysis এর জন্য।

    Example
        sns.countplot(x=df["Gender"])

    15. Countplot কী দেখায়?
        কোন category বেশি
        Class imbalance আছে কিনা

    Example:

        Gender	Count
        Male	90
        Female	10

    এটা imbalance হতে পারে।

    16. value_counts() vs Countplot
            value_counts()
            df["Gender"].value_counts()

        Numeric output দেয়।

    countplot()
        Visual output দেয়।

    17. Boxplot 

    Outlier detect করার জন্য সবচেয়ে important graph।

    Example
        sns.boxplot(x=df["Salary"])

    18. Boxplot Parts

    Boxplot এ থাকে:

        Part	    Meaning
        Box	Middle  50% data
        Line inside	Median
        Whiskers	Normal range
        Dots	    Outliers

    19. IQR 

        Boxplot IQR use করে।

    Formula:

        IQR=Q3−Q1

    20. Outlier Rule

    Outlier usually:

        x<Q1−1.5(IQR)or x>Q3+1.5(IQR)

    21. Example Outlier
        10, 12, 13, 14, 500

        500 = outlier

    22. Pie Chart 
            Categorical percentage দেখায়।

            df["Gender"].value_counts().plot.pie()

    কিন্তু EDA তে অনেক সময় countplot better।

    23. Distplot (Old)

    আগে use হতো:

        sns.distplot(df["Age"])

    এখন deprecated।

    24. Numerical Feature Questions

    EDA expert numerical feature দেখে জিজ্ঞেস করে:

        Distribution normal?
        Skewed?
        Outlier আছে?
        Spread বেশি?
        Negative value valid?

    25. Categorical Feature Questions
        Dominant category কোনটা?
        Rare category আছে?
        Imbalance আছে?
        Typo আছে?

    26. Real-world Example
    Salary Column

    Possible insights:

        Most people medium salary
        Few people extremely rich
        Right skewed distribution
        Outliers present

    27. Common Beginner Mistakes
    Mistake 1

        সব graph blindly use করা

    Mistake 2

        Datatype অনুযায়ী graph না choose করা

    Mistake 3

        Outlier ignore করা

    Mistake 4

        Countplot ছাড়া categorical analysis করা

    28. Recommended Graphs
        Data Type	Best Graph
        Numerical	Histogram
        Numerical	Boxplot
        Numerical	KDE
        Categorical	Countplot

    29. Full Practice Example
            import pandas as pd
            import seaborn as sns
            import matplotlib.pyplot as plt

            df = pd.read_csv("student.csv")

            # Histogram
            sns.histplot(df["Age"], kde=True)

            # Boxplot
            sns.boxplot(x=df["Salary"])

            # Countplot
            sns.countplot(x=df["Gender"])

            plt.show()

    30. EDA Expert Mindset

    EDA expert graph দেখে instantly বুঝতে চেষ্টা করে:

        Shape
        Spread
        Skew
        Outlier
        Balance
        Data quality

#                   NOTE
                        Histogram
                        KDE Plot
                        Histogram + KDE
                        Boxplot
                        Countplot
                        Pie Chart
                        Value Counts Plot
                        Distplot (পুরাতন)

                        1. Histogram
                        কী?
                            Histogram numerical data এর distribution দেখায়।

                        মানে:

                            ডাটা কোন range এ বেশি আছে সেটা দেখায়।

                        Example:

                            Student marks:

                            marks = [40,45,50,55,60,65,70,75,80]

                        Histogram bars দিয়ে দেখাবে কোন marks কতবার এসেছে।

                        Example
                            import seaborn as sns
                            import matplotlib.pyplot as plt

                            sns.histplot(data=df, x="Age")

                            plt.show()
                        কী দেখায়?
                            Data spread
                            Most common values
                            Skewness
                            Outliers
                            Distribution shape
                        কোথায় ব্যবহার করবো?

                        যখন numerical column থাকবে:

                            Age
                            Salary
                            Height
                            Marks
                            Price
                        কেন ব্যবহার করবো?

                        কারণ এটা quickly বুঝায়:

                            data evenly spread কিনা
                            data normal কিনা
                            কোন range এ বেশি value আছে
                        
                        2. KDE Plot
                        কী?

                        KDE = Kernel Density Estimation

                            এটা histogram এর smooth version।

                        Bars না দেখিয়ে smooth curve দেখায়।

                        Example
                            sns.kdeplot(data=df, x="Salary")

                            plt.show()
                        কী বুঝায়?
                            Data density
                            Distribution shape
                            Peaks কোথায়
                        কোথায় ব্যবহার করবো?

                        Numerical data এর distribution বুঝতে।

                        কেন ব্যবহার করবো?

                            Histogram এ bars থাকে।

                            KDE smooth curve দেয় তাই pattern clearer হয়।

                        3. Histogram + KDE
                        কী?

                        একসাথে Histogram + KDE দেখানো।

                        সবচেয়ে বেশি ব্যবহার হয়।

                        Example
                            sns.histplot(data=df, x="Salary", kde=True)

                            plt.show()
                        সুবিধা

                        একসাথে পাওয়া যায়:

                            bars
                            smooth distribution curve
                        কোথায় ব্যবহার করবো?

                        Distribution analyse করার best option।

                        কেন?

                        কারণ:

                            Histogram frequency দেখায়
                            আর KDE trend দেখায়।

                    
                        4. Boxplot
                        কী?

                            Boxplot data এর summary দেখায়।

                        এটা দেখায়:

                            Median
                            Quartiles
                            Outliers
                        Example
                            sns.boxplot(data=df, x="Salary")

                            plt.show()

                        কী বুঝায়?
                            Outliers আছে কিনা
                            Spread
                            Skewness
                            Median

                        কোথায় ব্যবহার করবো?

                            Outlier detection এর জন্য best।

                        কেন?

                        কারণ easily unusual values ধরা যায়।

                        Boxplot Components
                            Middle line → Median
                            Box → Q1 to Q3
                            Whiskers → normal range
                            Dots → outliers
                        
                        5. Countplot
                        কী?

                        Categorical data count দেখায়।

                        Example
                            sns.countplot(data=df, x="Gender")

                            plt.show()
                        কী বুঝায়?

                        প্রতিটি category কতবার আছে।

                        Example:

                            Male = 300
                            Female = 200

                        কোথায় ব্যবহার করবো?

                        Categorical column এ:

                            Gender
                            City
                            Department
                            Product Type
                        কেন?

                        Frequency comparison সহজ হয়।

                        
                        6. Pie Chart
                        কী?

                         Percentage আকারে data দেখায়।

                        Example
                            df["Gender"].value_counts().plot.pie(autopct="%1.1f%%")
                        কী বুঝায়?

                        Category proportion।

                        কোথায় ব্যবহার করবো?

                            যখন percentage comparison দরকার।

                        কেন?

                            Quick percentage understanding।

                        Problem

                        Too many categories হলে confusing হয়।

                        Best Practice

                            ৫-৬ category এর বেশি না।

                    
                        7. Value Counts Plot
                        কী?

                        value_counts() দিয়ে category count বের করে plot করা।

                        Example
                            df["Gender"].value_counts().plot(kind="bar")
                        কী বুঝায়?

                            Countplot এর মতোই category frequency দেখায়।

                        Countplot vs Value Counts Plot

                        Countplot	            Value Counts Plot
                        Seaborn	                    Pandas
                        সুন্দর visualization	      Simple
                        More customizable	        দ্রুত

                        কোথায় ব্যবহার করবো?

                            Quick analysis এ।

                        কেন?

                            Fast and simple।

                
                        8. Distplot (Deprecated)
                        কী?

                            আগে distribution দেখানোর জন্য ব্যবহার হতো।

                            এখন deprecated।

                        Old Example
                            sns.distplot(df["Age"])

                        এখন কী ব্যবহার করবো?

                        Instead use:

                             sns.histplot(df["Age"], kde=True)

                        কেন deprecated?

                        কারণ:

                        functionality confusing ছিল
                        histplot + kdeplot better

                        কোনটা কখন ব্যবহার করবো?
                        Plot	            Data Type	Main Use
                        Histogram	        Numerical	Distribution
                        KDE Plot	        Numerical	Smooth distribution
                        Histogram + KDE	    Numerical	Best distribution analysis
                        Boxplot	            Numerical	Outlier detection
                        Countplot	        Categorical	Frequency count
                        Pie Chart	        Categorical	Percentage
                        Value Counts Plot	Categorical	Quick count
                        Distplot	        Numerical	Old method

                        খুব Important Shortcut
                        Numerical Data হলে

                        Use:

                            Histogram
                            KDE
                            Boxplot
                            Categorical Data হলে

                        Use:

                            Countplot
                            Pie Chart
                            Real Life Example

                        Situation	            Best Plot
                        Salary distribution	    Histogram
                        Smooth salary trend	    KDE
                        Outlier salary detect	Boxplot
                        Male vs Female count	Countplot
                        Percentage share	    Pie Chart
                        Quick category count	value_counts plot