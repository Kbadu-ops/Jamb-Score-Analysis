	BACKGROUND:
The Joint Admissions and Matriculation Board (JAMB) is an essential exam in Nigeria that determines student eligibility for tertiary institutions, like the SAT exams in the United States. The JAMB score reflects the students' preparedness for higher education, influencing their admission opportunities. However, students' performances are affected by multiple factors, including their background, gender, state of origin, and subject choices.

This project is motivated by the question: "How do factors such as students' demographic attributes and subject performances affect their overall JAMB scores?" A deeper understanding of these relationships can reveal how non-academic factors contribute to academic success, offering insights for educators and policymakers to create more equitable systems. Accurate prediction of performance can assist educators, policymakers, and students in making informed decisions regarding educational interventions 

	Predictive Purpose:
The primary aim of this project is to predict students' overall performance in JAMB, specifically their total score, based on various factors, including demographic and subject performances, that influence overall student scores. Predicting JAMB scores can provide insights that can help improve student interventions, guide resource allocation, and inform policy decisions aimed at enhancing educational equity and academic success.

This project will also assess how categorical variables (such as gender and state of origin) correlate with students' scores and examine the relationships between different subject scores to provide comprehensive insights into student performance patterns.

R Code Used for the project work
# Load necessary libraries
library(tidyverse)
library(caret)
library(ggplot2)
library(ggcorrplot)
library(readr)
library(dplyr)

library(readr)

################# step 1
# Load the dataset
jamb_data<- read_csv("Week 3/jamb_exam_results (2).csv")
View(jamb_data)
  
# Remove Student_ID
jamb_data <- select(jamb_data,-Student_ID,-Age,-Gender,-Assignments_Completed,-School_Location)



################# step 2 Converting Categorical Data to Numeric
# Convert categorical data to numeric
jamb_data$School_Type <- as.numeric(factor(jamb_data$School_Type))
jamb_data$Extra_Tutorials <- as.numeric(factor(jamb_data$Extra_Tutorials))
jamb_data$Access_To_Learning_Materials <- as.numeric(factor(jamb_data$Access_To_Learning_Materials))
jamb_data$Parent_Involvement <- as.numeric(factor(jamb_data$Parent_Involvement))
jamb_data$IT_Knowledge <- as.numeric(factor(jamb_data$IT_Knowledge))
jamb_data$Socioeconomic_Status <- as.numeric(factor(jamb_data$Socioeconomic_Status))
jamb_data$Parent_Education_Level <- as.numeric(factor(jamb_data$Parent_Education_Level))




#### calculating the multiple linear regression to identify how related they are the non-statistical data 

# Load necessary libraries
library(tidyverse)

# Fit the multiple linear regression model
# Assuming JAMB_Score is the dependent variable
linear_model <- lm(JAMB_Score ~ ., data = jamb_data)

# Display the summary of the regression model
model_summary <- summary(linear_model)

# Print the model summary
print(model_summary)


# Extract and print coefficients, standard errors, t-values, and p-values
coefficients_table <- data.frame(
  Predictor = rownames(model_summary$coefficients),
  Estimate = model_summary$coefficients[, "Estimate"],
  Std_Error = model_summary$coefficients[, "Std. Error"],
  t_Value = model_summary$coefficients[, "t value"],
  P_Value = model_summary$coefficients[, "Pr(>|t|)"]
)

print(coefficients_table)




# Adding interaction terms to the model
model_interaction <- lm(
  JAMB_Score ~ Study_Hours_Per_Week * Age + 
    Gender * Teacher_Quality + 
    Assignments_Completed * Access_To_Learning_Materials + 
    School_Location  * School_Type ,
  data = jamb_data
)

# Summarizing the results
summary(model_interaction)







# Load necessary library
library(e1071)  # For skewness calculation
library(ggplot2)  # For visualization

# List of predictors
predictors <- c("Study_Hours_Per_Week", "Attendance_Rate", "Teacher_Quality", 
                "Distance_To_School","School_Type","Extra_Tutorials","Access_To_Learning_Materials"
                ,"Parent_Involvement","IT_Knowledge",
                "Parent_Education_Level", "Socioeconomic_Status")

# Loop through each predictor
for (predictor in predictors) {
  # Skewness calculation
  skew <- skewness(jamb_data[[predictor]], na.rm = TRUE)
  cat(paste("Skewness of", predictor, ":", round(skew, 2), "\n"))
  
  # Create the plot
  p <- ggplot(jamb_data, aes_string(x = predictor)) +
    geom_histogram(aes(y = ..density..), bins = 30, fill = "skyblue", color = "black") +
    geom_density(color = "red") +
    ggtitle(paste("Distribution of", predictor)) +
    theme_minimal()
  
  # Print the plot
  print(p)
}

# Normality test (Shapiro-Wilk) for each predictor
shapiro_results <- sapply(predictors, function(x) shapiro.test(jamb_data[[x]])$p.value)
shapiro_results <- round(shapiro_results, 4)
shapiro_results





