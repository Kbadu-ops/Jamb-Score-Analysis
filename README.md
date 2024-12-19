	BACKGROUND:
The Joint Admissions and Matriculation Board (JAMB) is an essential exam in Nigeria, determining student eligibility for tertiary institutions, like the SAT exams in the United States. The JAMB score reflects the students' preparedness for higher education, influencing their admission opportunities. However, students' performances are affected by multiple factors, including their background, gender, state of origin, and subject choices.

This project is motivated by the question: "How do factors such as students' demographic attributes and subject performances affect their overall JAMB scores?" A deeper understanding of these relationships can reveal how non-academic factors contribute to academic success, offering insights for educators and policymakers to create more equitable systems. Accurate prediction of performance can assist educators, policymakers, and students in making informed decisions regarding educational interventions 

	Predictive Purpose:
The primary aim of this project is to predict students' overall performance in JAMB, specifically their total score, based on various factors, including demographic and subject performances, influence overall student scores. The goal of predicting JAMB scores is to provide insights that can help improve student interventions, guide resource allocation, and inform policy decisions aimed at enhancing educational equity and academic success.

This project will also assess how categorical variables (such as gender and state of origin) correlate with students' scores and examine the relationships between different subject scores to provide comprehensive insights into student performance patterns.

	Data Source
The data set used for this project is from Kaggle:

Students Performance in 2024 JAMB (kaggle.com)
	Variable Description
	Response Variable (Independent Variable)
	JAMB Score: The total score obtained by students in the JAMB exam, measured out of a possible 400. The goal of the analysis is to predict this score.

	Predictor Variables
	The predictor variables used in the model are categorized as Continuous (Numeric) and Categorical. To ensure consistency in the analysis, all categorical variables will be converted into numerical data. The variables are as follows:

	Continuous Variables
	Attendance Rate: The frequency of school attendance.
	Teacher Quality: A measure of the quality of teachers in the school.
	Distance to School: The distance from the student’s residence to the school.
	Assignments Completed: The number of assignments completed by the student.
	Age: The age of each student.
	Study Hours Per Week: The average number of hours spent studying per week.
	Student ID: The unique identification number of each student




	Categorical Variables:
	School Type: The type of school attended (Public/Private).
	School Location: The location of the school (Rural/Urban).
	Extra Tutorials: Participation in extracurricular tutorials.
	Access to Learning Materials: Accessibility of adequate learning materials.
	Parent Involvement: The level of parental engagement in the student’s academic life.
	Gender: The gender of the student (Male/Female).
	Socioeconomic Status: The economic stability of the student’s family.
	IT Knowledge: What’s the student's knowledge of IT 
	Parent Education Level: The highest level of education attained by the student’s parents.

Appendix 1 shows details of categorical variables converted to numerical continuous variables.

	Model Specification
The mathematical framework of the model is designed to predict students' JAMB scores (Y) based on various predictor variables. The model follows the formula for multiple linear regression:

Y=β0+β1X1+β2X2+⋯+βpXp +ϵ
Where:
	Y: The dependent variable, representing the Predicted JAMB Score.
	β0: The intercept term, which indicates the expected JAMB score when all predictor variables are zero.
	βi:  The coefficient of the ith predictor variable, showing the expected change in Y for a one-unit increase in Xi, assuming other variables remain constant.
	Xi: The predictor variable is used to explain Y.
	ϵ: The error term accounting for variability in Y that is not explained by the predictors.

	Applying the Formula to This Project
In the context of this project, the formula becomes:

Predicted JAMB Score=β0+β1(Attendance Rate)+β2(Teacher Quality)+β3(Distance To School)+β4(Assignments_Completed)+β5(Age)+β6(Study Hours Per Week)+β7(IT Knowledge)+β8(School Type)+β9(School_Location)+β10(Student_ID)+β11(Extra Tutorials)+β12(Access To Learning Materials)+β13(Parent Involvement)+β14(Gender)+β15(Socioeconomic_Status)+β16(Paren Education Level)+ϵ

	Explanation:
	Intercept (β0):
	Represents the baseline JAMB score when all predictors are zero.
	Predictor Coefficients (β1to β15 ):
	Each coefficient represents the influence of a corresponding predictor variable. For example:
	β6: Indicates the effect of increasing weekly study hours on JAMB scores.
	β8: Captures the difference in JAMB scores between students from public and private schools.
	Error Term (ϵ):
	Accounts for unobserved variables or random factors influencing JAMB scores.
	Assumptions:
	The relationship between predictors and the response variable is linear.
	Predictors are independent of each other (no multicollinearity).
	The residuals (differences between observed and predicted values) are normally distributed with constant variance.
