
library(qcc)
library(plotly)
library(htmlwidgets)

part_length_data <- X029...029$PartLength

q_length <- qcc(part_length_data, type="xbar.one", plot=FALSE)

p_length_i_chart <- plot_ly(data = as.data.frame(part_length_data),
                         x = ~seq_along(part_length_data), y = ~part_length_data, type = 'scatter', mode = 'lines+markers',
                         name = 'Individual Value', line = list(color = '#0072B2')) %>%
  add_trace(y = ~q_length$center, mode = 'lines', name = 'Center Line', line = list(color = 'gray', dash = 'dash')) %>%
  add_trace(y = ~q_length$limits[2,1], mode = 'lines', name = 'UCL', line = list(color = 'red', dash = 'dash')) %>%
  add_trace(y = ~q_length$limits[1,1], mode = 'lines', name = 'LCL', line = list(color = 'red', dash = 'dash')) %>%
  layout(title = list(text = "Individual Control Chart for Part Length", font = list(size = 18)),
         xaxis = list(title = list(text = "Observation Order", font = list(size = 18)), tickfont = list(size = 14)),
         yaxis = list(title = list(text = "Part Length (mm)", font = list(size = 18)), tickfont = list(size = 14)),
         showlegend = TRUE, plot_bgcolor = "white", paper_bgcolor = "white")

saveWidget(p_length_i_chart, file = "/content/project/media/plots/part_length_i_chart.html", selfcontained = TRUE)
