library(ggplot2)
library(htmlwidgets)

# Histogram of age distribution
plot_age_histogram <- ggplot(bigclass, aes(x = age)) +
  geom_histogram(binwidth = 1, fill = '#0072B2', color = 'white') +
  labs(title = 'Distribution of Age', x = 'Age', y = 'Frequency') +
  theme_minimal() +
  theme(
    axis.title.x = element_text(size = 18),
    axis.title.y = element_text(size = 18),
    axis.text.x = element_text(size = 14),
    axis.text.y = element_text(size = 14),
    panel.background = element_rect(fill = 'white', colour = 'white'),
    plot.background = element_rect(fill = 'white', colour = 'white')
  )

# Convert ggplot to plotly for interactivity
plotly_age_histogram <- ggplotly(plot_age_histogram)

# Save as HTML widget
saveWidget(plotly_age_histogram, "media/plots/age_histogram.html", selfcontained = TRUE)

# Save R code
writeLines(r_code_age_histogram, "media/plots/age_histogram.md")