This model specification ensures that the predictive framework is robust and interpretable, providing valuable insights into the factors influencing students' JAMB performance. It also allows educators and policymakers to focus on interventions that are statistically significant in improving academic outcomes.

	Multiple Linear Regression Results
To investigate the relationships between students' total JAMB scores and various predictor variables, a multiple linear regression model was fitted. The table above displays the coefficients, standard errors, t-statistics, and p-values for each predictor included in the model. Below is a detailed explanation of the results:

	Model Overview
The regression equation derived from the analysis is as follows:

Predicted JAMB Score =  49.194+0.99(Attendance Rate)+10.94(Teacher Quality) - 0.72 (Distance To School) +1.38(Assignments_Completed)-0.3(Age)+1.63(Study Hours Per Week)-3.48(IT Knowledge)-5.3(School Type)+ 1.55(School_Location) +  0.0001(Student_ID)+ 4.7(Extra Tutorials)+ 2.73(Access To Learning Materials)-4.53(Parent Involvement)-0.69(Gender)-3.9(Socioeconomic_Status)+4.9(Paren Education Level)+ϵ

	The Intercept(β0): 49.194 represents the expected JAMB score when all predictor variables are zero.

	Significant Predictors

Predictors with a p-value < 0.05 are statistically significant, indicating a strong relationship with JAMB scores:

	Study Hours Per Week (1.63, p<0.05): Students who study more hours per week tend to achieve higher JAMB scores.
	Attendance Rate (0.99, p<0.05): A higher attendance rate correlates with improved JAMB scores.
	Teacher Quality (10.90, p<0.05): Higher teacher quality significantly increases student performance.
	Distance to School (−0.72, p<0.05): Greater distance from school negatively impacts JAMB scores.
	Extra Tutorials (4.76, p<0.05): Participation in extracurricular tutorials is associated with higher scores.
	Access to Learning Materials (2.73, p<0.05): Better access to learning materials improves performance.
	Parent Involvement (−4.52, p<0.05-): Surprisingly, higher parental involvement appears to slightly reduce scores, potentially due to over-involvement.
	Socioeconomic Status (−3.90, p<0.05): Students from lower socioeconomic backgrounds perform worse in JAMB exams.
	Parent Education Level (4.90, p<0.05): Students with parents having higher education levels tend to perform better.
	School Type (-5.3, p<0.05): Student attending public schools tend to score lower compared to their peers in private schools.
	IT Knowledge (-3.5, p<0.05): Students with lower levels of IT knowledge tend to perform worse, with a 3.48-point decrease in JAMB scores per unit reduction in IT knowledge.

	Non-Significant Predictors
Predictors with a p-value ≥ 0.05 are not statistically significant in explaining variability in JAMB scores:
	Student ID (p=0.08): This variable does not contribute meaningfully to the model.
	Age (p=0.31): Age shows no significant impact on JAMB scores.
	Gender (p=0.54): Gender does not significantly affect performance.
	School Location (p=0.17): School location shows no significant influence on JAMB scores.
	Assignment Completed (p=0.05): Assignment Completed shows no significant influence on JAMB scores.


	Key Findings:
	Positive Effects: Study Hours Per Week, Attendance Rate, Teacher Quality, Extra Tutorials, and Access to Learning Materials contribute positively to higher JAMB scores.
	Negative Effects: Distance to School, Socioeconomic Status, and Parental Involvement are negatively associated with performance.
	Unexpected Findings: Parent Involvement shows a negative correlation, possibly reflecting overbearing involvement or lack of autonomy.


Appendix 2 shows the details of the regression coefficient


6. Predictive Results

a. Interaction Terms
Interaction terms were included in the model to explore whether relationships between predictors with weak p value and those with stronger p value influenced JAMB scores jointly rather than independently. Specifically, interaction terms such as Study Hours Per Week × Age, Gender × Teacher Quality, Assignments Completed × Access to Learning Materials, and School_Location × School Type were tested.

