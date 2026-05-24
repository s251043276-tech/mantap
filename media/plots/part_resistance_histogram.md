
library(plotly)
library(htmlwidgets)

p_resistance_hist <- plot_ly(data = X029...029, x = ~PartResistance, type = "histogram",
                           marker = list(color = '#D55E00', line = list(color = 'white', width = 1)))
p_resistance_hist <- p_resistance_hist %>%
  layout(title = list(text = "Distribution of Part Resistance", font = list(size = 18)),
         xaxis = list(title = list(text = "Part Resistance (Ohms)", font = list(size = 18)), tickfont = list(size = 14)),
         yaxis = list(title = list(text = "Frequency", font = list(size = 18)), tickfont = list(size = 14)),
         plot_bgcolor = "white", paper_bgcolor = "white")

saveWidget(p_resistance_hist, file = "/content/project/media/plots/part_resistance_histogram.html", selfcontained = TRUE)
