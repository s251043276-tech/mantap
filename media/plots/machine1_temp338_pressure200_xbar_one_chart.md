# Filter data for Machine 1, Temperature 338, Pressure 200
filtered_data <- X029...029 %>% filter(Machine == 1, Temperature == 338, Pressure == 200)

# Prepare control chart data
chart_data <- filtered_data$PartLength

# Define target and limits
target_val <- 50
lsl_val <- 45
usl_val <- 55

# Create xbar.one control chart
if (length(chart_data) > 0) {
  q <- qcc(chart_data, type = "xbar.one", plot = FALSE,
           center = target_val, std.dev = sd(chart_data))
  q$s.limits <- c(lsl_val, usl_val)

  df_plot <- data.frame(
    Sample = 1:length(chart_data),
    PartLength = chart_data,
    Type = "Data Point"
  )

  center_line <- q$center
  lcl <- q$limits[1, "LCL"]
  ucl <- q$limits[1, "UCL"]

  g <- ggplot(df_plot, aes(x = Sample, y = PartLength)) +
    geom_point(aes(text = paste("Sample:", Sample, "<br>Part Length:", PartLength)), color = "#0072B2", size = 2) +
    geom_line(color = "#0072B2") +
    geom_hline(yintercept = center_line, linetype = "dashed", color = "#D55E00", linewidth = 1, aes(text = paste("Center Line:", center_line))) +
    geom_hline(yintercept = lcl, linetype = "solid", color = "#CC79A7", linewidth = 1, aes(text = paste("Lower Control Limit:", lcl))) +
    geom_hline(yintercept = ucl, linetype = "solid", color = "#CC79A7", linewidth = 1, aes(text = paste("Upper Control Limit:", ucl))) +
    geom_hline(yintercept = lsl_val, linetype = "dotdash", color = "gray", linewidth = 1, aes(text = paste("Lower Spec Limit:", lsl_val))) +
    geom_hline(yintercept = usl_val, linetype = "dotdash", color = "gray", linewidth = 1, aes(text = paste("Upper Spec Limit:", usl_val))) +
    labs(title = "Xbar.one Control Chart for Part Length (Machine 1, 338K, 200kPa)",
         x = "Sample", y = "Part Length") +
    theme_minimal() +
    theme(plot.title = element_text(size = 20, face = "bold"),
          axis.title.x = element_text(size = 18), 
          axis.title.y = element_text(size = 18),
          axis.text.x = element_text(size = 14),
          axis.text.y = element_text(size = 14),
          panel.background = element_rect(fill = "white", colour = "white"),
          plot.background = element_rect(fill = "white", colour = "white"))

  p <- ggplotly(g, tooltip = "text")

  p <- layout(p, 
              xaxis = list(title = list(text = "Sample", font = list(size = 18)), tickfont = list(size = 14)),
              yaxis = list(title = list(text = "Part Length", font = list(size = 18)), tickfont = list(size = 14)),
              plot_bgcolor = "white", 
              paper_bgcolor = "white")
  saveWidget(p, file = "media/plots/machine1_temp338_pressure200_xbar_one_chart.html", selfcontained = TRUE)
} else {
  p <- plot_ly() %>% layout(title = "No Data for Machine 1, Temp 338, Pressure 200",
                            xaxis = list(visible=F), yaxis = list(visible=F))
  saveWidget(p, file = "media/plots/machine1_temp338_pressure200_xbar_one_chart.html", selfcontained = TRUE)
}
