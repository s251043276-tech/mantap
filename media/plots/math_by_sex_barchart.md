library(ggplot2)
library(htmlwidgets)

# Bar chart of average Math score by sex
plot_math_by_sex <- ggplot(bigclass, aes(x = sex, y = Math, fill = sex)) +
  stat_summary(fun = "mean", geom = "bar", position = "dodge", color = "white") +
  labs(title = 'Average Math Score by Sex', x = 'Sex', y = 'Average Math Score') +
  scale_fill_manual(values = c('F' = '#D55E00', 'M' = '#009E73')) +
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
plotly_math_by_sex <- ggplotly(plot_math_by_sex)

# Save as HTML widget
saveWidget(plotly_math_by_sex, "media/plots/math_by_sex_barchart.html", selfcontained = TRUE)

# Save R code
writeLines(r_code_math_by_sex, "media/plots/math_by_sex_barchart.md")
