# R Code for ANOVA: Part Resistance vs. Pressure*Temperature Interaction (Machine 1)
# File: machine1_resistance_pressure_temperature_interaction_anova_pvalue.md

library(dplyr)

# The dataframe X029___029 is assumed to be available in the R session (passed from Python).
# Filter for Machine 1
machine1_data_interaction <- X029___029 %>% filter(Machine == 1)

# Perform ANOVA for PartResistance by Pressure and Temperature interaction
interaction_anova_model <- aov(PartResistance ~ factor(Pressure) * factor(Temperature), data = machine1_data_interaction)

# Get the summary of the ANOVA model
interaction_anova_summary <- summary(interaction_anova_model)

# Extract the p-value for the Pressure:Temperature interaction term
p_value_for_md_interaction_anova <- interaction_anova_summary[[1]][["Pr(>F)"]][3]

# Print the p-value (for context in the markdown file)
cat(paste0("P-value for Pressure:Temperature Interaction (Machine 1 Resistance): ", sprintf("% .4f", p_value_for_md_interaction_anova), "\n"))
