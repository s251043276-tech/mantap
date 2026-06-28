# R Code for Boxplot: Part Resistance vs. Temperature (Machine 1)
# File: machine1_resistance_boxplot_by_temperature.md

library(dplyr)
library(plotly)
library(htmlwidgets)

# The dataframe X029___029 is assumed to be available in the R session (passed from Python).
# Filter for Machine 1
machine1_data_filtered <- X029___029 %>% filter(Machine == 1)

# Create a factor for Temperature for plotting
machine1_data_filtered$Temperature_Factor <- factor(machine1_data_filtered$Temperature)

# Create the boxplot for PartResistance by Temperature
boxplot_temperature <- plot_ly(machine1_data_filtered, y = ~PartResistance, x = ~Temperature_Factor, type = "box", 
                           boxpoints = "outliers", marker = list(color = '#D55E00')) %>% 
  layout(
    title = list(text = "Part Resistance by Temperature (Machine 1)", font = list(size = 18)),
    yaxis = list(title = list(text = "Part Resistance", font = list(size = 18)), tickfont = list(size = 14)),
    xaxis = list(title = list(text = "Temperature (K)", font = list(size = 18)), tickfont = list(size = 14)),
    plot_bgcolor = "white",
    paper_bgcolor = "white"
  )

# Add USL line
boxplot_temperature <- boxplot_temperature %>% 
  add_annotations(x = max(as.numeric(machine1_data_filtered$Temperature_Factor)) + 0.5, y = 10,
                  text = "USL = 10", showarrow = FALSE, yanchor = "bottom", xanchor = "left",
                  font = list(size = 14, color = "#D55E00")) %>% 
  add_trace(x = c(min(as.numeric(machine1_data_filtered$Temperature_Factor)) - 0.5, max(as.numeric(machine1_data_filtered$Temperature_Factor)) + 0.5), y = c(10, 10), mode = "lines",
            line = list(color = "#D55E00", dash = "dash"), showlegend = FALSE, inherit = FALSE)

# Save the plot as an HTML widget
boxplot_temperature_filepath <- file.path("media", "plots", paste0(boxplot_temperature_plot_name, ".html"))
saveWidget(boxplot_temperature, file = boxplot_temperature_filepath, selfcontained = TRUE)