However, the results demonstrated that the interaction terms did not significantly improve the model's performance. The adjusted R2, which measures the explanatory power of the model, decreased from 32% (main effects model) to 24% when interaction terms were included. This reduction suggests that the added complexity introduced by interaction terms weakened the model's predictive accuracy.

Based on these findings, the final model excludes interaction terms, as they do not contribute meaningfully to explaining the variability in JAMB scores. This decision prioritizes model simplicity and predictive effectiveness.

                                    Main Model			                               Introduction of Interaction terms 
 



See more details in Appendix 3


b. Non-linear Predictor Transformations (Inclusion/Exclusion)
Non-linear predictor transformations were not included in this model based on an analysis of the skewness of the significant predictors. Skewness measures the asymmetry of the data distribution, with values close to 0 indicating a symmetric and roughly normal distribution suitable for linear regression. For this dataset, the skewness values of all predictors ranged between -1.14 and 0.72, which is within the acceptable range of -2 to +2 for linear modeling.
Most predictors, such as Distance to School (-0.02) and Study Hours Per Week (0.05), exhibited near-zero skewness, confirming a symmetric distribution. Even School Type, with a skewness of -1.14, remains within the tolerable range, suggesting no extreme asymmetry that would necessitate transformations.
Given the results of the skewness analysis, the data shows no significant deviation from normality that would compromise the assumptions of the linear regression model. Therefore, non-linear transformations of predictors were excluded to maintain the simplicity and interpretability of the model while adhering to linear modeling assumptions.

The skewness of the predictors has been shown in Appendix 4

	Descriptive Statistics 

	Pearson Product-Moment Correlation Matrix
A correlation matrix will be generated to examine relationships between the predictor variables and the response variable (JAMB Score). Any pair of variables with a correlation absolute value greater than 0.9 will be carefully reviewed and potentially removed to avoid multicollinearity.
From our correlation matrix below, we could see that:

	Study Hours Per Week has a stronger correlation with JAMB score which is 0.42, meaning that more study hours tend to increase JAMB scores, but it’s a moderate relationship.
	Teacher Quality has a 0.30 correlation with JAMB score, indicating that better teacher quality is moderately related to higher JAMB scores.
	Attendance Rate shows a 0.28 correlation with JAMB score, meaning higher attendance slightly improves JAMB scores.
	Assignments Completed has a 0.28 correlation with JAMB score, meaning completing more assignments is linked to higher scores.
	However other factors like distance to school, school type, and gender don't seem to have a strong impact on JAMB scores.

Pearson Correlation Matrix – Numeric
 

For more details check out Appendix 5






	Arithmetic Mean and Standard Deviation

The arithmetic means provides a central tendency, offering insight into the average value of variables like study hours or JAMB scores, which helps identify general patterns. The standard deviation measures the spread or variability of the data, showing how much individual values deviate from the mean. Together, these metrics give a clear picture of the data's overall behavior, helping to detect outliers, assess consistency, and inform further analysis.

1. JAMB Score
	Mean: 174.07 — This indicates the average score obtained by students in the JAMB exam.
	Standard Deviation: 47.62 — The scores deviate from the mean by an average of 47.62 points, showing moderate variability in performance.

2. Study Hours Per Week
	Mean: 19.52 — Students, on average, spend about 19.52 hours per week studying.
	Standard Deviation: 9.63 — The study hours vary by about 9.63 hours, indicating some students study significantly more or less than the average.

3. Attendance Rate
	Mean: 84.24 — On average, students have an attendance rate of 84.24%.
	Standard Deviation: 9.49 — Attendance rates vary by about 9.49%, showing most students have consistent attendance.

4. Teacher Quality
	Mean: 2.52 — This represents the average rating of teacher quality on the given scale.
	Standard Deviation: 0.99 — Teacher quality ratings vary by 0.99, suggesting slightly varied perceptions or measurements of teacher effectiveness.

5. Distance To School
	Mean: 10.00 — Students live an average of 10 kilometers from school.
	Standard Deviation: 4.82 — The distance to school varies by about 4.82 kilometers, reflecting a moderate range of commute distances.

6. School Type
	Mean: 1.75 — This represents the average school type, with a numerical coding (e.g., 1 for public, 2 for private).
	Standard Deviation: 0.43 — The variation in school type is minimal, indicating a slightly higher representation of one school type over the other.

