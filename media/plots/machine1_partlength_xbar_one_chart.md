
library(tidyverse)
library(qcc)
library(plotly)
library(htmlwidgets)

# Filter the data based on user-specified conditions
filtered_data_control <- X029...029 %>%
  filter(Machine == 1, Temperature == 338, Pressure == 200)

# Check if filtered_data_control has enough data for an xbar.one chart
if (nrow(filtered_data_control) < 2) { # At least two points needed for a moving range
  stop(paste0("Insufficient data: Only ", nrow(filtered_data_control), " observation(s) found for Machine = 1, Temperature = 338, and Pressure = 200. At least 2 observations are required to create an xbar.one chart."))
}

if (length(unique(filtered_data_control$PartLength)) <= 1) { # Need variability to calculate control limits
  stop(paste0("Insufficient variability: All ", nrow(filtered_data_control), " PartLength values are identical for Machine = 1, Temperature = 338, and Pressure = 200. Cannot create a meaningful xbar.one chart."))
}

# Check for NAs in PartLength and handle them
if (any(is.na(filtered_data_control$PartLength))) {
  warning("NA values found in PartLength. These will be removed before creating the chart.")
  filtered_data_control <- filtered_data_control %>%
    drop_na(PartLength)
}

# Create the xbar.one chart QCC object for PartLength
xbar_one_chart <- qcc(filtered_data_control$PartLength, type="xbar.one", plot=FALSE)

# Extract limits
cl_xbar_one <- xbar_one_chart$center
lcl_xbar_one <- xbar_one_chart$limits[1]
ucl_xbar_one <- xbar_one_chart$limits[2]

# Prepare data for plotting
plot_data_xbar_one <- data.frame(
  Observation = 1:length(filtered_data_control$PartLength),
  PartLength = filtered_data_control$PartLength
)

# Create Plotly chart for PartLength xbar.one
p_xbar_one <- plot_data_xbar_one %>%
  ggplot(aes(x = Observation, y = PartLength)) +
  geom_line(color = "#0072B2") +
  geom_point(color = "#0072B2", size = 2) +
  geom_hline(yintercept = cl_xbar_one, linetype = "dashed", color = "red", aes(text = paste("Center Line:", round(cl_xbar_one, 2)))) +
  geom_hline(yintercept = lcl_xbar_one, linetype = "dotted", color = "red", aes(text = paste("LCL:", round(lcl_xbar_one, 2)))) +
  geom_hline(yintercept = ucl_xbar_one, linetype = "dotted", color = "red", aes(text = paste("UCL:", round(ucl_xbar_one, 2)))) +
  labs(
    title = "Xbar.one Chart for Part Length (Machine 1, 338K, 200kPa)",
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
plotly_p_xbar_one <- ggplotly(p_xbar_one, tooltip = "all")

# Save Plotly widget
htmlwidgets::saveWidget(plotly_p_xbar_one, file = "media/plots/machine1_partlength_xbar_one_chart.html", selfcontained = TRUE)

