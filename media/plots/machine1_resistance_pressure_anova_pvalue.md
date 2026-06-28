# R Code for ANOVA: Part Resistance vs. Pressure (Machine 1)
# File: machine1_resistance_pressure_anova_pvalue.md

library(dplyr)

# The dataframe X029___029 is assumed to be available in the R session (passed from Python).
# Filter for Machine 1
machine1_data <- X029___029 %>% filter(Machine == 1)

# Perform ANOVA for PartResistance by Pressure
anova_model <- aov(PartResistance ~ factor(Pressure), data = machine1_data)

# Get the summary of the ANOVA model
anova_summary <- summary(anova_model)

# Extract the p-value for Pressure
p_value_for_md <- anova_summary[[1]][["Pr(>F)"]][1]

# Print the p-value (for context in the markdown file)
cat(paste0("P-value for Pressure (Machine 1 Resistance): ", sprintf("% .4f", p_value_for_md), "\n"))