# Check residual diagnostics
par(mfrow = c(2, 2))  # Arrange plots in a 2x2 grid
plot(linear_model)    # Plot diagnostic plots





# Load necessary libraries
library(tidyverse)  # For data manipulation and visualization

# Create the predictive model using multiple linear regression
predictive_model <- lm(
  JAMB_Score ~ Study_Hours_Per_Week + Attendance_Rate + Teacher_Quality +
    Distance_To_School + School_Type + Extra_Tutorials  +
    Access_To_Learning_Materials + Parent_Involvement + IT_Knowledge 
     + Socioeconomic_Status + Parent_Education_Level,
  data = jamb_data
)

# View the summary of the predictive model
summary(predictive_model)

# Predict JAMB scores using the model
jamb_data$Predicted_JAMB_Score <- predict(predictive_model, newdata = jamb_data)

# Export the data with predictions to a CSV file
write.csv(jamb_data, "jamb_data_with_predictions.csv", row.names = FALSE)

# Display the first few rows of the data with predictions
head(jamb_data)





# Calculate RMSE
# RMSE is the square root of the mean squared error
rmse <- sqrt(mean((jamb_data$JAMB_Score - jamb_data$Predicted_JAMB_Score)^2))
cat("Root Mean Squared Error (RMSE):", rmse, "\n")



# Calculate R-squared (R²)
# R² measures the proportion of variance explained by the model
ss_total <- sum((jamb_data$JAMB_Score - mean(jamb_data$JAMB_Score))^2)  # Total sum of squares
ss_residual <- sum((jamb_data$JAMB_Score - jamb_data$Predicted_JAMB_Score)^2)  # Residual sum of squares
r_squared <- 1 - (ss_residual / ss_total)
cat("R-squared (R²):", r_squared, "\n")




# Calculate Adjusted R-squared
# Assuming the model is called "jamb_model" and the dataset is "jamb_data"

# Extracting R-squared from the model
r_squared <- summary(predictive_model)$r.squared

# Extracting the number of predictors (p) and observations (n)
n <- nrow(jamb_data)  # Total number of observations
p <- length(predictive_model$coefficients) - 1  # Number of predictors (excluding the intercept)

# Adjusted R-squared formula
adjusted_r_squared <- 1 - ((1 - r_squared) * (n - 1) / (n - p - 1))

# Print the Adjusted R-squared value
cat("Adjusted R-squared:", adjusted_r_squared, "\n")








# Generate Diagnostic Plots for the Final Model

# Assuming your model is called 'model'
# Replace 'model' with the name of your actual regression model if different

par(mfrow = c(2, 2)) # Arrange plots in a 2x2 grid

# a. Residuals vs. Fitted
plot(predictive_model, which = 1, main = "Residuals vs. Fitted")

# b. Normal Q-Q
plot(predictive_model, which = 2, main = "Normal Q-Q")

# c. Scale-Location
plot(predictive_model, which = 3, main = "Scale-Location")

# d. Residuals vs. Leverage
plot(predictive_model, which = 5, main = "Residuals vs. Leverage")

# Reset graphical parameters
par(predictive_model = c(1, 1)) # Reset to single plot layout







################# step 3 Calculating Standard Deviation and Arithmetic Mean
# Calculate mean and standard deviation for each column
jamb_summary_stats <- data.frame(
  Variable = colnames(jamb_data),
  Mean = sapply(jamb_data, mean, na.rm = TRUE),
  SD = sapply(jamb_data, sd, na.rm = TRUE)
)

# View the summary statistics
print(jamb_summary_stats)



################# step 4 Calculating Tukey’s 5 Number Summaries

# Function to calculate and name Tukey's 5-number summary
tukey_summary <- function(x) {
  summary <- fivenum(x, na.rm = TRUE)
  names(summary) <- c("Min", "1st Quartile (Q1)", "Median (Q2)", "3rd Quartile (Q3)", "Max")
  return(summary)
}

# Apply the Tukey summary function to each numeric column in the dataset
jamb_tukey_summaries <- apply(jamb_data, 2, tukey_summary)

# View the labeled Tukey's 5-number summaries
print(jamb_tukey_summaries)





################# step 5 Plotting Box Plots of Tukey's Summaries color picture
# Load necessary libraries
library(tidyverse)

# Assuming your dataset is named 'jamb_data', select the first three variables
first_three_vars <- jamb_data %>%
  select(Parent_Education_Level,Teacher_Quality )

# Reshape the data into long format for ggplot2
jamb_long <- pivot_longer(first_three_vars, 
                          cols = everything(), 
                          names_to = "Variable", 
                          values_to = "Value")

