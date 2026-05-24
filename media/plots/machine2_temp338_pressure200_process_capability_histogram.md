# Filter data for Machine 2, Temperature 338, Pressure 200
data_filtered_machine2_cap <- X029...029 %>% filter(Machine == 2, Temperature == 338, Pressure == 200)

# Define specification limits and target
LSL <- 45
USL <- 55
TARGET <- 50

# Create a qcc object (individual control chart) first
qcc_obj_m2 <- qcc(data_filtered_machine2_cap$PartLength, type = "xbar.one", plot = FALSE)

# Perform process capability analysis
cap_m2 <- process.capability(
  qcc_obj_m2,
  spec.limits = c(LSL, USL),
  target = TARGET
)

# Extract capability statistics
center_m2 <- round(as.numeric(cap_m2$center), 2)
stdev_m2 <- round(as.numeric(cap_m2$std.dev), 4)

# For cpm
temp_cpm_m2 <- as.numeric(unname(cap_m2$cpm[1]))
cpm_m2 <- round(temp_cpm_m2, 3)
temp_cpm_ci_lower_m2 <- as.numeric(unname(cap_m2$cpm[2]))
cpm_ci_lower_m2 <- round(temp_cpm_ci_lower_m2, 3)
temp_cpm_ci_upper_m2 <- as.numeric(unname(cap_m2$cpm[3]))
cpm_ci_upper_m2 <- round(temp_cpm_ci_upper_m2, 3)

# For cp
temp_cp_m2 <- as.numeric(unname(cap_m2$cp[1]))
cp_m2 <- round(temp_cp_m2, 3)
temp_cp_ci_lower_m2 <- as.numeric(unname(cap_m2$cp[2]))
cp_ci_lower_m2 <- round(temp_cp_ci_lower_m2, 3)
temp_cp_ci_upper_m2 <- as.numeric(unname(cap_m2$cp[3]))
cp_ci_upper_m2 <- round(temp_cp_ci_upper_m2, 3)

# For cpk
temp_cpk_m2 <- as.numeric(unname(cap_m2$cpk[1]))
cpk_m2 <- round(temp_cpk_m2, 3)
temp_cpk_ci_lower_m2 <- as.numeric(unname(cap_m2$cpk[2]))
cpk_ci_lower_m2 <- round(temp_cpk_ci_lower_m2, 3)
temp_cpk_ci_upper_m2 <- as.numeric(unname(cap_m2$cpk[3]))
cpk_ci_upper_m2 <- round(temp_cpk_ci_upper_m2, 3)

# For cpl
temp_cpl_m2 <- as.numeric(unname(cap_m2$cpl[1]))
cp_l_m2 <- round(temp_cpl_m2, 3)
temp_cpl_ci_lower_m2 <- as.numeric(unname(cap_m2$cpl[2]))
cp_l_ci_lower_m2 <- round(temp_cpl_ci_lower_m2, 3)
temp_cpl_ci_upper_m2 <- as.numeric(unname(cap_m2$cpl[3]))
cp_l_ci_upper_m2 <- round(temp_cpl_ci_upper_m2, 3)

# For cpu
temp_cpu_m2 <- as.numeric(unname(cap_m2$cpu[1]))
cp_u_m2 <- round(temp_cpu_m2, 3)
temp_cpu_ci_lower_m2 <- as.numeric(unname(cap_m2$cpu[2]))
cp_u_ci_lower_m2 <- round(temp_cpu_ci_lower_m2, 3)
temp_cpu_ci_upper_m2 <- as.numeric(unname(cap_m2$cpu[3]))
cp_u_ci_upper_m2 <- round(temp_cpu_ci_upper_m2, 3)

# Calculate overall defect rate (expected percentage) and export
overall_defect_rate_m2_raw <- unname(cap_m2$exp.lsl) + unname(cap_m2$exp.usl)
overall_defect_rate_m2 <- round(as.numeric(overall_defect_rate_m2_raw) * 100, 2)

# Prepare data for ggplot2 histogram
df_hist_m2 <- data.frame(PartLength = data_filtered_machine2_cap$PartLength)

# Plot histogram with ggplot2
p_hist_m2 <- ggplot(df_hist_m2, aes(x = PartLength)) +
  geom_histogram(aes(y = after_stat(density)), binwidth = 0.5, fill = "#0072B2", color = "white", alpha = 0.7) +
  geom_density(color = "#D55E00", size = 1) +
  geom_vline(xintercept = TARGET, linetype = "dashed", color = "black", size = 0.8, aes(x = TARGET, linetype = "Target")) +
  geom_vline(xintercept = LSL, linetype = "dotted", color = "#009E73", size = 0.8, aes(x = LSL, linetype = "LSL")) +
  geom_vline(xintercept = USL, linetype = "dotted", color = "#CC79A7", size = 0.8, aes(x = USL, linetype = "USL")) +
  scale_linetype_manual(name = "Limits", values = c("Target" = "dashed", "LSL" = "dotted", "USL" = "dotted"),
                        labels = c("Target" = paste0("Target (", TARGET, ")"),
                                   "LSL" = paste0("LSL (", LSL, ")"),
                                   "USL" = paste0("USL (", USL, ")"))) +
  labs(title = "Process Capability Histogram for Part Length",
       subtitle = "Machine 2, Temperature 338K, Pressure 200kPa",
       x = "Part Length",
       y = "Density") +
  theme_minimal() +
  theme(plot.title = element_text(size = 18),
        axis.title = element_text(size = 18),
        axis.text = element_text(size = 14),
        legend.position = "bottom",
        panel.background = element_rect(fill = "white", colour = "white"),
        plot.background = element_rect(fill = "white", colour = "white"))

p_plotly_hist_m2 <- ggplotly(p_hist_m2)
saveWidget(p_plotly_hist_m2, file = "media/plots/machine2_temp338_pressure200_process_capability_histogram.html", selfcontained = TRUE)
