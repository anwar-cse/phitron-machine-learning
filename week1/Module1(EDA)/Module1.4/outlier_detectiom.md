# Outlier Detection and Treatment in EDA

    EDA তে সবচেয়ে important এবং tricky topic গুলোর একটা হলো:

    Outlier

    কারণ outlier:

        Statistics নষ্ট করতে পারে
        ML model ভুল train করতে পারে
        Visualization distort করতে পারে
        Business insight misleading করতে পারে
    1. Outlier কী?

    Outlier হলো:

        এমন data point যা অন্য data থেকে অনেক দূরে

    Example
        10, 12, 14, 15, 16, 500

    এখানে:

        500 = outlier

    2. কেন Outlier হয়?

    Real-world এ অনেক কারণ:

                Cause	            Example
                Data entry mistake	Age = 500
                Sensor error	    Temperature = -999
                Fraud	            Unusual transaction
                Rare event	        Billionaire salary
                Natural variation	Extremely talented student
    3. Outlier কেন Dangerous?

    Example:

        10, 12, 14, 15, 500

    Mean অনেক বড় হয়ে যাবে।

    Formula:
        Mean=∑x/n

    4. Outlier সবসময় Bad না

    VERY IMPORTANT

    কখনো outlier:

        Valuable information

    Example:

        Fraud detection
        Cyber attack
        Rare disease
        VIP customer

    তাই blindly remove করা dangerous।

    5. Outlier Detection Methods

    Main methods:

            Method	        Best For
            Boxplot	        Quick visual
            IQR	            Skewed data
            Z-score	        Normal distribution
            Scatterplot	    Relationship outlier

    6. Boxplot দিয়ে Outlier Detection

    সবচেয়ে common visual method।

        sns.boxplot(x=df["Salary"])

    7. Boxplot Review
            Part	Meaning
            Box	    Middle 50%
            Line	Median
            Dots	Outliers

    8. IQR Method 

    Most important practical method।

            Step 1 — Quartile বের করা
            Q1 = df["Salary"].quantile(0.25)

            Q3 = df["Salary"].quantile(0.75)

    9. IQR Formula

        IQR=Q3−Q1

    Code
        IQR = Q3 - Q1

    10. Lower & Upper Bound

    Formula:
        Lower Bound=Q1−1.5(IQR)

        Upper Bound=Q3+1.5(IQR)

    Code
        lower = Q1 - 1.5 * IQR

        upper = Q3 + 1.5 * IQR

    11. Outlier Detect করা
        outliers = df[
            (df["Salary"] < lower) |
            (df["Salary"] > upper)
        ]

    12. Outlier Remove করা
        df = df[
            (df["Salary"] >= lower) &
            (df["Salary"] <= upper)
        ]

    13. Z-Score Method

        Normal distribution এর জন্য useful।

    14. Z-score কী?

    একটা value mean থেকে কত standard deviation দূরে।

    Formula:
             z=>...

    15. Z-score Intuition
            Z-score	Meaning
            0	    Mean এর কাছে
            1	    1 std away
            3	    Very far

    16. Common Rule

    Usually:

         |z| > 3

    → possible outlier

    17. Z-score Code
        from scipy.stats import zscore

        df["zscore"] = zscore(df["Salary"])

    18. Outlier Filter with Z-score
        df[df["zscore"].abs() > 3]

    19. IQR vs Z-score
        Method	Better For
        IQR	    Skewed data
        Z-score	Normal distribution

    20. Scatterplot দিয়ে Outlier

    Relationship outlier detect করা যায়।

    sns.scatterplot(
        x=df["Experience"],
        y=df["Salary"]
    )

    Example:

        Low experience কিন্তু huge salary

    21. Outlier Treatment Strategies
        Strategy	Meaning
        Remove	    Delete outlier
        Cap	        Limit value
        Transform	Log transform
        Keep	    Business important

    22. Capping / Winsorization

    Extreme value limit করা।

    Example:

        500 → 100
    Code Idea
        df["Salary"] = df["Salary"].clip(lower, upper)

    23. Log Transformation

        Right-skewed data normalize করতে।

    Formula:

        y=log(x)
    Code
        import numpy as np

        df["Salary"] = np.log(df["Salary"])

    24. When NOT to Remove Outlier

    VERY IMPORTANT

    Do NOT remove if:

        Fraud detection
        Cybersecurity anomaly
        Rare disease
        VIP customer analysis
        Genuine rare events

    25. Real-world Example
        Banking Fraud

        Most transaction:

            100–5000

        One transaction:

            5 million

        এটা outlier
        কিন্তু very important।

    26. Distribution Before & After

    EDA expert সবসময় compare করে:

        Before cleaning
        After cleaning

    27. Common Beginner Mistakes
    Mistake 1

        সব outlier remove করা

    Mistake 2

        Business logic ignore করা

    Mistake 3

        Skewed data তে Z-score use করা

    Mistake 4

        Visualization ছাড়া outlier remove করা

    28. Recommended Workflow
                        Visualize
                        ↓
                        Understand Business Context
                        ↓
                        Choose Detection Method
                        ↓
                        Detect Outliers
                        ↓
                        Decide Treatment
                        ↓
                        Recheck Distribution

    29. Full Practice Example
                import pandas as pd
                import seaborn as sns

                df = pd.read_csv("salary.csv")

                # Boxplot
                sns.boxplot(x=df["Salary"])

                # IQR
                Q1 = df["Salary"].quantile(0.25)
                Q3 = df["Salary"].quantile(0.75)

                IQR = Q3 - Q1

                lower = Q1 - 1.5 * IQR
                upper = Q3 + 1.5 * IQR

                # Detect
                outliers = df[
                    (df["Salary"] < lower) |
                    (df["Salary"] > upper)
                ]

                # Remove
                df = df[
                    (df["Salary"] >= lower) &
                    (df["Salary"] <= upper)
                ]

    30. EDA Expert Mindset

    EDA expert outlier দেখে ভাবে:

        Error?
        Fraud?
        Rare event?
        Business insight?
        Important anomaly?
    31. এই Step শেষে যা Clear হওয়া উচিত

                                    Outlier
                                    IQR method
                                    Z-score
                                    Boxplot analysis
                                    Winsorization
                                    Log transformation
                                    Outlier removal strategy
                                    Business-aware outlier handling