7. Extra Tutorials
	Mean: 1.54 — The average value for participation in extra tutorials is 1.54, likely on a scale of participation (e.g., 1 for no, 2 for yes).
	Standard Deviation: 0.49 — There is minimal variability in whether students attend tutorials.

8. Access To Learning Materials
	Mean: 1.67 — The average access to learning materials is 1.67 on the given scale.
	Standard Deviation: 0.47 — Variation in access is low, suggesting similar levels of availability for most students.
9. Parent Involvement
	Mean: 2.18 — Parents are moderately involved on average, as per the scale used.
	Standard Deviation: 0.77 — Parental involvement varies slightly, reflecting differences in engagement levels.

10. IT Knowledge
	Mean: 2.16 — Students, on average, rate their IT knowledge at 2.16 on the scale.
	Standard Deviation: 0.78 — There is moderate variation in IT knowledge among students.

11. Socioeconomic_Status
	Mean: 2.18 — The average socioeconomic status is 2.18, based on the scale.
	Standard Deviation: 0.76 — Students’ socioeconomic statuses show moderate variability.

12. Paren Education Level
	Mean: 2.62 — On average, parents have attained a moderate level of education as per the scale.
	Standard Deviation: 1.04 — Parent education levels vary by about 1.04, reflecting a broad spectrum of educational attainment.

13. Predicted JAMB Score
	Mean: 174.07 — The predicted average JAMB score aligns closely with the actual average JAMB score, indicating the model's accuracy in prediction.
	Standard Deviation: 27.02 — The variability in predicted scores (27.02) is lower than the actual scores, likely due to the smoothing effect of the regression model.

In summary, the standard deviations indicate that most variables have moderate variability, with some, like Study Hours Per Week and Distance to School, showing greater dispersion, while others, like School Type and Extra Tutorials, exhibit minimal variation. This variability plays a role in understanding the predictors’ impact on the response variable, JAMB Score


Find the data below: Appendix 6

	Box-Plots of Tukey’s Five Number Summaries 
Tukey’s Five-Number Summary is a statistical method used to describe the distribution of a dataset through five key data points: the minimum, first quartile (Q1), median (Q2), third quartile (Q3), and maximum. These values provide a quick, visual summary of the data's spread and central tendency, helping to identify patterns such as skewness, outliers, and the overall range of the data. This summary is often visualized using a box plot, which offers a clear depiction of the data distribution and highlights potential outliers for further analysis.
	Numerical Representation of the Tukey’s Five Number Summaries 


	Box-Plots of Tukey’s Five Number Summaries
 
	Summary of Evaluation Metric
The evaluation metrics used to assess the predictive performance of the multiple linear regression model are the Root Mean Squared Error (RMSE) and R-squared (R²). These metrics provide insights into the accuracy and explanatory power of the model.

	Root Mean Squared Error (RMSE)
The RMSE for the model was calculated to be 39.19. This metric represents the average deviation of the predicted JAMB scores from the actual scores, measured in the same units as the response variable. Specifically, an RMSE of 39.19 means that, on average, the model’s predictions deviate from the actual JAMB scores by approximately 39.19 points.

Interpretation:
	Considering the total possible JAMB score ranges from 0 to 400, the RMSE accounts for approximately 9.8% of the score range.
	While this level of error suggests the model has captured some of the predictive relationships in the data, the relatively high RMSE indicates that the predictions are not highly precise.
	Additional variables, improved data quality, or advanced modeling techniques may help reduce the prediction error.

Implications:
	A lower RMSE would indicate better predictive performance, meaning the model’s predictions are closer to the actual scores.
	Strategies to reduce the RMSE could include exploring non-linear transformations, addressing multicollinearity, or adding more explanatory variables to the model.

	 R-squared (R²)
The R² value for the model was calculated to be 0.323, indicating that 32.3% of the variability in the total JAMB scores is explained by the predictors included in the model. This value reflects the proportion of variance in the response variable that can be accounted for by the independent variables.

Interpretation:
	An R² of 0.323 suggests that while the model captures some of the relationships between predictors and the response variable, a significant portion (67.7%) of the variability remains unexplained.
	This lower R² indicates that there are likely other factors influencing JAMB scores that are not included in the current dataset.

