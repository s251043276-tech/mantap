library(tidyverse)
library(plotly)
library(htmlwidgets)

# Filter data based on user request
filtered_data <- subset(df_data_r, Machine == 1 & Pressure == 200 & Temperature == 338)

if (nrow(filtered_data) > 1) {
    # Calculate control chart parameters for Xbar.one
    mean_val <- mean(filtered_data$PartLength, na.rm = TRUE)
    moving_ranges <- abs(diff(filtered_data$PartLength))
    avg_moving_range <- mean(moving_ranges, na.rm = TRUE)
    estimated_std_dev <- avg_moving_range / 1.128

    UCL <- mean_val + 3 * estimated_std_dev
    LCL <- mean_val - 3 * estimated_std_dev

    plot_data <- data.frame(
        Index = 1:nrow(filtered_data),
        PartLength = filtered_data$PartLength,
        CL = mean_val,
        UCL = UCL,
        LCL = LCL
    )

    p <- ggplot(plot_data, aes(x = Index, y = PartLength)) +
        geom_line(color = '#0072B2') +
        geom_point(color = '#0072B2') +
        geom_hline(aes(yintercept = CL), linetype = 'solid', color = '#D55E00', linewidth = 1) +
        geom_hline(aes(yintercept = UCL), linetype = 'dashed', color = '#CC79A7', linewidth = 1) +
        geom_hline(aes(yintercept = LCL), linetype = 'dashed', color = '#CC79A7', linewidth = 1) +
        labs(
            title = 'Xbar.one Control Chart for Part Length (Machine 1, 338K, 200kPa)',
            x = 'Observation Index',
            y = 'Part Length'
        ) +
        theme_minimal() +
        theme(
            plot.title = element_text(size = 18, face = 'bold'),
            axis.title.x = element_text(size = 18),
            axis.title.y = element_text(size = 18),
            axis.text.x = element_text(size = 14),
            axis.text.y = element_text(size = 14),
            panel.background = element_rect(fill = 'white', colour = NA),
            plot.background = element_rect(fill = 'white', colour = NA)
        )

    interactive_plot <- ggplotly(p)
    htmlwidgets::saveWidget(interactive_plot, 'media/plots/machine1_temp338_pressure200_xbar_one_chart.html', selfcontained = TRUE)
} else {
    print('Not enough data to create control chart for the specified conditions.')
}
