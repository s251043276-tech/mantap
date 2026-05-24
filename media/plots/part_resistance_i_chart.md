
library(qcc)
library(plotly)
library(htmlwidgets)

part_resistance_data <- X029...029$PartResistance

q_resistance <- qcc(part_resistance_data, type="xbar.one", plot=FALSE)

p_resistance_i_chart <- plot_ly(data = as.data.frame(part_resistance_data),
                         x = ~seq_along(part_resistance_data), y = ~part_resistance_data, type = 'scatter', mode = 'lines+markers',
                         name = 'Individual Value', line = list(color = '#D55E00')) %>%
  add_trace(y = ~q_resistance$center, mode = 'lines', name = 'Center Line', line = list(color = 'gray', dash = 'dash')) %>%
  add_trace(y = ~q_resistance$limits[2,1], mode = 'lines', name = 'UCL', line = list(color = 'red', dash = 'dash')) %>%
  add_trace(y = ~q_resistance$limits[1,1], mode = 'lines', name = 'LCL', line = list(color = 'red', dash = 'dash')) %>%
  layout(title = list(text = "Individual Control Chart for Part Resistance", font = list(size = 18)),
         xaxis = list(title = list(text = "Observation Order", font = list(size = 18)), tickfont = list(size = 14)),
         yaxis = list(title = list(text = "Part Resistance (Ohms)", font = list(size = 18)), tickfont = list(size = 14)),
         showlegend = TRUE, plot_bgcolor = "white", paper_bgcolor = "white")

saveWidget(p_resistance_i_chart, file = "/content/project/media/plots/part_resistance_i_chart.html", selfcontained = TRUE)
