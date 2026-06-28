# R Code for T-test: Part Length (Machine 1 vs Machine 2, P=100, T=303)
# File: machine1_vs_machine2_t_test_p100_t303_p_value.md

library(dplyr)

# The dataframe X029___029 is assumed to be available in the R session (passed from Python).
# Filter data for Machine 1 and Machine 2 under specified conditions
filtered_data <- X029___029 %>% filter(Pressure == 100, Temperature == 303, Machine %in% c(1, 2))

# Perform t-test for PartLength between Machine 1 and Machine 2
t_test_result <- t.test(PartLength ~ Machine, data = filtered_data)

# Extract the p-value
p_value_for_md <- t_test_result$p.value

# Print the p-value (for context in the markdown file)
cat(paste0("P-value for T-test (Machine 1 vs Machine 2, P=100, T=303): ", sprintf("% .4f", p_value_for_md), "\n"))
