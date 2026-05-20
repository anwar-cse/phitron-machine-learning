# Duplicate Data Analysis in EDA

    EDA তে আরেকটা খুব common problem হলো:

    Duplicate Data

        মানে একই data একাধিকবার থাকা।

    1. Duplicate Data কী?

    Example:

            ID	Name	Salary
            1	Rahim	25000
            2	Karim	30000
            2	Karim	30000

    এখানে দ্বিতীয় এবং তৃতীয় row একই।

    এটাই duplicate।

    2. কেন Duplicate Dangerous?

    Duplicate data থাকলে:

        Statistics ভুল হয়
        Average ভুল হয়
        ML model bias হয়
        Wrong business insight আসে

    Example:

        Salary
        10000
        10000
        50000

    একটা duplicate average কে change করতে পারে।

    3. Duplicate কেন হয়?

    Real-world এ:

        Database merge
        Multiple form submission
        System bug
        Manual entry
        Data scraping issue

    4. Duplicate Detect করার Main Function
            duplicated()
            df.duplicated()

    Output:

        Row	Duplicate?
        0	False
        1	False
        2	True

    True = duplicate row

    5. Duplicate Rows Count
        df.duplicated().sum()

    Example Output:

    15

    মানে:

        15টা duplicate row আছে

    6. Duplicate Rows দেখানো
        df[df.duplicated()]

        এটা duplicate rows display করবে।

    7. Duplicate Remove করা
        drop_duplicates()
        df.drop_duplicates()

    Duplicate remove করবে।

    Before:

        ID	Name
        1	A
        1	A

    After:

        ID	Name
        1	A

    8. Permanentভাবে Save করা
        df = df.drop_duplicates()

    9. Specific Column Based Duplicate

        সবসময় পুরো row same হয় না।

    Example:

        ID	Email
        1	a@gmail.com
        2	a@gmail.com

    এখানে Email duplicate।

    subset use করা
         df.duplicated(subset=["Email"])

    10. Multiple Column Based Duplicate
        df.duplicated(subset=["Name", "Phone"])

    11. First Duplicate vs All Duplicate

    Default:

    প্রথম row keep হয়
    পরেরগুলো duplicate ধরা হয়

    Example:

        Row	Value
        0	A
        1	A
        2	A

    Output:

        Row	Duplicate
        0	False
        1	True
        2	True

    12. keep Parameter
            keep='first'

            Default behavior

            df.duplicated(keep='first')
            keep='last'

    শেষটা keep করবে।

            df.duplicated(keep='last')
            keep=False

    সব duplicate True হবে।

            df.duplicated(keep=False)

    13. Duplicate Remove না করে Analyze করা

        EDA expert সবসময় remove করার আগে analyse করে।

        কারণ:

        Duplicate itself হতে পারে important information

    Example:

    Same customer multiple purchases করেছে

        এটা duplicate না —
        এটা valid repeated transaction।

    14. Exact Duplicate vs Logical Duplicate
        Exact Duplicate

        সব column same

    Logical Duplicate

    Example:

        Name	    Phone
        Rahim	    01711
        Rahim Hasan	01711

    Technically different
    But logically same person।

    15. Fake Duplicate Problem

    Example:

            Customer	Product
            A	         Laptop
            A	         Mouse

    এটা duplicate না।

    একই customer multiple product কিনতে পারে।

    16. Real-world EDA Thinking

    Duplicate detect করার আগে প্রশ্ন:

        Row কি transaction?
        Row কি customer?
        Row কি event?
        Same entry repeat valid নাকি invalid?

    17. Duplicate Visualization Idea

    Category count suddenly খুব বেশি হলে duplicate suspect করা যায়।

    Example:

        df["Country"].value_counts()

    18. Duplicate + Dataset Shape

    Before remove:

        df.shape

    Example:

        (1000, 5)

    After remove:

        .drop_duplicates().shape

    Output:

        (950, 5)

    মানে:

        50 duplicate ছিল

    19. Important Practice Example

            import pandas as pd

            df = pd.read_csv("data.csv")

            # Count duplicates
            df.duplicated().sum()

            # Show duplicates
            df[df.duplicated()]

            # Remove duplicates
            df = df.drop_duplicates()

            # Check new shape
            df.shape

    20. Common Beginner Mistakes
        Mistake 1

            সব repeated row কে duplicate ভাবা

        Mistake 2

            Business logic না বুঝে remove করা

        Mistake 3

            subset use না করা

        Mistake 4

            Duplicate remove করার আগে backup না রাখা

    21. EDA Expert Mindset

        EDA expert শুধু code চালায় না।

    সে বুঝতে চায়:

        Duplicate কেন?
        System error?
        Fraud?
        Data entry issue?
        Real repeated event?
        22. Missing vs Duplicate
        Problem	Meaning
        Missing	Data নেই
        Duplicate	একই data repeated

    23. Full Cleaning Flow (Till Now)
                Load Data
                ↓
                head()
                ↓
                info()
                ↓
                Missing Check
                ↓
                Duplicate Check
                ↓
                Cleaning

    24. এই Step শেষে যা Clear hovo:
                Duplicate কী
                duplicated()
                drop_duplicates()
                subset
                keep parameter
                Exact vs logical duplicate
                Business logic importance

#                           Note 
                        keep Parameter কী?

                            duplicated() function এ keep parameter বলে দেয়:

                        কোন row কে original (keep) ধরা হবে
                        আর কোনগুলো duplicate হবে।

                        Example Dataset
                                import pandas as pd

                                data = {
                                    "Name": ["A", "A", "A", "B"]
                                }

                                df = pd.DataFrame(data)

                                print(df)

                        Output:

                                Index	Name
                                0	    A
                                1	    A
                                2	    A
                                3	    B

                        এখানে:
                            A তিনবার আছে

                        1. keep='first' (Default)
                        df.duplicated(keep='first')

                        Output:

                            Index	Result
                            0	    False
                            1	    True
                            2	    True
                            3	    False
                        Explanation

                        প্রথম A কে original ধরা হয়েছে।

                        তাই:

                        Index 0 → False
                        বাকিগুলো → True

                        Visualization
                                    A   ← original
                                    A   ← duplicate
                                    A   ← duplicate
                                    2. keep='last'

                        df.duplicated(keep='last')

                        Output:

                                Index	Result
                                0	    True
                                1	    True
                                2	    False
                                3	    False
                        Explanation

                        এবার শেষ A কে original ধরা হয়েছে।

                        তাই:

                        শেষটা False
                        আগেরগুলো True
                        Visualization
                                A   ← duplicate
                                A   ← duplicate
                                A   ← original

                        3. keep=False
                        df.duplicated(keep=False)

                        Output:

                                Index	Result
                                0	    True
                                1	    True
                                2	    True
                                3	    False
                        Explanation

                        এখানে কোনোটাকেই original ধরা হয়নি।

                        যতগুলো duplicate group এ আছে —
                        সবগুলোকে True করা হয়েছে।

                        Visualization
                                A   ← duplicate
                                A   ← duplicate
                                A   ← duplicate
                        Real Meaning
                        keep Value	Meaning
                        'first'	প্রথমটা keep করবে
                        'last'	শেষটা keep করবে
                        False	সব duplicate mark করবে