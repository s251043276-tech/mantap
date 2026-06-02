# Filter data for Machine 1, Temperature 338, Pressure 200
filtered_data <- X029...029 %>% filter(Machine == 1, Temperature == 338, Pressure == 200)

# Define target and limits
target_val <- 50
lsl_val <- 45
usl_val <- 55

# Prepare data for capability analysis
chart_data <- filtered_data$PartLength

if (length(chart_data) > 10) { # Need sufficient data for capability analysis
  process_mean <- mean(chart_data)
  process_sd <- sd(chart_data)

  df_hist <- data.frame(PartLength = chart_data)

  g <- ggplot(df_hist, aes(x = PartLength)) +
    geom_histogram(aes(y = after_stat(density), 
                       text = paste("Count:", after_stat(count), "<br>Density:", round(after_stat(density), 3))), 
                   binwidth = 0.5, fill = "#0072B2", color = "white", alpha = 0.8) +
    geom_density(color = "#D55E00", linewidth = 1) +
    geom_vline(xintercept = target_val, linetype = "dashed", color = "green", linewidth = 1.2, aes(text = paste("Target:", target_val))) +
    geom_vline(xintercept = lsl_val, linetype = "solid", color = "red", linewidth = 1.2, aes(text = paste("LSL:", lsl_val))) +
    geom_vline(xintercept = usl_val, linetype = "solid", color = "red", linewidth = 1.2, aes(text = paste("USL:", usl_val))) +
    labs(title = "Process Capability Histogram for Part Length (Machine 1, 338K, 200kPa)",
         x = "Part Length", y = "Density") +
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
              xaxis = list(title = list(text = "Part Length", font = list(size = 18)), tickfont = list(size = 14)),
              yaxis = list(title = list(text = "Density", font = list(size = 18)), tickfont = list(size = 14)),
              plot_bgcolor = "white", 
              paper_bgcolor = "white")
  saveWidget(p, file = file.path(plot_dir, "machine1_temp338_pressure200_capability_histogram.html"), selfcontained = TRUE)
} else {
  p <- plot_ly() %>% layout(title = "Not Enough Data for Capability Analysis (Machine 1, Temp 338, Pressure 200)",
                            xaxis = list(visible=F), yaxis = list(visible=F))
  saveWidget(p, file = file.path(plot_dir, "machine1_temp338_pressure200_capability_histogram.html"), selfcontained = TRUE)
}
