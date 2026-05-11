library(ggplot2)
library(htmlwidgets)

# Boxplot of weight distribution grouped by sex
plot_weight_by_sex <- ggplot(bigclass, aes(x = sex, y = weight, fill = sex)) +
  geom_boxplot(outlier.colour = "#CC79A7", outlier.shape = 8) +
  labs(title = 'Weight Distribution by Sex', x = 'Sex', y = 'Weight') +
  scale_fill_manual(values = c('F' = '#0072B2', 'M' = '#D55E00')) +
  theme_minimal() +
  theme(
    axis.title.x = element_text(size = 18),
    axis.title.y = element_text(size = 18),
    axis.text.x = element_text(size = 14),
    axis.text.y = element_text(size = 14),
    panel.background = element_rect(fill = 'white', colour = 'white'),
    plot.background = element_rect(fill = 'white', colour = 'white'),
    legend.position = "none"
  )

# Convert ggplot to plotly for interactivity
plotly_weight_by_sex <- ggplotly(plot_weight_by_sex)

# Save as HTML widget
saveWidget(plotly_weight_by_sex, "media/plots/weight_by_sex_boxplot.html", selfcontained = TRUE)

# Save R code
writeLines(r_code_weight_by_sex, "media/plots/weight_by_sex_boxplot.md")
