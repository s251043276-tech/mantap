# Filter data for the specified conditions
df_filtered <- filter(`X029...029`, Pressure == 100, Temperature == 303, Machine == 1 | Machine == 2)

# Create a boxplot using plotly
p <- plot_ly(df_filtered, y = ~PartResistance, color = ~factor(Machine), type = "box")
p <- layout(p, title = "Part Resistance for Machine 1 vs Machine 2 (P=100, T=303)",
                yaxis = list(title = "Part Resistance"),
                xaxis = list(title = "Machine"))
saveWidget(p, file = "media/plots/machine1_vs_machine2_boxplot.html", selfcontained = TRUE)
