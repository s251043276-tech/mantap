# R Code for Xbar.one Control Chart: Part Resistance (Machine 1)
# File: machine1_resistance_xbar_one_chart.md

library(dplyr)
library(qcc)
library(plotly)
library(htmlwidgets)

# The dataframe X029___029 is assumed to be available in the R session (passed from Python).
# Filter for Machine 1
machine1_resistance_data <- X029___029 %>% filter(Machine == 1) %>% select(PartResistance)

resistance_values <- as.numeric(machine1_resistance_data$PartResistance)
resistance_qcc_obj <- qcc(resistance_values, type = "xbar.one", plot = FALSE, std.dev = "MR")

cl <- resistance_qcc_obj$center
ucl <- resistance_qcc_obj$limits[2]
lcl <- resistance_qcc_obj$limits[1]
usl_value <- 10

plot_data <- data.frame(
  Observation = 1:length(resistance_values),
  PartResistance = resistance_values
)

control_chart_resistance_plot <- plot_ly(plot_data, x = ~Observation, y = ~PartResistance, type = 'scatter', mode = 'lines+markers',
                                        name = 'Part Resistance', marker = list(color = '#0072B2')) %>%
  add_trace(y = cl, mode = 'lines', name = 'Center Line', line = list(color = '#009E73', dash = 'dash'), showlegend = TRUE) %>%
  add_trace(y = usl_value, mode = 'lines', name = 'USL (10)', line = list(color = '#D55E00', dash = 'dot'), showlegend = TRUE) %>%
  add_trace(y = usl_value, mode = 'none', name = '', text = 'USL = 10', hoverinfo = 'text', showlegend = FALSE) %>%
  layout(
    title = list(text = "Xbar.one Control Chart for Part Resistance (Machine 1)", font = list(size = 18)),
    xaxis = list(title = list(text = "Observation Order", font = list(size = 18)), tickfont = list(size = 14)),
    yaxis = list(title = list(text = "Part Resistance", font = list(size = 18)), tickfont = list(size = 14)),
    shapes = list(
      list(type = 'line', x0 = 0, x1 = length(resistance_values), y0 = usl_value, y1 = usl_value, line = list(color = '#D55E00', dash = 'dot', width = 2), layer = 'below')
    ),
  annotations = list(
    list(x = length(resistance_values) * 0.95, y = usl_value, text = "USL = 10", showarrow = FALSE, yshift = 10, font = list(color = '#D55E00'))
  ),
    plot_bgcolor = "white",
    paper_bgcolor = "white"
  )

if (!is.na(ucl)) {
  control_chart_resistance_plot <- control_chart_resistance_plot %>% add_trace(y = ucl, mode = 'lines', name = 'UCL', line = list(color = 'red', dash = 'dash'), showlegend = TRUE)
}
if (!is.na(lcl)) {
  control_chart_resistance_plot <- control_chart_resistance_plot %>% add_trace(y = lcl, mode = 'lines', name = 'LCL', line = list(color = 'red', dash = 'dash'), showlegend = TRUE)
}

control_chart_resistance_html_filepath <- file.path("media", "plots", paste0(control_chart_resistance_plot_name, ".html"))
saveWidget(control_chart_resistance_plot, file = control_chart_resistance_html_filepath, selfcontained = TRUE)