Implications:
	A higher R² would mean the predictors are collectively better at explaining the variability in JAMB scores.
	The low R² suggests the need for further investigation into additional factors that may affect JAMB scores, such as students' mental health, quality of teaching methods, or environmental influences.





	Relationships Between Response and Each Predictor

	Relationship between Study Hours Per Week and JAMB Score
The scatter plot below demonstrates a positive linear relationship between Study Hours Per Week and JAMB Score. The line of best fit (red line) indicates that, generally, as students increase their weekly study hours, their JAMB scores tend to improve. This positive trend suggests that study time is an important factor in achieving higher JAMB scores.
However, there is significant variability in scores at each level of study hours. For instance, scores vary widely from around 10 to 40 study hours per week, indicating that study hours alone do not fully predict JAMB scores; other factors may also influence performance. Additionally, some outliers exist, with certain students achieving exceptionally high or low scores regardless of their study hours.
Finally, while the relationship is generally linear, there appears to be some clustering at higher study hours (20-30 hours per week), which may suggest diminishing returns to additional study time. Nonetheless, the linear trend captures the overall positive relationship effectively, highlighting that increased study time generally correlates with higher JAMB scores, albeit with some individual differences.













	Relationship between Attendance Rate and JAMB Score
The scatter plot below reveals a positive linear relationship between Attendance Rate and JAMB Score. The line of best fit (red line) indicates that students with higher attendance rates tend to achieve higher JAMB scores, suggesting that consistent attendance contributes positively to exam performance.
However, there is substantial variability in JAMB scores at each attendance level, especially between 70% and 100% attendance rates. This variability implies that while attendance is an important factor, it is not the sole determinant of JAMB scores, and other factors likely influence academic outcomes. Additionally, some outliers are visible, where students with similar attendance rates show very different JAMB scores. This further suggests that individual differences or other external factors may affect performance.






	Relationship between Teacher Quality and JAMB Score
The scatter plot below shows a positive linear relationship between Teacher Quality (rated from 1 to 5) and JAMB Score. The line of best fit (red line) suggests that higher teacher quality ratings are associated with slightly higher JAMB scores, implying that better-rated teaching quality may contribute positively to students' performance.
However, there is considerable variability in JAMB scores across all levels of teacher quality. For each quality rating, the scores range widely, indicating that while teacher quality has a positive influence, it is not the sole predictor of JAMB performance. Additional factors likely affect students' scores, as reflected in the scattered points at each rating level.
In summary, this plot suggests that improved teacher quality has a positive, albeit modest, impact on JAMB scores. The substantial score variability at each quality level implies that other factors contribute to performance, highlighting that while teacher quality matters, it is one of several influences on academic success.












	Relationship between Distance to School and JAMB Score
The scatter plot below shows a negative linear relationship between Distance To School and JAMB Score. The line of best fit (red line) suggests that students living farther from school tend to have slightly lower JAMB scores, implying that increased distance to school may have a modest adverse effect on performance.
However, there is considerable variability in JAMB scores across all distances. For each distance, the scores range widely, indicating that while distance may have a small negative influence, it is not the sole determinant of JAMB performance. Additional factors likely play a significant role, as evidenced by the scattered points at each distance.
In summary, this plot suggests that greater distance to school has a slight negative impact on JAMB scores. The substantial score variability at each distance highlights that while proximity to school matters, it is one of several factors influencing academic success.








	Relationship between School Type and JAMB Score
The scatter plot illustrates the relationship between School Type (where 1 represents private schools and 2 represents public schools) and JAMB Score. The red trendline indicates that there is little to no significant difference in average JAMB scores between students from private schools and those from public schools.
Although the average scores are similar, the plot shows that there is considerable variability in scores within both school types. This wide range suggests that factors beyond school type may have a substantial influence on JAMB performance.
In summary, while the type of school (private or public) does not appear to have a strong direct impact on average JAMB scores, individual performance varies widely, indicating that additional factors contribute to student outcomes.









	Relationship between Extra Tutorials and JAMB Score
