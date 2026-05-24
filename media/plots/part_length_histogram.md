
library(plotly)
library(htmlwidgets)

p_length_hist <- plot_ly(data = X029...029, x = ~PartLength, type = "histogram",
                      marker = list(color = '#0072B2', line = list(color = 'white', width = 1)))
p_length_hist <- p_length_hist %>%
  layout(title = list(text = "Distribution of Part Length", font = list(size = 18)),
         xaxis = list(title = list(text = "Part Length (mm)", font = list(size = 18)), tickfont = list(size = 14)),
         yaxis = list(title = list(text = "Frequency", font = list(size = 18)), tickfont = list(size = 14)),
         plot_bgcolor = "white", paper_bgcolor = "white")

saveWidget(p_length_hist, file = "/content/project/media/plots/part_length_histogram.html", selfcontained = TRUE)
