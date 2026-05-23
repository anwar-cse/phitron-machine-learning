# Exploratory Data Analysis (EDA) এর Foundation

    Machine Learning এ EDA শেখার আগে সবচেয়ে গুরুত্বপূর্ণ হলো — data কী, dataset কীভাবে কাজ করে, আর data analysis mindset তৈরি করা।

    1. EDA কী?

    EDA = Exploratory Data Analysis

    মানে:
        ডাটাকে analyse করে বুঝা —
                            Data তে কী আছে
                            কোন pattern আছে কিনা
                            কোন সমস্যা আছে কিনা
                            কোন feature important
                            Missing value আছে কিনা
                            Outlier আছে কিনা
                            Data clean নাকি noisy
                            Machine Learning model দেওয়ার আগে কী preprocess করতে হবে

    EDA মূলত:

        “Model train করার আগে data কে বুঝার process”

    2. কেন EDA এত Important?

        Real world data কখনো clean হয় না।

        ধরো student result dataset:
                            Name	Study Hour	Attendance	Result
                            A	        5	          90	Pass
                            B	       NULL	          85	Pass
                            C	        20	          300	Fail

    এখানে problem:

        Missing value (NULL)
        Impossible value (Attendance = 300)
        Maybe outlier (Study Hour = 20)

    EDA ছাড়া model train করলে:

        Wrong prediction দিবে
        Accuracy কমবে
        Overfitting হতে পারে

    তাই:

    “Good model এর আগে good data দরকার।”

    3. EDA এর Main Goals

        EDA করার সময় সাধারণত এই জিনিসগুলো খুঁজা হয়:

                A. Data Understanding
                        Dataset এ কয়টা row/column?
                        কোন column numeric?
                        কোনটা categorical?
                B. Data Quality Check
                        Missing value
                        Duplicate
                        Wrong datatype
                        Noise
                C. Statistical Understanding
                        Mean
                        Median
                        Mode
                        Standard deviation
                D. Relationship Finding
                        Feature vs Target relation
                        Correlation
                E. Visualization
                        Histogram
                        Boxplot
                        Heatmap
                        Scatter plot

#  Full EDA Roadmap 
    Phase 1 - EDA introduction 
        Pandas + dataset loading 
        Missing values
        Duplicate data
        Data types fixing
        Basic data cleaning
    Phase 2 — Descriptive Statistics
        Mean / Median / Mode
        Variance / Standard deviation
        Percentile / Quartile
        Distribution understanding
        Skewness & kurtosis
    Phase 3 — Univariate Analysis
        Single column analysis
        Histogram
        Countplot
        Boxplot
        Density plot
    Phase 4 — Bivariate Analysis
        Numerical vs numerical
        Numerical vs categorical
        Categorical vs categorical
        Scatter plot
        Correlation analysis
        Heatmap
    Phase 5 — Multivariate Analysis
        Pairplot
        Feature interaction
        Crosstab
        Groupby analysis
        Pivot table
    Phase 6 — Data Cleaning for EDA
        Missing value handling
        Outlier detection
        IQR method
        Z-score method
        Duplicate handling
        String cleaning
    Phase 7 — Feature Understanding
        Feature distribution
        Feature importance intuition
        Cardinality
        Class imbalance
        Data leakage detection
    Phase 8 — Advanced EDA
        Advanced visualization
        Time-series EDA
        Correlation pitfalls
        Multicollinearity
        PCA intuition for EDA
    Phase 9 — Real-world EDA Projects
        Titanic dataset EDA
        House price EDA
        Sales dataset EDA
        Student performance EDA

