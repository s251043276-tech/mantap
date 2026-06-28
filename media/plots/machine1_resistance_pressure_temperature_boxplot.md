# R Code for Part Resistance Box Plot (Machine 1)

machine1_data <- X029...029[X029...029$Machine == 1, ]
machine1_data$Pressure_f <- factor(machine1_data$Pressure)
machine1_data$Temperature_f <- factor(machine1_data$Temperature)

ggplot(machine1_data, aes(x = Pressure_f, y = PartResistance, fill = Temperature_f)) +
  geom_boxplot() +
  labs(
    title = 'Part Resistance Distribution by Pressure and Temperature (Machine 1)',
    x = 'Pressure',
    y = 'Part Resistance'
  ) +
  scale_fill_manual(values = c(
    '#0072B2', '#D55E00', '#009E73', '#CC79A7' # Okabe-Ito colors
  ), name = 'Temperature') +
  theme_minimal() +
  theme(
    plot.title = element_text(size = 18, hjust = 0.5),
    axis.title.x = element_text(size = 18),
    axis.title.y = element_text(size = 18),
    axis.text.x = element_text(size = 14),
    axis.text.y = element_text(size = 14),
    panel.background = element_rect(fill = 'white', colour = NA),
    plot.background = element_rect(fill = 'white', colour = NA),
    legend.title = element_text(size = 16),
    legend.text = element_text(size = 14)
  )
