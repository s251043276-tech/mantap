```R # Load libraries
library(tidyverse)
library(qcc)
library(plotly)
library(htmlwidgets)
library(ggplot2) 
# Filter data
filtered_data <- X029...029 %>% filter(Machine == 1, Temperature == 338, Pressure == 200) 
# Extract PartLength
part_length_data <- filtered_data$PartLength 
# Define parameters
target_val <- 50
lsl_val <- 45
usl_val <- 55 
# Calculate center and std.dev from the filtered data
center_val <- mean(part_length_data, na.rm = TRUE)
std_dev_val <- sd(part_length_data, na.rm = TRUE) 
# Create the xbar.one control chart
xbar_one_chart <- qcc(part_length_data,                       type = "xbar.one",
                      plot = FALSE,
                      std.dev = std_dev_val,
                      center = center_val,
                      sizes = 1) # Individual observations 
# Add specification limits
xbar_one_chart$spec.limits <- c(lsl_val, usl_val) xbar_one_chart$target <- target_val 
# Convert qcc object to a data frame for ggplot2
chart_data <- data.frame(   sample = 1:length(xbar_one_chart$data),
  value = xbar_one_chart$data,
  center = xbar_one_chart$center,
  lcl = xbar_one_chart$limits[, "LCL"],
  ucl = xbar_one_chart$limits[, "UCL"]
) 
# Plot using ggplot2
p <- ggplot(chart_data, aes(x = sample, y = value)) +   geom_line(color = "#0072B2") +
  geom_point(color = "#0072B2", size = 2) +   geom_hline(aes(yintercept = center), linetype = "dashed", color = "#D55E00") +   geom_hline(aes(yintercept = lcl), linetype = "dashed", color = "#009E73") +   geom_hline(aes(yintercept = ucl), linetype = "dashed", color = "#CC79A7") +   geom_hline(yintercept = target_val, linetype = "solid", color = "black", size = 0.8) +   geom_hline(yintercept = lsl_val, linetype = "dotted", color = "red", size = 0.8) +   geom_hline(yintercept = usl_val, linetype = "dotted", color = "red", size = 0.8) +   annotate("text", x = max(chart_data$sample) + 0.5, y = chart_data$center, label = "CL", hjust = 0, vjust = 0.5, color = "#D55E00", size = 4) +   annotate("text", x = max(chart_data$sample) + 0.5, y = chart_data$lcl, label = "LCL", hjust = 0, vjust = 0.5, color = "#009E73", size = 4) +   annotate("text", x = max(chart_data$sample) + 0.5, y = chart_data$ucl, label = "UCL", hjust = 0, vjust = 0.5, color = "#CC79A7", size = 4) +   annotate("text", x = max(chart_data$sample) + 0.5, y = target_val, label = "Target", hjust = 0, vjust = 0.5, color = "black", size = 4) +   annotate("text", x = max(chart_data$sample) + 0.5, y = lsl_val, label = "LSL", hjust = 0, vjust = 0.5, color = "red", size = 4) +   annotate("text", x = max(chart_data$sample) + 0.5, y = usl_val, label = "USL", hjust = 0, vjust = 0.5, color = "red", size = 4) +   labs(     title = "Xbar.one Control Chart for Part Length (Machine 1, 338K, 200kPa)",
    x = "Observation Number",
    y = "Part Length"
  ) +   theme_minimal() +
  theme(     plot.title = element_text(size = 18, face = "bold"),
    axis.title = element_text(size = 18),
    axis.text = element_text(size = 14),
    panel.background = element_rect(fill = "white", colour = NA),
    plot.background = element_rect(fill = "white", colour = NA)
  ) 
# Convert to plotly
p_plotly <- ggplotly(p) 
# Save the widget
saveWidget(p_plotly, "media/plots/machine1_temp338_pressure200_xbar_one_chart_new.html", selfcontained = TRUE) ```
