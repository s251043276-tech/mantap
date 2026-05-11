library(ggplot2)
library(htmlwidgets)

# Scatterplot of height vs weight, colored by sex
plot_height_weight_sex <- ggplot(bigclass, aes(x = height, y = weight, color = sex)) +
  geom_point(alpha = 0.8, size = 3) +
  labs(title = 'Height vs. Weight (Colored by Sex)', x = 'Height (inches)', y = 'Weight (lbs)') +
  scale_color_manual(values = c('F' = '#D55E00', 'M' = '#0072B2')) +
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
plotly_height_weight_sex <- ggplotly(plot_height_weight_sex)

# Save as HTML widget
saveWidget(plotly_height_weight_sex, "media/plots/height_weight_scatterplot.html", selfcontained = TRUE)

# Save R code
writeLines(r_code_height_weight_sex, "media/plots/height_weight_scatterplot.md")
