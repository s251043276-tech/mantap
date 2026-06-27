# Ensure the directory exists from R's perspective
dir.create('media/plots', showWarnings = FALSE)
# Filter data for the specified conditions
df_filtered_new_boxplot <- filter(get(df_actual_name), Pressure == 300, Temperature == 373, Machine == 1 | Machine == 2)

# Create a boxplot using plotly
p_new_boxplot <- plot_ly(df_filtered_new_boxplot, y = ~PartResistance, color = ~factor(Machine), type = "box")
p_new_boxplot <- layout(p_new_boxplot, title = "Part Resistance for Machine 1 vs Machine 2 (P=300, T=373)",
                yaxis = list(title = "Part Resistance"),
                xaxis = list(title = "Machine"))
saveWidget(p_new_boxplot, file = "media/plots/machine1_vs_machine2_p300_t373_boxplot.html", selfcontained = TRUE)
