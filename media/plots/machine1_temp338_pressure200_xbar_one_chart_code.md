dir.create('media/plots', showWarnings = FALSE)
df_filtered_machine1 <- get(df_actual_name) %>% filter(Machine == 1, Temperature == 338, Pressure == 200)
xbar_one_chart_machine1 <- qcc(df_filtered_machine1$PartLength, type="xbar.one", plot=FALSE)
plot_data <- data.frame(
  index = 1:length(df_filtered_machine1$PartLength),
  PartLength = df_filtered_machine1$PartLength,
  CL = xbar_one_chart_machine1$center,
  UCL = xbar_one_chart_machine1$limits[2],
  LCL = xbar_one_chart_machine1$limits[1]
)
p_part_length_machine1 <- plot_ly(plot_data, x = ~index, y = ~PartLength, type = 'scatter', mode = 'lines+markers', name = 'Part Length') %>%
  add_trace(y = ~CL, mode = 'lines', name = 'Center Line', line = list(color = '#0072B2', dash = 'dash')) %>%
  add_trace(y = ~UCL, mode = 'lines', name = 'Upper Control Limit', line = list(color = '#D55E00', dash = 'dash')) %>%
  add_trace(y = ~LCL, mode = 'lines', name = 'Lower Control Limit', line = list(color = '#D55E00', dash = 'dash')) %>%
  layout(title = "Xbar.one Control Chart for Part Length (Machine 1, Temp: 338K, Pressure: 200kPa)",
         xaxis = list(title = "Observation"),
         yaxis = list(title = "Part Length"),
         hovermode = "x unified")
saveWidget(p_part_length_machine1, file = "media/plots/machine1_temp338_pressure200_xbar_one_chart.html", selfcontained = TRUE)
