
library(qcc)
library(plotly)
library(htmlwidgets)

# Prepare data for I-MR chart for PartLength
part_length_data <- X029...029$PartLength

# Create I-MR chart objects
q_length <- qcc(part_length_data, type="xbar.one", plot=FALSE)

# Get UCL and LCL for Moving Range safely
ucl_mr_length <- if (!is.null(q_length$s.limits) && nrow(q_length$s.limits) >= 2) q_length$s.limits[2,1] else NA
lcl_mr_length <- if (!is.null(q_length$s.limits) && nrow(q_length$s.limits) >= 1) q_length$s.limits[1,1] else NA

# Create plotly plot for Moving Range chart
p_length_mr_chart <- plot_ly(data = as.data.frame(q_length$s),
                           x = ~seq_along(q_length$s), y = ~q_length$s, type = 'scatter', mode = 'lines+markers',
                           name = 'Moving Range', line = list(color = '#0072B2')) %>% add_trace(y = ~q_length$s.center, mode = 'lines', name = 'Center Line', line = list(color = 'gray', dash = 'dash'))

# Add UCL and LCL only if they are not NA
if (!is.na(ucl_mr_length)) {
  p_length_mr_chart <- p_length_mr_chart %>% add_trace(y = ucl_mr_length, mode = 'lines', name = 'UCL', line = list(color = 'red', dash = 'dash'))
}
if (!is.na(lcl_mr_length)) {
  p_length_mr_chart <- p_length_mr_chart %>% add_trace(y = lcl_mr_length, mode = 'lines', name = 'LCL', line = list(color = 'red', dash = 'dash'))
}

p_length_mr_chart <- p_length_mr_chart %>% layout(title = list(text = "Moving Range Control Chart for Part Length", font = list(size = 18)), xaxis = list(title = list(text = "Observation Order", font = list(size = 18)), tickfont = list(size = 14)), yaxis = list(title = list(text = "Moving Range (mm)", font = list(size = 18)), tickfont = list(size = 14)), showlegend = TRUE, plot_bgcolor = "white", paper_bgcolor = "white")

saveWidget(p_length_mr_chart, file = "/content/project/media/plots/part_length_mr_chart.html", selfcontained = TRUE)
