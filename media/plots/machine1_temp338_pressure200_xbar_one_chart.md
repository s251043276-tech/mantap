
# R code for Xbar.one Control Chart for Part Length (Machine 1, Temp 338, Pressure 200)
library(tidyverse)
library(plotly)
library(htmlwidgets)

TARGET <- 50
USL <- 55
LSL <- 45

filtered_data <- X029...029 %>%
  filter(Machine == 1, Temperature == 338, Pressure == 200)

if (nrow(filtered_data) == 0) {
  message('No data found for Machine = 1, Temperature = 338, Pressure = 200. Plot will be empty.')
}

filtered_data$Timestamp <- as.POSIXct(filtered_data$Timestamp)

x_min <- min(filtered_data$Timestamp)
x_max <- max(filtered_data$Timestamp)

p <- plot_ly(data = filtered_data, x = ~Timestamp, y = ~PartLength, type = 'scatter', mode = 'lines+markers',
             name = 'Part Length',
             marker = list(size = 5, color = '#0072B2')) %>%
  layout(
    title = list(text = 'Xbar.one Control Chart for Part Length (Machine 1, 338K, 200kPa)', font = list(size = 18)),
    xaxis = list(title = list(text = 'Timestamp', font = list(size = 18)), tickfont = list(size = 14)),
    yaxis = list(title = list(text = 'Part Length', font = list(size = 18)), tickfont = list(size = 14)),
    shapes = list(
      list(type = 'line', x0 = x_min, x1 = x_max, y0 = TARGET, y1 = TARGET,
           line = list(color = '#D55E00', width = 2, dash = 'dash'), name = 'Target (CL)'),
      list(type = 'line', x0 = x_min, x1 = x_max, y0 = USL, y1 = USL,
           line = list(color = '#CC79A7', width = 2, dash = 'dot'), name = 'UCL'),
      list(type = 'line', x0 = x_min, x1 = x_max, y0 = LSL, y1 = LSL,
           line = list(color = '#CC79A7', width = 2, dash = 'dot'), name = 'LCL')
    ),
    showlegend = TRUE,
    plot_bgcolor = 'white',
    paper_bgcolor = 'white'
  )

p <- p %>%
  add_annotations(
  x = x_max, y = TARGET,
  text = paste('CL:', TARGET), showarrow = FALSE, xanchor = 'left', yanchor = 'bottom',
  font = list(color = '#D55E00', size = 12)
) %>%
  add_annotations(
  x = x_max, y = USL,
  text = paste('UCL:', USL), showarrow = FALSE, xanchor = 'left', yanchor = 'bottom',
  font = list(color = '#CC79A7', size = 12)
) %>%
  add_annotations(
  x = x_max, y = LSL,
  text = paste('LCL:', LSL), showarrow = FALSE, xanchor = 'left', yanchor = 'top',
  font = list(color = '#CC79A7', size = 12)
)

print(p)