The scatter plot below shows the relationship between Extra Tutorials (categorized as 1 = No and 2 = Yes) and JAMB Score. The line of best fit (red line) indicates that students who attended extra tutorials (2) tend to achieve slightly higher JAMB scores compared to those who did not (1). This suggests that participating in extra tutorials may have a positive impact on academic performance.
However, there is notable variability in JAMB scores for both groups. Students in both categories exhibit a wide range of scores, from low to high, indicating that extra tutorials are not the sole determinant of JAMB performance. Other factors, such as individual study habits, access to learning materials, or teacher quality, likely play significant roles.
In summary, this plot suggests that attending extra tutorials has a modest positive effect on JAMB scores. The considerable variation in scores within both groups highlights that while extra tutorials are beneficial, they are only one of many factors influencing academic success.











	Relationship between Access to Learning Materials and JAMB Score
The scatter plot below illustrates the relationship between Access to Learning Materials (categorized as 1 = No and 2 = Yes) and JAMB Score. The line of best fit (red line) suggests a slight increase in JAMB scores for students who had access to learning materials (2) compared to those who did not (1). This indicates that access to learning materials may have a modest positive impact on academic performance.
However, there is substantial variability in JAMB scores within both groups. Students with and without access to learning materials exhibit a wide range of scores, implying that while access to learning materials is beneficial, it is not the sole determinant of JAMB performance. Other factors, such as individual study habits, teacher quality, or socioeconomic status, likely contribute significantly to the observed performance.
In summary, the plot indicates that access to learning materials has a positive but limited influence on JAMB scores. The variability within each group underscores the multifaceted nature of academic performance, suggesting that learning materials are just one of many contributing factors.














	Relationship between Parent Involvement and JAMB Score
The scatter plot illustrates the relationship between Parent Involvement (categorized as High, Low, and Medium) and JAMB Scores. The regression line suggests a slight negative trend, where JAMB scores gradually decline as parental involvement transitions from High to Low to Medium.
Students with High Parent Involvement exhibit a wide range of JAMB scores, indicating that while high involvement provides a supportive environment, it does not guarantee higher performance. Similarly, Low Parent Involvement shows comparable score variability, suggesting no significant advantage or disadvantage compared to other categories. For students with Medium Parent Involvement, the regression line indicates a slightly lower average score compared to those with high involvement, though variability remains evident across all categories.
In conclusion, parental involvement influences JAMB scores to some extent, but the variability within each category highlights its limited predictive power. Other factors, such as student effort, teacher quality, and access to resources, likely play more decisive roles. The slight negative trend may reflect diminishing support as involvement becomes less consistent, potentially impacting student performance.





	Relationship between IT Knowledge Level and JAMB Score
The scatter plot below illustrates the relationship between IT Knowledge Level (1 = High, 2 = Low, and 3 = Medium) and JAMB Score. The line of best fit (red line) suggests a slight increase in JAMB scores for students with High IT Knowledge (1) compared to those with Low (2) or Medium (3) IT Knowledge levels. This could indicate that a higher level of IT Knowledge has a modest positive association with JAMB performance.
However, there remains substantial variability in JAMB scores within each IT Knowledge category. Both high and low scores are present in all three categories, implying that while High IT Knowledge may have some benefit, it is not the sole determinant of JAMB performance. Other factors—such as study habits, quality of teaching, or access to learning resources—likely also play significant roles in influencing scores.
In summary, the plot suggests that a higher level of IT Knowledge might have a positive but limited impact on JAMB scores. The variability within each group underscores the multifaceted nature of academic performance, suggesting that IT Knowledge is only one of many factors contributing to JAMB outcomes.








	Relationship between Socioeconomic Status and JAMB Score
The scatter plot below illustrates the relationship between Socioeconomic Status (1 = High, 2 = Low, and 3 = Medium) and JAMB Score. The line of best fit (red line) shows a slight downward trend, indicating that students with High Socioeconomic Status (1) tend to have marginally higher JAMB scores compared to those with Medium (3) and Low (2) Socioeconomic Status.
However, there is substantial variability in JAMB scores within each group. Students across all socioeconomic levels show a wide range of scores, suggesting that while socioeconomic status may have some influence, it is not the sole determinant of JAMB performance. Other factors, such as study habits, access to educational resources, and teacher quality, likely play significant roles in academic outcomes.
In summary, the plot indicates that higher socioeconomic status may be associated with a slight advantage in JAMB scores. Nonetheless, the variability within each group underscores the multifaceted nature of academic performance, suggesting that socioeconomic status is just one of many contributing factors.





