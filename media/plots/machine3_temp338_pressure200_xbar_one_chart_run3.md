
# R code for Xbar.one Control Chart for Machine 3, 338K, 200kPa
library(tidyverse)
library(plotly)
library(qcc)

df_machine3_filtered <- X029...029 %>% filter(Machine == 3, Temperature == 338, Pressure == 200)

xbar_one_chart_machine3 <- qcc(df_machine3_filtered$PartLength,
                               type = "xbar.one",
                               std.dev = "MR",
                               plot = FALSE,
                               center = 50)

# Extract data for plotting
plot_data_machine3 <- data.frame(
  Observation = 1:length(xbar_one_chart_machine3$data),
  PartLength = xbar_one_chart_machine3$data,
  UCL = xbar_one_chart_machine3$limits[2],
  CL = xbar_one_chart_machine3$center,
  LCL = xbar_one_chart_machine3$limits[1]
)

# Create ggplot object
p_machine3 <- ggplot(plot_data_machine3, aes(x = Observation, y = PartLength)) +
  geom_line(aes(y = PartLength), color = "#0072B2") +
  geom_point(aes(y = PartLength), color = "#0072B2") +
  geom_hline(aes(yintercept = UCL), color = "#D55E00", linetype = "dashed", linewidth = 1.0) +
  geom_hline(aes(yintercept = CL), color = "#009E73", linetype = "solid", linewidth = 1.0) +
  geom_hline(aes(yintercept = LCL), color = "#D55E00", linetype = "dashed", linewidth = 1.0) +
  geom_hline(yintercept = 50, color = "#CC79A7", linetype = "dotted", linewidth = 1.0) + # Target
  geom_hline(yintercept = 55, color = "grey", linetype = "dotted", linewidth = 1.0) + # USL
  geom_hline(yintercept = 45, color = "grey", linetype = "dotted", linewidth = 1.0) + # LSL
  annotate("text", x = max(plot_data_machine3$Observation) * 0.9, y = 50, label = "Target: 50", color = "#CC79A7", hjust = 0) +
  annotate("text", x = max(plot_data_machine3$Observation) * 0.9, y = 55, label = "USL: 55", color = "grey", hjust = 0) +
  annotate("text", x = max(plot_data_machine3$Observation) * 0.9, y = 45, label = "LSL: 45", color = "grey", hjust = 0) +
  labs(title = "Xbar.one Chart for Part Length (Machine 3, 338K, 200kPa)",
       y = "Part Length",
       x = "Observation") +
  theme_minimal() +
  theme(plot.title = element_text(size = 18),
        axis.title = element_text(size = 18),
        axis.text = element_text(size = 14),
        panel.background = element_rect(fill = "white", colour = "white"))

plotly_chart_machine3 <- ggplotly(p_machine3)

