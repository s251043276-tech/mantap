
library(tidyverse)
library(qcc)
library(plotly)
library(htmlwidgets)

# Filter the data based on user-specified conditions
filtered_data <- X029...029 %>%
  filter(Machine == 1, Pressure == 200, Temperature == 338)

# Check if filtered_data has enough data for an I-chart
if (nrow(filtered_data) < 2) { # At least two points needed for a moving range
  stop(paste0("Insufficient data: Only ", nrow(filtered_data), " observation(s) found for Machine = 1, Pressure = 200kPa, and Temperature = 338K. At least 2 observations are required to create an I-chart."))
}

if (length(unique(filtered_data$PartLength)) <= 1) { # Need variability to calculate control limits
  stop(paste0("Insufficient variability: All ", nrow(filtered_data), " PartLength values are identical for Machine = 1, Pressure = 200kPa, and Temperature = 338K. Cannot create a meaningful I-chart."))
}

# Check for NAs in PartLength and handle them
if (any(is.na(filtered_data$PartLength))) {
  warning("NA values found in PartLength. These will be removed before creating the chart.")
  filtered_data <- filtered_data %>%
    drop_na(PartLength)
}

# Diagnostic prints
print(paste0("Filtered data rows (after NA removal): ", nrow(filtered_data)))
print(paste0("Unique PartLength values (after NA removal): ", length(unique(filtered_data$PartLength))))

# More detailed diagnostics for PartLength
print("Summary of PartLength:")
print(summary(filtered_data$PartLength))
print(paste0("Standard Deviation of PartLength: ", sd(filtered_data$PartLength)))

# Calculate and summarize moving ranges
moving_ranges <- abs(diff(filtered_data$PartLength))
print("Summary of Moving Ranges:")
print(summary(moving_ranges))
print(paste0("Standard Deviation of Moving Ranges: ", sd(moving_ranges)))

# Create the I-chart QCC object for PartLength
i_chart_partlength <- qcc(filtered_data$PartLength, type="xbar.one", plot=FALSE)

# Extract limits
cl <- i_chart_partlength$center
lcl <- i_chart_partlength$limits[1]
ucl <- i_chart_partlength$limits[2]

# Prepare data for plotting
plot_data <- data.frame(
  Observation = 1:length(filtered_data$PartLength),
  PartLength = filtered_data$PartLength
)

# Create Plotly chart for PartLength
p_partlength <- plot_data %>%
  ggplot(aes(x = Observation, y = PartLength)) +
  geom_line(color = "#0072B2") +
  geom_point(color = "#0072B2", size = 2) +
  geom_hline(yintercept = cl, linetype = "dashed", color = "red", aes(text = paste("Center Line:", round(cl, 2)))) +
  geom_hline(yintercept = lcl, linetype = "dotted", color = "red", aes(text = paste("LCL:", round(lcl, 2)))) +
  geom_hline(yintercept = ucl, linetype = "dotted", color = "red", aes(text = paste("UCL:", round(ucl, 2)))) +
  labs(
    title = "I-Chart for Part Length (Machine 1, 200kPa, 338K)",
    x = "Observation Number",
    y = "Part Length"
  ) +
  theme_minimal() +
  theme(
    plot.background = element_rect(fill = "white", color = NA),
    panel.background = element_rect(fill = "white", color = NA),
    axis.title.x = element_text(size = 18),
    axis.title.y = element_text(size = 18),
    axis.text.x = element_text(size = 14),
    axis.text.y = element_text(size = 14)
  )

# Convert to plotly object
plotly_p_partlength <- ggplotly(p_partlength, tooltip = "all")

# Save Plotly widget
htmlwidgets::saveWidget(plotly_p_partlength, file = "media/plots/machine1_partlength_i_chart_filtered.html", selfcontained = TRUE)

