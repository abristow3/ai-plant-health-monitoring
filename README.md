# AI-Powered IoT Plant Health Monitoring and Disease Detection

Graduate research project, East Texas A&M University
**Authors:** Sang Suh, Alex Bristow

A low-cost Raspberry Pi system that combines soil and climate sensors with leaf image analysis to tell whether a plant's yellowing is caused by its environment or by likely disease.

<img src="docs/hardware.jpg" width="320" alt="Physical system">

## How it works

1. **Sense:** At a set interval the Raspberry Pi 4 reads soil moisture, soil pH, temperature, and humidity.
2. **Capture:** A USB camera photographs the plant.
3. **Detect yellowing:** `YellowDetector` converts the image to HSV, masks green and yellow pixels, and computes the percentage of leaf area that is yellow.
4. **Flag:** Readings with 20% or more yellowing are flagged.
5. **Diagnose:** `HealthModel` (XGBoost) checks the flagged reading. If the model expects no yellowing under the current conditions and those conditions are optimal, the yellowing is attributed to disease.
6. **Alert:** A red LED lights for 10 seconds when disease is detected.

## Hardware

| Component | Purpose |
|---|---|
| Raspberry Pi 4 | Central controller |
| LM393 soil moisture sensor | Soil hydration |
| Teyleten Robot pH sensor | Soil pH |
| DHT22 / AM2302 | Air temperature and humidity |
| MCP3008 ADC | Analog-to-digital conversion for the pH sensor |
| USB camera | Leaf images |
| Red LED + breadboard | Disease alert |

## Software

Python, OpenCV, XGBoost, scikit-learn, pandas, NumPy, running on Raspberry Pi OS.

## Results

The `HealthModel` was trained on 10,000 synthetic data points modelled on a miniature fig tree (80/20 train/test split) and evaluated on 200 samples.

| Metric | Value |
|---|---|
| Test accuracy | 86% |
| Class 1 (yellowing) recall | 0.93 |
| Class 1 (yellowing) precision | 0.69 |
| Confusion matrix | TN 118, FP 24, FN 4, TP 54 |

The model rarely misses a yellowing plant but produces some false positives.

## Future work

More (and real-world) training data, hyperparameter tuning, better pH sensor accuracy, a dedicated leaf-image disease model, support for more plant species, and a richer notification system.

## White paper

📄 [Download the full paper (PDF)](docs/AI_IoT_Plant_Health_Monitoring.pdf)

<details>
<summary><b>Read the paper here</b> (click to expand)</summary>
<br>

<img src="docs/paper/page-01.png" width="700" alt="Page 1"><br>
<img src="docs/paper/page-02.png" width="700" alt="Page 2"><br>
<img src="docs/paper/page-03.png" width="700" alt="Page 3"><br>
<img src="docs/paper/page-04.png" width="700" alt="Page 4"><br>
<img src="docs/paper/page-05.png" width="700" alt="Page 5"><br>
<img src="docs/paper/page-06.png" width="700" alt="Page 6"><br>
<img src="docs/paper/page-07.png" width="700" alt="Page 7"><br>
<img src="docs/paper/page-08.png" width="700" alt="Page 8"><br>
<img src="docs/paper/page-09.png" width="700" alt="Page 9"><br>
<img src="docs/paper/page-10.png" width="700" alt="Page 10"><br>
<img src="docs/paper/page-11.png" width="700" alt="Page 11"><br>
<img src="docs/paper/page-12.png" width="700" alt="Page 12"><br>
<img src="docs/paper/page-13.png" width="700" alt="Page 13"><br>
<img src="docs/paper/page-14.png" width="700" alt="Page 14"><br>
<img src="docs/paper/page-15.png" width="700" alt="Page 15"><br>
<img src="docs/paper/page-16.png" width="700" alt="Page 16"><br>
<img src="docs/paper/page-17.png" width="700" alt="Page 17"><br>
<img src="docs/paper/page-18.png" width="700" alt="Page 18"><br>

</details>