# Missing Values Analysis in EDA

        EDA তে সবচেয়ে common এবং সবচেয়ে important problem হলো:
                                                                Missing Values

        Real-world dataset এ প্রায় সবসময় কিছু data missing থাকে।

        Example:
                Name	Age	    Salary
                A	    22	    25000
                B	    NULL	30000
                C	    25	    NULL

        এখানে:

        B এর Age missing
        C এর Salary missing

        1. Missing Value কী?

             কোনো cell এ data থাকে না।

        এগুলো বিভিন্নভাবে দেখা যায়:

        Representation
                NULL
                NaN
                None
                Blank
        2. কেন Missing Value হয়?

                Real world এ অনেক কারণ আছে:

                User form পূরণ করেনি
                Sensor error
                Database issue
                Data collection problem
                Manual entry mistake
        3. কেন Missing Value Dangerous?

        কারণ:

                ML model error দিতে পারে
                Wrong statistics আসতে পারে
                Visualization ভুল হতে পারে
                Bias create হতে পারে

        Example:
                Salary
                10000
                12000
                NULL

        Average calculate করলে problem হতে পারে।

        4. Missing Value Detect করার সবচেয়ে Important Function
                    isnull()
                    df.isnull()

        এটা boolean output দেয়।

        Example:
            Name	Age
            False	False
            False	True

            True = missing

        5. Column-wise Missing Count
            isnull().sum()
            df.isnull().sum()

        সবচেয়ে important command গুলোর একটা।

        Example Output:

                Column	Missing Count
                Age	    5
                Salary	2
        6. Missing Percentage বের করা

            EDA তে শুধু count না —
            percentage ও important।

            (df.isnull().sum() / len(df)) * 100

        Example:

            Column	Missing %
            Age	    5%
            Salary	20%

        7. Missing Value আছে কিনা দ্রুত Check
            df.isnull().any()

        Output:

        Age        True
        Salary     True
        Name      False

        8. Total Missing Values
            df.isnull().sum().sum()

        সব column মিলিয়ে total missing count।

        9. Missing Value Visualization

        EDA তে visual detection খুব useful।

            Basic heatmap:

                import seaborn as sns

                sns.heatmap(df.isnull())

            White/colored area দিয়ে missing value দেখা যায়।

        10. Missing Values এর Types
        A. Random Missing

            Randomly missing

            Example:

            কিছু user age দেয়নি

        B. Systematic Missing

            একটা pattern আছে

            Example:

            Female users salary field বেশি missing

            এটা dangerous।

        11. Missing Data Handle করার Main Strategies

            EDA তে missing data দেখার পর decision নিতে হয়।

        Main options:

                Strategy	Meaning
                Delete row	পুরো row remove
                Delete column	পুরো column remove
                Fill value	Missing জায়গা fill
                Predict value	ML দিয়ে predict

        12. Row Delete
            dropna()
            df.dropna()

            যেসব row তে missing আছে remove করবে।

        Before:

        Age	    Salary
        22	    20000
        NULL	30000

        After:

        Age	Salary
        22	20000

        13. Problem with dropna()

            Too much data হারিয়ে যেতে পারে।

        Example:

            40% row delete হয়ে গেল

            তাই blindly use করা dangerous।

        14. Specific Column Missing হলে Remove
            df.dropna(subset=["Age"])

        শুধু Age missing row remove হবে।

        15. Column Delete

            যদি একটা column এ খুব বেশি missing থাকে।

        Example:

            80% missing

        তখন:

            df.drop(columns=["Salary"])
            16. Missing Value Fill করা

        সবচেয়ে common strategy।

            fillna()
            df.fillna(0)

        সব missing 0 হবে।

        17. Mean দিয়ে Fill

            Numeric column এর জন্য common।

            df["Age"] = df["Age"].fillna(df["Age"].mean())

            Mean formula:

            Mean=∑x/n
            ​


        18. Median দিয়ে Fill

            Outlier থাকলে mean dangerous হতে পারে।

            তখন median better।

            df["Salary"] = df["Salary"].fillna(df["Salary"].median())

        19. Mode দিয়ে Fill

            Categorical data এর জন্য।

            df["Gender"] = df["Gender"].fillna(df["Gender"].mode()[0])
            
        20. Forward Fill

            আগের value দিয়ে fill।

            df.fillna(method="ffill")

        21. Backward Fill

            পরের value দিয়ে fill।

            df.fillna(method="bfill")

        22. কোন Strategy কখন Use হবে?
            Situation	                 Better Choice
            Few missing rows	            dropna()
            Numeric normal distribution 	mean
            Numeric with outlier	        median
            Categorical	                    mode
            Too many missing	            drop column

        23. Real EDA Thinking

            EDA expert শুধু fill করে না।

            সে প্রশ্ন করে:

            কেন missing?
            কোনো pattern আছে?
            Missing itself কি useful information?
            Column drop করা উচিত?
        24. Common Beginner Mistakes
        Mistake 1

            সব missing এ 0 fill করা

        Mistake 2

            Data distribution না দেখে mean use করা

        Mistake 3

            80% missing column রেখে দেওয়া

        Mistake 4

            Missing pattern ignore করা

        25. Full Practice Example
            import pandas as pd

            df = pd.read_csv("student.csv")

            # Missing check
            df.isnull().sum()

            # Percentage
            (df.isnull().sum()/len(df))*100

            # Fill missing age
            df["Age"] = df["Age"].fillna(df["Age"].mean())

            # Remove missing rows
            df.dropna()

            # Heatmap
            import seaborn as sns
            sns.heatmap(df.isnull())

        26. EDA Mindset (Very Important)

            EDA তে missing value মানে শুধু “empty cell” না।

        এটা হতে পারে:

            Data collection problem
            Business insight
            Human behavior
            Sensor issue

        Good analyst missing value কে investigate করে।

        27. এই Step শেষে যা Clear হওয়া উচিত
                            Missing value detect
                            isnull()
                            sum()
                            any()
                            dropna()
                            fillna()
                            mean/median/mode filling
                            Missing percentage
                            Missing visualization
                            Missing handling strategy