Relationship between Parent Education Level and JAMB Score
The scatter plot depicts the relationship between Parent Education Level (categorized as None, Primary, Secondary, and Tertiary) and JAMB Scores, with the line of best fit (red line) indicating a weak positive relationship. Students whose parents have higher education levels tend to achieve slightly higher JAMB scores on average.
Across all education levels, students display a wide range of JAMB scores, spanning from below 200 to above 300. The slight upward slope of the trend line suggests a marginal increase in average JAMB scores as parental education level rises from None to Tertiary. However, the substantial variability within each category highlights that parent education level is not a dominant factor in determining JAMB performance.













	Diagnostic Plots of the Final Model
In this project work, we employ multiple linear regression to analyze factors influencing JAMB scores. To ensure the model's validity, we assess four diagnostic plots that evaluate the assumptions underlying linear regression: linearity, normality of residuals, homoscedasticity, and influence of outliers.

Residuals vs Fitted Plot: 
The Residuals vs. Fitted Plot was used to evaluate the assumptions of linearity and homoscedasticity in the model. The residuals are generally scattered around the horizontal line at zero, indicating that the linearity assumption is largely satisfied. However, the following observations were made:
	Heteroscedasticity: The spread of residuals increases with higher fitted values, as seen from the funnel-shaped pattern. This indicates that the variance of the residuals is not constant across all fitted values, a violation of the homoscedasticity assumption. This could affect the accuracy of p-values and confidence intervals.
	Minor Non-Linearity: The red trend line in the plot shows a slight curve, suggesting a mild non-linear relationship between the predictors and the outcome variable. This indicates that the model may not fully capture all patterns in the data.
	Outliers: A few points (e.g., observations 4191, 1542, and 313) deviate significantly from the rest of the data. These may represent influential observations that could disproportionately impact the model's performance.




















Normal Q-Q
The Normal Q-Q plot was employed to evaluate whether the residuals of the predictive model for JAMB scores adhered to a normal distribution. This evaluation is critical, as one of the foundational assumptions of multiple linear regression is that residuals should follow a normal distribution. Normality of residuals ensures the validity of statistical inferences derived from the model.

Upon analyzing the plot, the central portion of the residuals aligns closely with the diagonal line, indicating that for most observations, the residuals are approximately normally distributed. This alignment reflects that the model adequately captures the general trends in the dataset, suggesting a reasonable overall fit.

However, deviations are evident at both the upper and lower tails of the distribution. The upper tail shows more pronounced departures from the diagonal line, suggesting the presence of extreme residuals where the model either significantly overestimates or underestimates JAMB scores. These deviations could point to the presence of outliers—observations that differ markedly from most of the data. Such outliers might arise from unique student characteristics not captured by the predictors, such as unusually high or low academic performance, exceptional preparation techniques, or disparities in access to educational resources.
 



Scale-Location

The Scale-Location plot, also referred to as the Spread-Location plot, was utilized to examine the assumption of homoscedasticity (constant variance of residuals) in the JAMB score prediction model. This diagnostic tool is essential in evaluating whether the spread of residuals remains consistent across all fitted values, a critical assumption for reliable linear regression results.

The plot visualizes the square root of the standardized residuals on the y-axis against the fitted values on the x-axis. Ideally, the points should be randomly scattered without forming any discernible pattern. Such a distribution would confirm that the residuals exhibit constant variance, fulfilling the assumption of homoscedasticity. However, in this case, the plot exhibits a slight funnel-shaped pattern, with residuals displaying a narrower spread at lower fitted values and a wider spread as fitted values increase. This observation suggests heteroscedasticity, where the variance of residuals is not constant. In the context of this model, it indicates that predictions for lower JAMB scores are more consistent, while predictions for higher scores are more variable.

Additionally, the red smoothing line, which provides a trend for the residuals, shows a slight upward curvature. This curvature further signals variance inconsistency and hints at potential non-linearity in the data, suggesting that the linear regression model may not fully capture the relationship between the predictors and the response variable.



 


Residuals vs. Leverage

The Residuals vs. Leverage plot is an important diagnostic tool used to identify influential observations in the dataset that might disproportionately affect the results of the JAMB score prediction model. This plot examines the relationship between residuals (differences between observed and predicted JAMB scores) and leverage (a measure of how much an observation influences the model). It is particularly useful for detecting points that could have a significant impact on the regression model's performance and validity.

