# Ensure the directory exists from R's perspective
dir.create('media/plots', showWarnings = FALSE)
# Filter data for the specified conditions
df_filtered_new <- get(df_actual_name) %>% filter(Pressure == 300, Temperature == 373)

# Filter for Machine 1 and Machine 2
machine1_data_new <- df_filtered_new %>% filter(Machine == 1)
machine2_data_new <- df_filtered_new %>% filter(Machine == 2)

# Perform t-test
t_test_result_new <- t.test(machine1_data_new$PartResistance, machine2_data_new$PartResistance)

p_value_new_conditions <- t_test_result_new$p.value
