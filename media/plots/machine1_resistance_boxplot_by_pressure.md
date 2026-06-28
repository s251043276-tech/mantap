# R Code for Boxplot: Part Resistance vs. Pressure (Machine 1)
# File: machine1_resistance_boxplot_by_pressure.md

library(dplyr)
library(plotly)
library(htmlwidgets)

# The dataframe X029___029 is assumed to be available in the R session (passed from Python).
# Filter for Machine 1
machine1_data_filtered <- X029___029 %>% filter(Machine == 1)

# Create a factor for Pressure for plotting
machine1_data_filtered$Pressure_Factor <- factor(machine1_data_filtered$Pressure)

# Create the boxplot for PartResistance by Pressure
boxplot_pressure <- plot_ly(machine1_data_filtered, y = ~PartResistance, x = ~Pressure_Factor, type = "box", 
                           boxpoints = "outliers", marker = list(color = '#0072B2')) %>% 
  layout(
    title = list(text = "Part Resistance by Pressure (Machine 1)", font = list(size = 18)),
    yaxis = list(title = list(text = "Part Resistance", font = list(size = 18)), tickfont = list(size = 14)),
    xaxis = list(title = list(text = "Pressure (kPa)", font = list(size = 18)), tickfont = list(size = 14)),
    plot_bgcolor = "white",
    paper_bgcolor = "white"
  )

# Add USL line
boxplot_pressure <- boxplot_pressure %>% 
  add_annotations(x = max(as.numeric(machine1_data_filtered$Pressure_Factor)) + 0.5, y = 10,
                  text = "USL = 10", showarrow = FALSE, yanchor = "bottom", xanchor = "left",
                  font = list(size = 14, color = "#D55E00")) %>% 
  add_trace(x = c(min(as.numeric(machine1_data_filtered$Pressure_Factor)) - 0.5, max(as.numeric(machine1_data_filtered$Pressure_Factor)) + 0.5), y = c(10, 10), mode = "lines",
            line = list(color = "#D55E00", dash = "dash"), showlegend = FALSE, inherit = FALSE)

# Save the plot as an HTML widget
boxplot_pressure_filepath <- file.path("media", "plots", paste0(boxplot_pressure_plot_name, ".html"))
saveWidget(boxplot_pressure, file = boxplot_pressure_filepath, selfcontained = TRUE)