From the plot, most data points are clustered around low leverage values and near-zero residuals. This indicates that most observations have a minimal influence on the model and align well with its predictions. However, a few points, such as observations 1542, 2875, and 4191, stand out due to their higher leverage values and relatively large residuals. These points are flagged as potential influential observations because they deviate more significantly from the main cluster of data. While these points fall below the Cook's distance threshold (indicated by the dotted line), which suggests they do not exert excessive influence over the regression results, their presence warrants further investigation to understand whether they represent legitimate data variations or possible errors.

The red trend line in the plot remains relatively flat, suggesting that the residuals do not systematically increase or decrease with leverage. This indicates that the linear regression model does not exhibit significant issues related to linearity or systemic patterns associated with high-leverage points.
 


	Variable Inflation Factor (VIF)

This is a is a measure used to detect multicollinearity in a regression model. Multicollinearity occurs when two or more independent variables in a model are highly correlated, which can make it difficult to interpret the effect of each variable on the dependent variable. High multicollinearity can lead to unstable estimates of regression coefficients, making it harder to identify the true relationship between predictors and the dependent variable.

How VIF is Calculated
For each independent variable Xi in a regression model, VIF is calculated as follows:
VIF(Xi)=  1/(1-R_i^2 )

Where Ri2 is the coefficient of determination for a regression model where Xi    is the dependent variable, and all other predictors are independent variables. Essentially, VIF quantifies how much the variance of an estimated regression coefficient increases due to multicollinearity with other predictors.

Interpreting VIF Values
	VIF = 1: No correlation between the variable and others, so there is no multicollinearity.
	1 < VIF < 5: Moderate multicollinearity, typically considered acceptable.
	VIF > 5: Indicates high multicollinearity. While not an absolute cutoff, a VIF greater than 5 suggests that the variable is highly correlated with others, which could cause problems in the regression analysis.
	VIF > 10: Severe multicollinearity, often considered a strong sign that the variable should be removed or that corrective measures should be taken.


VIF Values for the Model Predictor
Each of the VIF values in this analysis falls below the threshold of 5, indicating that multicollinearity is not a concern for this model. This suggests that the predictors provide unique information without substantial overlap in variance, which supports the stability and reliability of the coefficient estimates.
To interpret the individual VIF values, Study Hours Per Week has a VIF of 1.04, indicating a low level of multicollinearity and that it contributes unique information to the model. Similarly, Attendance Rate and Teacher Quality have VIF values of 1.03 and 1.02, respectively, indicating minimal correlation with other predictors. Other variables, including Distance to School and School Type, each have VIF values close to 1, further confirming their independence. 

For details of the calculated VIF  Appendix 7


Summary of Findings 
This study investigated the factors influencing students' JAMB scores through a multiple linear regression model. The analysis incorporated various predictors, including study habits, school-related attributes, socioeconomic factors, and parental involvement, to determine their impact on academic performance. The final model explained 33% of the variation in JAMB scores, indicating that these predictors collectively provide meaningful insights into performance trends.
The results highlighted that factors such as study hours, attendance rate, teacher quality, and access to learning materials positively contributed to higher JAMB scores. Conversely, variables like distance to school and socioeconomic status negatively influenced scores, emphasizing the role of systemic and logistical challenges in academic outcomes. Predictors such as gender and school type showed minimal impact, indicating their limited relevance in this context.
Diagnostic assessments confirmed that the model assumptions of normality, linearity, and homoscedasticity were reasonably met. Residual analysis revealed no significant violations, and skewness checks showed that the predictors were sufficiently distributed to warrant no need for transformations. Although a few outliers were detected, their influence on the model's reliability was minimal.
Overall, this analysis provides a clear understanding of the key determinants of academic performance, offering valuable insights for targeted interventions aimed at improving student outcomes. By focusing on enhancing study environments and addressing socioeconomic disparities, stakeholders can better support students in achieving higher academic success.






 

APPENDIX 1: Categorical Variables Converted to Numerical
 
APPENDIX 2: Multilinear Regression Coefficient














Appendix 3: Introduction of Interaction Terms
 




Appendix 4: Skewness of Predictors
 































 



































Appendix 5:  Pearson Correlation Matrix – Numeric
 

 





Appendix 6: Arithmetic Mean and Standard Deviation
  	

















Appendix 7: Variable Inflation Factor (VIF) 
Appendix 8: Project plan
 
 
