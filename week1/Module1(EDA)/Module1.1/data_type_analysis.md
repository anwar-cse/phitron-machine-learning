# Data Types Analysis in EDA

    EDA তে সবচেয়ে important কাজগুলোর একটা হলো:

    Correct Data Type বোঝা

    কারণ datatype ভুল হলে:

        Analysis ভুল হবে
        Visualization problem হবে
        ML model issue করবে
        Memory waste হবে
        Statistics wrong আসবে

    1. Data Type কী?

        Data type বলে:

            Column এর data কী ধরনের

    Example:
        Column	Type
        Age	Integer
        Salary	Float
        Name	Text
        Date	Datetime

    2. Pandas এ Main Data Types
            Type	Meaning
            int64	Integer
            float64	Decimal number
            object	Text/String
            bool	True/False
            datetime64	Date & time
            category	Repeated 
            
    3. Data Type Check
        dtypes
         df.dtypes

    Example Output:

            Age          int64
            Salary     float64
            Name        object

    4. Detailed Information
        info()
            df.info()

    এটা দেখায়:

    Column names
    Non-null count
    Datatypes
    Memory usage

    5. Integer Type (int64)

    Whole number।

    Example:
        Age
        20
        25
        30

    6. Float Type (float64)

    Decimal number।

    Example:
        Salary
        25000.50
        18000.75

    7. Object Type

    Mostly text/string।

    Example:
            Name
            Rahim
            Karim

    8. Bool Type

        True / False

    Example:
            Passed
            True
            False

    9. Datetime Type

    Date related data।

    Example:
            Joining_Date
            2025-01-10

    10. Category Type

    Repeated category data।

    Example:
            Gender
            Male
            Female

    এটা memory efficient।

    11. Wrong Datatype Problem (VERY IMPORTANT)

    Real dataset এ datatype প্রায়ই ভুল থাকে।

    Example:
            Age
            "22"
            "25"

    এগুলো number হলেও string হিসেবে stored হতে পারে।

    12. কেন Wrong Datatype Dangerous?

    Example:
        df["Age"].mean()

    Error আসতে পারে যদি Age string হয়।

    13. String Number Problem

    Example:
        Salary
        "25000"
        "30000"

    দেখতে number
    কিন্তু actually text।

    14. Type Conversion
        astype()
            df["Age"] = df["Age"].astype(int)

    String → integer

    15. Float Conversion
        df["Salary"] = df["Salary"].astype(float)

    16. String Conversion
        df["ID"] = df["ID"].astype(str)

    17. Datetime Conversion (VERY IMPORTANT)
        to_datetime()
        df["Date"] = pd.to_datetime(df["Date"])

    Before:

        Date
        "2025-01-10"

        Type:

        object

    After:

        datetime64

    18. কেন Datetime Important?

    Datetime convert করলে:

        Year বের করা যায়
        Month বের করা যায়
        Time-series analysis করা যায়

    Example:

     df["Date"].dt.year

    19. Category Conversion
        df["Gender"] = df["Gender"].astype("category")

    20. Memory Optimization

        Category datatype memory কম খায়।

    Example:

        1 million rows gender column

        object → বেশি memory
        category → কম memory

    21. Numeric vs Categorical

    EDA তে এটা খুব important distinction।

        Numeric
        Age
        Salary
        Height

    Operations possible:

        Mean
        Median
        Correlation
        Categorical
        Gender
        City
        Department

    Operations:

        value_counts()
        countplot

    22. Continuous vs Discrete
        Continuous

        Infinite possible values

    Example:

        Height
        Weight
        Discrete

    Countable values

    Example:
        Student count

    23. Ordinal vs Nominal
        Nominal

        No order

        Example:
            Red / Blue / Green

        Ordinal
        Ordered category

        Example:
            Low / Medium / High

    24. Detecting Wrong Datatype

        EDA expert এই signs দেখে সন্দেহ করে:

            Sign	                Possible Problem
            Numeric column object	    Wrong type
            Date column object	        Need datetime
            Too many unique categories	Maybe ID
            0/1 column int	            Maybe bool

    25. Example Dataset Analysis
            Age	    Salary	    Date
            "22"	"25000"	    "2025-01-01"

    Current type:

        সব object

    Correct type:

        Age → int
        Salary → float
        Date → datetime

    26. Common EDA Type Workflow
        df.info()

        df["Age"] = df["Age"].astype(int)

        df["Date"] = pd.to_datetime(df["Date"])

        df["Gender"] = df["Gender"].astype("category")

    27. Common Beginner Mistakes
        Mistake 1

            Datatype check না করা

        Mistake 2

            Date কে string হিসেবেই রাখা

        Mistake 3

            Numeric string বুঝতে না পারা

        Mistake 4

            Category datatype use না করা

    28. EDA Expert Mindset

    EDA expert datatype দেখে immediately বুঝে:

            কোন analysis possible
            কোন graph use হবে
            কোন preprocessing লাগবে
            কোন ML model compatible

    29. Real-world Example
                Age object type

                Problem:

                "20" + "5"

                Output:

                "205"

                But numeric হলে:

                20 + 5

                Output:


                25
    30. এই Step শেষে যা Clear হওয়া উচিত

            Data types
            int / float / object
            datetime
            category
            bool
            astype()
            to_datetime()
            Wrong datatype detection
            Numeric vs categorical