# R Code for ANOVA: Part Resistance vs. Temperature (Machine 1)
# File: machine1_resistance_temperature_anova_pvalue.md

library(dplyr)

# The dataframe X029___029 is assumed to be available in the R session (passed from Python).
# Filter for Machine 1
machine1_data_temp <- X029___029 %>% filter(Machine == 1)

# Perform ANOVA for PartResistance by Temperature
temp_anova_model <- aov(PartResistance ~ factor(Temperature), data = machine1_data_temp)

# Get the summary of the ANOVA model
temp_anova_summary <- summary(temp_anova_model)

# Extract the p-value for Temperature
p_value_for_md_temp_anova <- temp_anova_summary[[1]][["Pr(>F)"]][1]

# Print the p-value (for context in the markdown file)
cat(paste0("P-value for Temperature (Machine 1 Resistance): ", sprintf("% .4f", p_value_for_md_temp_anova), "\n"))
