# Filter data for Machine 2, Temperature 338, Pressure 200
data_filtered_machine2 <- X029...029 %>% filter(Machine == 2, Temperature == 338, Pressure == 200)

# Create xbar.one chart for PartLength
qcc_chart_m2 <- qcc(data_filtered_machine2$PartLength, type = "xbar.one", nsigmas = 3, plot = FALSE)

# Extract relevant data for plotting from qcc_chart
df_plot_m2 <- data.frame(
  x = 1:length(qcc_chart_m2$data),
  y = qcc_chart_m2$data,
  cl = qcc_chart_m2$center,
  lcl = qcc_chart_m2$limits[1],
  ucl = qcc_chart_m2$limits[2]
)

# Plot using ggplot2 and convert to plotly
p_m2 <- ggplot(df_plot_m2, aes(x = x, y = y)) +
  geom_line(color = "black") +
  geom_point(aes(color = ifelse(y < lcl | y > ucl, "red", "black")), size = 2) +
  geom_hline(aes(yintercept = cl, linetype = "CL"), color = "#0072B2", size = 0.8) +
  geom_hline(aes(yintercept = lcl, linetype = "LCL"), color = "#D55E00", size = 0.8) +
  geom_hline(aes(yintercept = ucl, linetype = "UCL"), color = "#D55E00", size = 0.8) +
  scale_color_identity() +
  scale_linetype_manual(name = "Limits", values = c("CL" = "solid", "LCL" = "dashed", "UCL" = "dashed"),
                        labels = c("CL" = paste0("Center Line (", round(qcc_chart_m2$center, 2), ")"),
                                   "LCL" = paste0("LCL (", round(qcc_chart_m2$limits[1], 2), ")"),
                                   "UCL" = paste0("UCL (", round(qcc_chart_m2$limits[2], 2), ")"))) +
  labs(title = "Xbar.one Control Chart for Part Length",
       subtitle = "Machine 2, Temperature 338K, Pressure 200kPa",
       x = "Observation",
       y = "Part Length") +
  theme_minimal() +
  theme(plot.title = element_text(size = 18),
        axis.title = element_text(size = 18),
        axis.text = element_text(size = 14),
        legend.position = "bottom",
        panel.background = element_rect(fill = "white", colour = "white"),
        plot.background = element_rect(fill = "white", colour = "white"))

p_plotly_m2 <- ggplotly(p_m2)
saveWidget(p_plotly_m2, file = "media/plots/machine2_temp338_pressure200_xbar_one_chart.html", selfcontained = TRUE)
