
library(qcc)
library(plotly)
library(htmlwidgets)

# Prepare data for I-MR chart for PartResistance
part_resistance_data <- X029...029$PartResistance

# Create I-MR chart objects
q_resistance <- qcc(part_resistance_data, type="xbar.one", plot=FALSE)

# Get UCL and LCL for Moving Range safely
ucl_mr_resistance <- if (!is.null(q_resistance$s.limits) && nrow(q_resistance$s.limits) >= 2) q_resistance$s.limits[2,1] else NA
lcl_mr_resistance <- if (!is.null(q_resistance$s.limits) && nrow(q_resistance$s.limits) >= 1) q_resistance$s.limits[1,1] else NA

# Create plotly plot for Moving Range chart
p_resistance_mr_chart <- plot_ly(data = as.data.frame(q_resistance$s),
                             x = ~seq_along(q_resistance$s), y = ~q_resistance$s, type = 'scatter', mode = 'lines+markers',
                             name = 'Moving Range', line = list(color = '#D55E00')) %>% add_trace(y = ~q_resistance$s.center, mode = 'lines', name = 'Center Line', line = list(color = 'gray', dash = 'dash'))

# Add UCL and LCL only if they are not NA
if (!is.na(ucl_mr_resistance)) {
  p_resistance_mr_chart <- p_resistance_mr_chart %>% add_trace(y = ucl_mr_resistance, mode = 'lines', name = 'UCL', line = list(color = 'red', dash = 'dash'))
}
if (!is.na(lcl_mr_resistance)) {
  p_resistance_mr_chart <- p_resistance_mr_chart %>% add_trace(y = lcl_mr_resistance, mode = 'lines', name = 'LCL', line = list(color = 'red', dash = 'dash'))
}

p_resistance_mr_chart <- p_resistance_mr_chart %>% layout(title = list(text = "Moving Range Control Chart for Part Resistance", font = list(size = 18)), xaxis = list(title = list(text = "Observation Order", font = list(size = 18)), tickfont = list(size = 14)), yaxis = list(title = list(text = "Moving Range (Ohms)", font = list(size = 18)), tickfont = list(size = 14)), showlegend = TRUE, plot_bgcolor = "white", paper_bgcolor = "white")

saveWidget(p_resistance_mr_chart, file = "/content/project/media/plots/part_resistance_mr_chart.html", selfcontained = TRUE)
