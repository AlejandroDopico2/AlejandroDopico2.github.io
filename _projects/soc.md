---
layout: page
title: Battery SoC Estimator
description: Huawei TechArena 2024 – Nuremberg
img: assets/img/projects/soc/diagram_cuadrado.png
importance: 1
category: hackathons
---

Ever wondered how electric vehicles or smartphones know how much battery they have left? Behind that simple percentage lies a complex estimation problem—and solving it well is critical for performance, safety, and reliability.

At the [**Huawei TechArena 2024 Hackathon in Nuremberg**](https://www.huawei.com/minisite/techarena2024/), my teammates and I faced this challenge. We built an efficient and robust **Machine Learning system** that estimates the **State of Charge (SoC)** of a lithium battery in real time.

---

### 🔋 Why SoC Estimation Matters

The **State of Charge (SoC)** tells you how full a battery is—like a fuel gauge for electricity. But measuring it isn't as simple as reading a value.

> There’s no sensor that directly tells you the SoC.

Traditionally, estimation relies on physical models or recursive filters that need to "settle" over time. But that’s a problem when conditions are changing fast—like in electric vehicles or IoT sensors, where continuous, accurate readings are crucial.

So we asked ourselves:

> Can we make an SoC estimator that’s **fast**, **accurate**, and **doesn't depend on convergence**?

---

### ⚙️ Our Approach: A Two-Stage ML Pipeline for Clean Estimation

Our solution, "Real-time Battery State of Charge Estimation: A Non-Autoregressive Machine Learning Approach," tackled the problem with a novel, two-stage ML pipeline. As computer scientists, not electrical engineers, we observed a crucial insight: while voltage and SoC are inherently linked, the raw voltage readings from sensors are often "dirty"—heavily influenced by **current** (charging/discharging) and **temperature**. These factors introduce noise, making direct SoC prediction unreliable.

To address this, our core idea was to first **clean the noisy voltage signal** before estimating the SoC. This approach allowed us to leverage the strong, almost direct relationship between a _clean_ voltage and the battery's true state of charge.

We focused on **tree-based ensemble models** (XGBoost, LightGBM, CatBoost) for both stages due to their:

- **Speed and Efficiency:** Lightweight enough for embedded systems.
- **Robustness:** Surprisingly resilient to noisy real-world data.
- **Performance:** Often more efficient than deep learning methods for this type of real-time prediction.

Our system operates in two main phases:

1.  **Offline Training Phase:** This involved extensive cross-validation, Bayesian optimization for hyperparameter tuning, and careful engineering of features to create highly performant and generalized models for both the voltage cleaner and SoC estimator.
2.  **Online Inference Phase:** This phase focused on sub-millisecond predictions, ensuring real-time performance across both stages of our pipeline.

---

### 🧠 Stage 1: The Voltage Cleaner Module

Our first critical step was to obtain a "clean" representation of the battery's voltage. Raw voltage readings are significantly affected by the **current** flowing through the battery (which can momentarily increase or decrease voltage) and **temperature**.

To filter out this "noise," we developed a dedicated **Voltage Cleaner module**, itself an ML model trained using tree-based ensembles. This module takes recent sensor readings (raw voltage, current, and temperature) and, through advanced feature engineering, learns to predict what the voltage _would be_ if these external influences were minimized.

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/soc/cleaner.png" title="Voltage Cleaner" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
Example output of our Voltage Cleaner module, showing how it denoises raw sensor voltage to reveal the underlying, "clean" voltage signal.
</div>

---

### 🧠 Stage 2: SoC Estimation from Clean Voltage

Once we had a cleaner voltage signal, the task of SoC estimation became much more direct and robust. The output from our Voltage Cleaner module, along with other relevant features, fed into our main **SoC Estimator model**.

This second tree-based model then efficiently and accurately predicts the battery's State of Charge in real time. By decoupling the noise from the core voltage signal, we achieved highly stable and reliable SoC estimates, even under rapidly changing battery conditions.

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/soc/inference_results.png" title="SoC Estimator" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
Example output of our SoC Estimator module, showing how it predicts the battery's State of Charge in real time.
</div>

---

### ⚙️ Feature Engineering: From Raw Data to Actionable Insights

For both the Voltage Cleaner and the SoC Estimator, we engineered rich features using **sliding windows** (typical in time series analysis) over:

- Recent **voltage**, **current**, and **temperature** readings.
- Statistical aggregations like mean, min, max, and standard deviation to capture temporal patterns and trends.

---

### 🚀 Real-Time Performance: Instant, Reliable Estimates

The real magic of our system lies in its real-time performance. It operates seamlessly, even on standard commodity laptops.

Just feed it new battery data, and it instantly returns SoC estimates—no warm-up, no wait, making it highly suitable for **real-world Battery Management Systems (BMS)** integration. Our system achieved **<1ms prediction latency** and **<1MB model size**, crucial metrics for edge deployment.

---

### 🔄 Full Workflow

Here’s how our non-autoregressive ML system seamlessly integrates the two stages to provide real-time SoC estimates:

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/soc/diagram.png" title="SoC Estimator" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
Our two-stage ML pipeline for real-time battery SoC estimation. Sensor data is first processed by the Voltage Cleaner, and its output then feeds into the SoC Estimator.
</div>

1.  **Collect Battery Data:** Raw voltage, current, and temperature readings are continuously collected from sensors.
2.  **Voltage Cleaner Input & Prediction:** Features are extracted from this raw data, and our dedicated Voltage Cleaner model predicts a "clean" voltage signal.
3.  **SoC Estimator Input & Prediction:** The clean voltage, along with other statistical features from raw data, are fed into the SoC Estimator model, which instantly predicts the State of Charge.
4.  **Log Predictions:** Predictions and relevant metrics are logged in real time for monitoring and analysis.

---

### 🧪 Evaluation

We rigorously validated our system across **multiple usage scenarios**, simulating various devices and operating conditions. The results consistently demonstrated **strong generalization**, providing accurate predictions even on entirely unseen battery profiles.

Through comprehensive cross-validation and automated hyperparameter tuning, we ensured our models avoided overfitting, giving us high confidence in their robustness and reliability in diverse real-world applications.

---

### 📦 Tech Stack

- Python 3.10
- XGBoost / LightGBM / CatBoost (for core ML models in both stages)
- Scikit-learn & Optuna (for model training and Bayesian optimization)
- Loguru (for efficient logging)

---

### 🏆 Second Place at Huawei TechArena 2024

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/soc/image1.png" class="img-fluid rounded z-depth-1" alt="Me during the Huawei TechArena 2024 finals in Nuremberg" %} 
  </div>
</div>
<div class="caption">
Me during the Huawei TechArena 2024 finals in Nuremberg.
</div>

This project was part of a unique and intense competition organized by **Huawei** in collaboration with **BeMyApp**. It was a multi-stage hackathon, spanning several months, culminating in an on-site final in Nuremberg, Germany.

My teammates, [**Abel Juncal Suárez**](https://www.linkedin.com/in/abel-juncal-su%C3%A1rez-52b86a240/) and [**Jorge Paz Ruza**](https://www.linkedin.com/in/jorge-paz-ruza-646141186), and I formed a team. We were thrilled to secure **second place** among many talented teams!

The competition unfolded in distinct phases:

- **Initial Online Phase (2 months):** We developed foundational algorithms with initial datasets.
- **Refinement Online Phase:** We further optimized our algorithms with more data.
- **On-Site Finals in Nuremberg:** We presented our solution, performed real-time predictions with new data, and competed against other finalists at Huawei's headquarters.

<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/soc/image2.png" class="img-fluid rounded z-depth-1" alt="Team 8 receiving second place award at Huawei TechArena 2024" %} 
  </div>
</div>
<div class="caption">
Team 8 receiving second place award at Huawei TechArena 2024.
</div>

---

### 🏁 Final Thoughts

This project was a deep dive into building an ML system that truly **needs to work in the real world**—on the edge, in real time, with imperfect signals. It highlighted that successful machine learning isn't just about achieving high accuracy in a lab setting; it's equally about **latency, reliability, and generalizability**.

The experience of competing in the Huawei TechArena 2024, collaborating with my teammates, and ultimately securing second place, was incredibly rewarding. It reinforced the importance of practical considerations in ML development and showed me just how much impact can be packed into a few hundred milliseconds of optimized Python code.

---
