# Descriptive Statistics in EDA

	EDA তে data বুঝার সবচেয়ে powerful অংশগুলোর একটা হলো:

		Descriptive Statistics

	এগুলো data এর summary দেয়।

	মানে:

		Average কত
		Data spread কেমন
		Extreme values আছে কিনা
		Distribution balanced নাকি skewed(=>Data distribution একদিকে বেশি ঝুঁকে থাকা বা অসম হওয়া।)

	1. কেন Descriptive Statistics Important?

	ধরো দুইটা class আছে:

		Class A Marks
		70, 72, 71, 73, 74

		Class B Marks
		20, 40, 70, 90, 130

	দুইটার average same হতে পারে।
	কিন্তু distribution completely different।

	তাই শুধু average যথেষ্ট না।

	2. Main Statistical Measures

	EDA তে সবচেয়ে important:

			Measure				কাজ
			Mean				Average
			Median				Middle value
			Mode				Most frequent
			Variance			Spread
			Standard deviation	Dispersion
			Percentile			Relative position
			Quartile			Data division

	3. Mean (Average)

	সব value এর average।

	Formula:

		Mean=∑x/n
		​

	Example

		Values:

		10, 20, 30

		Calculation:

		(10 + 20 + 30) / 3 = 20
		Pandas Code
			df["Marks"].mean()

	4. Mean Problem (Outlier Sensitive)

	Example:

		10, 12, 15, 18, 500

		Mean অনেক increase হয়ে যাবে।

		কারণ:

			Outlier effect

	5. Median

			Sorted data এর middle value।

			Example
				10, 20, 30

				Median = 20

			Even Count Example
				10, 20, 30, 40

				Median:

				Median=(20+30)/2
				Result = 25

			Pandas Code
				df["Marks"].median()

	6. কেন Median Important?

	Outlier থাকলে median better।

	Example:

		10, 12, 15, 18, 500

	Median = 15
	Much more realistic।

	7. Mode

	Most frequent value।

	Example
		10, 20, 20, 30

	Mode = 20

	Pandas Code
		df["City"].mode()

	8. Mean vs Median vs Mode
	Measure	Best For
			Mean	Normal distribution
			Median	Outlier data
			Mode	Categorical data

	9. Variance

	Data কত spread হয়েছে measure করে।

	Low variance:

		Data close together

	High variance:

		Data widely spread

	Formula: ......


	10. Standard Deviation

	Variance এর square root।

	সবচেয়ে important spread measure।

	Formula:...

	11. Standard Deviation Intuition
		Low Standard Deviation
		48, 49, 50, 51, 52

		সব কাছাকাছি।

		High Standard Deviation
		10, 30, 50, 70, 90

		অনেক spread।

		Pandas Code
			df["Marks"].std()

	12. Variance Code
		df["Marks"].var()

	13. Min & Max
		df["Marks"].min()

		df["Marks"].max()

	14. Range

		Difference between max and min।

		Formula:

			Range=Max−Min

	15. Percentile

	Percentile বলে:

	কত percent data এর নিচে আছে

	Example

		90th percentile মানে:

		90% data এর নিচে
		Pandas Code
			df["Marks"].quantile(0.90)

	16. Quartile

		Data কে 4 ভাগে divide করে।

		Quartile	Meaning
		Q1	25%
		Q2	50% (Median)
		Q3	75%
		Code
			df["Mark	s"].quantile([0.25, 0.50, 0.75])
			
	17. Interquartile Range (IQR)

	Outlier detection এ খুব important।

	Formula:

		IQR=Q3−Q1

	18. describe() আবার Important কেন?
		df.describe()

	এটা automatically দেয়:
						count
						mean
						std
						min
						max
						quartiles

	19. Distribution Understanding

	EDA তে analyst প্রশ্ন করে:

		Data symmetric?
		Outlier আছে?
		Spread বেশি?
		Mean ≈ median?

	20. Skewness Intuition (Basic)
		Right Skew
			10, 12, 15, 18, 200

	Mean > Median

		Left Skew
			2, 3, 4, 5, 100

	(Actually right skew example again — later properly শিখবো)

	21. Real-world Example
		Salary Dataset

	Most people:

	Medium salary

	Few people:

	Extremely high salary

	তাই:

		Salary distribution usually right-skewed

	Median বেশি meaningful হয়।

	22. Common Beginner Mistakes
	Mistake 1

		Mean blindly use করা

	Mistake 2

		Outlier ignore করা

	Mistake 3

		Spread না দেখা

	Mistake 4

		Only describe() দেখে analysis শেষ করা

	23. EDA Expert Mindset

	EDA expert statistics দেখে instantly বুঝে:

		Data stable নাকি noisy
		Outlier আছে কিনা
		Distribution balanced কিনা
		Scaling লাগবে কিনা

	24. Full Practice Example
			import pandas as pd

			df = pd.read_csv("student.csv")

			df["Marks"].mean()

			df["Marks"].median()

			df["Marks"].mode()

			df["Marks"].std()

			df["Marks"].var()

			df["Marks"].min()

			df["Marks"].max()

			df["Marks"].quantile([0.25,0.50,0.75])

			df.describe()

	25. learn summary:
					Mean
					Median
					Mode
					Variance
					Standard deviation
					Percentile
					Quartile
					IQR
					Distribution intuition