# Plot Tukey's 5-number summary boxplots for the first three variables
ggplot(jamb_long, aes(x = Variable, y = Value, fill = Variable)) +
  geom_boxplot() + # Basic boxplot
  ggtitle("Tukey's 5-number Summaries") + # Title
  theme_minimal() +  # Clean theme
  theme(axis.text.x = element_text(angle = 45, hjust = 1)) + # Rotate x-axis labels for readability
  labs(x = "Variables", y = "Values") + # Axis labels
  scale_fill_brewer(palette = "Set2")   # Set color palette for better presentation







################# step 6 Calculating Pearson Correlation Matrix (Numeric)


# Calculate Pearson correlation matrix
jamb_cor_matrix <- cor(jamb_data, use = "complete.obs")

# View Pearson correlation matrix
print(jamb_cor_matrix)



################# step 7. Visualizing Pearson Correlation Matrix (Graphical)
# Install and load corrplot package if not already installed

# Install necessary package if not already installed
if (!require("corrplot")) {
  install.packages("corrplot", dependencies = TRUE)
}

# Load the corrplot package
library(corrplot)

# Calculate the correlation matrix
correlation_matrix <- cor(jamb_data)

# Create the correlation matrix plot
corrplot(correlation_matrix, 
         method = "circle",        # Use circles to represent correlations
         type = "lower",           # Show only the lower triangle
         order = "original",       # Keep the original order of variables
         tl.col = "red",           # Text color of variable names
         tl.srt = 45,              # Rotate text labels
         addCoef.col = "black",    # Add correlation coefficients
         number.cex = 0.7,         # Size of correlation coefficient numbers
         col = colorRampPalette(c("red", "white", "blue"))(200), # Color scale
         cl.lim = c(-1, 1))        # Limit the color scale to -1 to 1






# Load the corrplot package
library(corrplot)

# Calculate the correlation matrix
correlation_matrix <- cor(jamb_data)

# Save the plot with larger dimensions
png("corrplot_large.png", width = 800, height = 600)

# Create the correlation matrix plot
corrplot(correlation_matrix, 
         method = "circle",        # Use circles to represent correlations
         type = "lower",           # Show only the lower triangle
         order = "original",       # Keep the original order of variables
         tl.col = "red",           # Text color of variable names
         tl.srt = 45,              # Rotate text labels
         addCoef.col = "black",    # Add correlation coefficients
         number.cex = 0.7,         # Size of correlation coefficient numbers
         col = colorRampPalette(c("red", "white", "blue"))(200), # Color scale
         cl.lim = c(-1, 1))        # Limit the color scale to -1 to 1

# Close the graphics device
dev.off()




























################# step 9. Calculating the VIF


# Install necessary package if not already installed
if (!require("car")) {
  install.packages("car", dependencies = TRUE)
}

# Load the car package
library(car)

# Fit the multilinear regression model
model <- lm(JAMB_Score ~ Study_Hours_Per_Week + Attendance_Rate + Teacher_Quality +
              Distance_To_School + School_Type +
              Extra_Tutorials + Access_To_Learning_Materials +
              Parent_Involvement + IT_Knowledge + 
              Socioeconomic_Status + Parent_Education_Level, data = jamb_data)

# Calculate the Variance Inflation Factor (VIF)
vif_values <- vif(model)

# Display VIF values
print(vif_values)

view (vif_values)

# Optional: Identify predictors with high multicollinearity
threshold <- 10  # Common threshold for high VIF values
high_vif <- vif_values[vif_values > threshold]
if (length(high_vif) > 0) {
  cat("Variables with high multicollinearity (VIF > 10):\n")
  print(high_vif)
} else {
  cat("No variables with high multicollinearity detected.\n")
}








library(ggplot2)
library(tidyr)

# Response variable
response_var <- "JAMB_Score"

# Predictor variables
predictors <- c("Study_Hours_Per_Week", "Attendance_Rate", "Teacher_Quality",
                "Distance_To_School", "School_Type",
                "Extra_Tutorials", "Access_To_Learning_Materials",
                "Parent_Involvement", "IT_Knowledge", 
                "Socioeconomic_Status", "Parent_Education_Level",
                "Assignments_Completed")

# Loop to create individual plots for each predictor
for (predictor in predictors) {
  # Determine the type of variable (continuous or categorical)
  if (is.numeric(jamb_data[[predictor]])) {
    # Scatterplot for continuous predictors
    plot <- ggplot(jamb_data, aes_string(x = predictor, y = response_var)) +
      geom_point(color = "blue", alpha = 0.6) +
      geom_smooth(method = "lm", color = "red", se = FALSE) +
      labs(title = paste("Relationship between", predictor, "and", response_var),
           x = predictor, y = response_var) +
      theme_minimal()
  } else {
    # Boxplot for categorical predictors
    plot <- ggplot(jamb_data, aes_string(x = predictor, y = response_var, fill = predictor)) +
      geom_boxplot(alpha = 0.7) +
      labs(title = paste("Relationship between", predictor, "and", response_var),
           x = predictor, y = response_var) +
      theme_minimal() +
      theme(legend.position = "none")
  }
  
  # Print each plot
  print(plot)
}


