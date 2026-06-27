
----

:::: {{.columns}}
::: {{.column width="50%"}}
### Xbar.one Control Chart for Part Length (Machine 1, Temp: 338K, Pressure: 200kPa)

This Xbar.one control chart monitors individual observations of 'PartLength' for Machine 1 under specific conditions (Temperature = 338K, Pressure = 200kPa). It helps to identify if the process is stable and within statistical control.

**Parameters:**
*   **Target:** 50
*   **LSL:** 45
*   **USL:** 55
:::

::: {{.column width="50%"}}
<iframe data-src='media/plots/machine1_temp338_pressure200_xbar_one_chart.html' width='100%' height='500px' style='border:none;'></iframe>
:::
::::

----

:::: {{.columns}}
::: {{.column width="50%"}}
### Xbar.one Control Chart for Part Length (Machine 2, Temp: 338K, Pressure: 200kPa)

This Xbar.one control chart monitors individual observations of 'PartLength' for Machine 2 under specific conditions (Temperature = 338K, Pressure = 200kPa). It helps to identify if the process is stable and within statistical control.

**Parameters:**
*   **Target:** 50
*   **LSL:** 45
*   **USL:** 55
:::

::: {{.column width="50%"}}
<iframe data-src='media/plots/machine2_temp338_pressure200_xbar_one_chart.html' width='100%' height='500px' style='border:none;'></iframe>
:::
::::

----

:::: {{.columns}}
::: {{.column width="50%"}}
### Xbar.one Control Chart for Part Length (Machine 3, Temp: 338K, Pressure: 200kPa)

This Xbar.one control chart monitors individual observations of 'PartLength' for Machine 3 under specific conditions (Temperature = 338K, Pressure = 200kPa). It helps to identify if the process is stable and within statistical control.

**Parameters:**
*   **Target:** 50
*   **LSL:** 45
*   **USL:** 55
:::

::: {{.column width="50%"}}
<iframe data-src='media/plots/machine3_temp338_pressure200_xbar_one_chart.html' width='100%' height='500px' style='border:none;'></iframe>
:::
::::

----

:::: {{.columns}}
::: {{.column width="50%"}}
### T-Test: Part Resistance (Machine 1 vs. Machine 2)

We performed an independent two-sample t-test to compare the 'PartResistance' of products from Machine 1 and Machine 2 under specific operating conditions:

*   **Pressure:** 100kPa
*   **Temperature:** 303K

The p-value obtained from this test indicates the probability of observing such a difference (or more extreme) in part resistance between the two machines, assuming there is no actual difference.

**Observed P-value:** <span style="color:#D55E00; font-weight:bold;">0.0000</span>

**Interpretation:** Based on this p-value, we can assess whether there is a statistically significant difference in part resistance between Machine 1 and Machine 2 under these conditions.

:::

::: {{.column width="50%"}}
<iframe data-src='media/plots/machine1_vs_machine2_t_test_p_value.md' width='100%' height='500px' style='border:none;'></iframe>
:::
::::

----

:::: {{.columns}}
::: {{.column width="50%%"}}
### Visualization: Part Resistance (Machine 1 vs. Machine 2)

This boxplot visually compares the 'PartResistance' between Machine 1 and Machine 2 under conditions of 100kPa Pressure and 303K Temperature.

As indicated by the previous t-test (p-value = 0), there is a statistically significant difference in part resistance between the two machines. This boxplot illustrates that difference, with distinct distributions for each machine.

*   **Machine 1:** Shows a distribution of part resistance...
*   **Machine 2:** Shows a distribution of part resistance...

**Conclusion:** The visual evidence from the boxplot supports the t-test finding that the part resistance produced by Machine 1 is significantly different from that of Machine 2 under these specific conditions.

:::

::: {{.column width="50%%"}}
<iframe data-src='media/plots/machine1_vs_machine2_boxplot.html' width='100%%' height='500px' style='border:none;'></iframe>
:::
::::

----

:::: {{.columns}}
::: {{.column width="50%"}}
### T-Test: Part Resistance (Machine 1 vs. Machine 2, P=300, T=373)

We performed an independent two-sample t-test to compare the 'PartResistance' of products from Machine 1 and Machine 2 under specific operating conditions:

*   **Pressure:** 300kPa
*   **Temperature:** 373K

The p-value obtained from this test indicates the probability of observing such a difference (or more extreme) in part resistance between the two machines, assuming there is no actual difference.

**Observed P-value:** <span style="color:#D55E00; font-weight:bold;">0.0000</span>

**Interpretation:** Based on this p-value, we can assess whether there is a statistically significant difference in part resistance between Machine 1 and Machine 2 under these conditions.

:::

::: {{.column width="50%"}}
<iframe data-src='media/plots/machine1_vs_machine2_t_test_p300_t373_p_value.md' width='100%' height='500px' style='border:none;'></iframe>
:::
::::


---
# Bibliography
<div id="refs"></div>
