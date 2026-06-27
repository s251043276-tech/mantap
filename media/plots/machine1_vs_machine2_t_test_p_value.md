# Filter data for the specified conditions
df_filtered <- X029...029 %>% filter(Pressure == 100, Temperature == 303)

# Filter for Machine 1 and Machine 2
machine1_data <- df_filtered %>% filter(Machine == 1)
machine2_data <- df_filtered %>% filter(Machine == 2)

# Perform t-test
t_test_result <- t.test(machine1_data$PartResistance, machine2_data$PartResistance)

p_value <- t_test_result$p.value
