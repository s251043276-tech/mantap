---
title-slide: false
bibliography: references.bib
csl: vancouver.csl
citeproc: true
theme: serif
background-color: "#ffffff"
transition: slide
navigationMode: linear
hash: true
---

:::: {.columns}
::: {.column width="50%"}

## Sample slides
#### PlaceHolderName
#### Universiti Malaysia Perlis
#### [placeholder@email.com](mailto:placeholder@email.com)

<audio id="bg-music" src="media/audio/sb.m4a" loop></audio>

<div id="audio-credit"
     style="position: absolute; bottom: 40px; right: 20px; font-size: 0.6em; opacity: 0.6;">
  Music: “Adrift” by Scott Buckley (CC BY 4.0)
</div>

<script>
  document.addEventListener('DOMContentLoaded', () => {
    const audio = document.getElementById('bg-music');
    const credit = document.getElementById('audio-credit');

    // hide credit by default
    credit.style.display = 'none';

    const test = new Audio('media/audio/bgm.mp3');

    test.addEventListener('canplaythrough', () => {
      // bgm.mp3 exists → use it, keep credit hidden
      audio.src = 'media/audio/bgm.mp3';
    }, { once: true });

    test.addEventListener('error', () => {
      // bgm.mp3 missing → sb.m4a will play → show credit
      credit.style.display = 'block';
    }, { once: true });

    document.addEventListener('click', () => {
      if (Reveal.getIndices().h === 0) {
        audio.volume = 0.5;
        audio.play();
      }
    }, { once: true });

    Reveal.on('slidechanged', (event) => {
      if (event.indexh > 0) { audio.pause(); }
      else { audio.play(); }
    });
  });
</script>

:::

::: {.column width="50%"}
![](media/pics/logo1.png)
:::

::::

---

:::: {.columns}
::: {.column width="50%"}
### Slide one
**Key Concepts:**
- Energy conservation per @carnot1824.
- $\Delta U = Q - W$
:::

::: {.column width="50%"}
![](media/pics/sample.png)
:::
::::

---

<span class="slide-title" data-title="My Hidden Slide Name"></span>

![](media/pics/wide.jpeg)

---

:::: {.columns}
::: {.column width="50%"}
### The Master Equation
The fundamental relation of thermodynamics:

$$\Delta U = Q - W$$

The work done $W$ is positive when the system expands against an external pressure.
:::

::: {.column width="50%"}
<video data-src="media/videos/sample.mp4" data-autoplay loop muted width="100%"></video>
:::

::::

---

:::: {.columns}
::: {.column width="50%"}
### Visualizing the Gas Law
**Interactive Model:**

- P, V, and T relationships.
- Use the slider to adjust pressure.
- Observe the phase boundary.
:::

::: {.column width="50%"}
<iframe 
  data-src="media/plots/sample.html" 
  width="100%" 
  height="500px" 
  style="border:none;" 
  scrolling="no">
</iframe>
:::
::::

---

# Bibliography
<div id="refs"></div>

---

:::: {.columns}
::: {.column width="50%"}
### Distribution of Age

This histogram illustrates the frequency distribution of ages within the dataset.
:::

::: {.column width="50%"}
<iframe data-src='media/plots/age_histogram.html' width='100%' height='500px' style='border:none;'></iframe>
:::
::::

---

:::: {.columns}
::: {.column width="50%"}
### Average Math Score by Sex

This bar chart compares the average Math scores between male and female students in the dataset.
:::

::: {.column width="50%"}
<iframe data-src='media/plots/math_by_sex_barchart.html' width='100%' height='500px' style='border:none;'></iframe>
:::
::::

---

:::: {.columns}
::: {.column width="50%"}
### Weight Distribution by Sex

This boxplot visualizes the distribution of weight, grouped by sex, showing median, quartiles, and outliers.
:::

::: {.column width="50%"}
<iframe data-src='media/plots/weight_by_sex_boxplot.html' width='100%' height='500px' style='border:none;'></iframe>
:::
::::

---

:::: {.columns}
::: {.column width="50%"}
### Height vs. Weight (Colored by Sex)

This scatterplot shows the relationship between height and weight, with points colored to distinguish between sexes.
:::

::: {.column width="50%"}
<iframe data-src='media/plots/height_weight_scatterplot.html' width='100%' height='500px' style='border:none;'></iframe>
:::
::::

---

:::: {.columns}
::: {.column width="50%"}
### Key Statistics for Machine 1 (Temp 303, Pressure 100)

This table summarizes the mean, median, and standard deviation for 'PartLength' and 'PartResistance' under specific operating conditions (Machine 1, Temperature 303, Pressure 100).
:::

::: {.column width="50%"}
<iframe data-src='media/plots/machine_stats_table.html' width='100%' height='500px' style='border:none;'></iframe>
:::
::::

---

:::: {.columns}
::: {.column width="50%"}
### Distribution of Part Length

This histogram illustrates the frequency distribution of 'PartLength' in the dataset, providing insight into the typical lengths of the output parts.
:::

::: {.column width="50%"}
<iframe data-src='media/plots/part_length_histogram.html' width='100%' height='500px' style='border:none;'></iframe>
:::
::::

---

:::: {.columns}
::: {.column width="50%"}
### Distribution of Part Resistance

This histogram displays the distribution of 'PartResistance', helping to understand the variability and typical resistance values of the output product.
:::

::: {.column width="50%"}
<iframe data-src='media/plots/part_resistance_histogram.html' width='100%' height='500px' style='border:none;'></iframe>
:::
::::

---

:::: {.columns}
::: {.column width="50%"}
### Control Chart for Part Length

This Individual and Moving Range (I-MR) control chart for 'PartLength' helps to monitor process stability over time. The Individual chart tracks individual data points, while the Moving Range chart monitors process variability.
:::

::: {.column width="50%"}
<iframe data-src='media/plots/part_length_i_chart.html' width='100%' height='500px' style='border:none;'></iframe>
:::
::::

---

:::: {.columns}
::: {.column width="50%"}
### Control Chart for Part Resistance

This Individual and Moving Range (I-MR) control chart for 'PartResistance' helps to monitor process stability over time. The Individual chart tracks individual data points, while the Moving Range chart monitors process variability.
:::

::: {.column width="50%"}
<iframe data-src='media/plots/part_resistance_i_chart.html' width='100%' height='500px' style='border:none;'></iframe>
:::
::::

---

:::: {.columns}
::: {.column width="50%"}
### Moving Range Control Chart for Part Length

This Moving Range (MR) chart for 'PartLength' monitors the process variability over time. It helps detect shifts in the process variation that the Individual chart might not catch. A stable MR chart indicates consistent process variation.
:::

::: {.column width="50%"}
<iframe data-src='media/plots/part_length_mr_chart.html' width='100%' height='500px' style='border:none;'></iframe>
:::
::::

---

:::: {.columns}
::: {.column width="50%"}
### Moving Range Control Chart for Part Resistance

This Moving Range (MR) chart for 'PartResistance' monitors the process variability over time. It helps detect shifts in the process variation that the Individual chart might not catch. A stable MR chart indicates consistent process variation.
:::

::: {.column width="50%"}
<iframe data-src='media/plots/part_resistance_mr_chart.html' width='100%' height='500px' style='border:none;'></iframe>
:::
::::
