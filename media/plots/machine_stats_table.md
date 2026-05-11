filtered_data <- `X029...029` %>% filter(Machine == 1, Temperature == 303, Pressure == 100)
mean_pl <- mean(filtered_data$PartLength, na.rm = TRUE)
median_pl <- median(filtered_data$PartLength, na.rm = TRUE)
sd_pl <- sd(filtered_data$PartLength, na.rm = TRUE)
mean_pr <- mean(filtered_data$PartResistance, na.rm = TRUE)
median_pr <- median(filtered_data$PartResistance, na.rm = TRUE)
sd_pr <- sd(filtered_data$PartResistance, na.rm = TRUE)
stats_df <- data.frame(
  Metric = c('Mean', 'Median', 'Standard Deviation'),
  PartLength = c(mean_pl, median_pl, sd_pl),
  PartResistance = c(mean_pr, median_pr, sd_pr)
)
p <- plot_ly(type = 'table', ... ) # Plotly table creation code
saveWidget(p, 'media/plots/machine_stats_table.html', selfcontained = TRUE)
