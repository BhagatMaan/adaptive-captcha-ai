# Towards Robust CAPTCHA Design: A Multi-Agent Curriculum Learning Approach with Calibration and Fairness Analysis

## 📌 Overview

This project presents an adaptive CAPTCHA framework designed to dynamically balance **security against automated attacks** and **usability for human users**.

Traditional CAPTCHA systems face a fundamental trade-off:

* Simple CAPTCHAs can be vulnerable to modern AI-based attacks such as OCR and computer vision models.
* Highly complex CAPTCHAs can negatively impact human usability and accessibility.

To address this challenge, this project proposes a **closed-loop, learning-based CAPTCHA framework** that dynamically adapts CAPTCHA difficulty based on attacker performance and human behavior.

The framework combines **multi-agent adversarial modeling, curriculum learning, human behavior modeling, entropy-based calibration, robustness evaluation, and fairness analysis**.

---

## 🎯 Problem Statement

Modern automated systems can increasingly solve static CAPTCHA mechanisms using machine learning and computer vision techniques.

Increasing CAPTCHA difficulty can improve resistance to automated attacks, but excessive difficulty can reduce human accuracy and increase response time.

Therefore, the central objective of this project is to find a balance between:

> **Security × Usability × CAPTCHA Complexity**

The proposed system dynamically adjusts CAPTCHA difficulty to maintain this balance.

---

## ⚙️ Proposed Solution

The framework consists of the following major components:

* 🤖 **Multi-Agent Adversarial Modeling** — simulates attackers with different capability levels.
* 📚 **Curriculum Learning** — progressively adjusts CAPTCHA difficulty.
* 👤 **Human Behavior Modeling** — models human accuracy, response time, and cognitive load.
* 🎯 **Entropy-Based Calibration** — evaluates the reliability and uncertainty of the system.
* ⚖️ **Fairness Analysis** — evaluates human performance across different difficulty levels.
* 📊 **Robustness Evaluation** — measures resistance against automated CAPTCHA solving.
* 🌍 **Real-World OCR Evaluation** — evaluates performance using real CAPTCHA samples and Tesseract OCR.

---

## 🧠 Key Innovation: Adaptive Robustness Index (ARI)

The project introduces the **Adaptive Robustness Index (ARI)** as a unified metric for evaluating CAPTCHA configurations.

The metric combines:

* Human usability
* Resistance to automated attacks
* CAPTCHA difficulty

The proposed formulation is:

```text
ARI = α × (Human Score) + β × (1 − Bot Success) − γ × Difficulty
```

where:

* **Human Score** represents human usability/performance.
* **Bot Success** represents the attacker's CAPTCHA-solving success rate.
* **Difficulty** represents the complexity of the generated CAPTCHA.
* **α, β, γ** are weighting parameters.

A higher ARI indicates a better balance between usability and security under the selected evaluation configuration.

---

## 🏗️ System Pipeline

```text
                CAPTCHA Generation
                       ↓
             Multi-Agent Attack Model
                       ↓
              Human Behavior Model
                       ↓
        ARI + Calibration + Fairness
                       ↓
              Curriculum Update
                       ↓
           New CAPTCHA Difficulty
                       ↺
```

The system forms a closed-loop pipeline where evaluation results influence the difficulty of subsequent CAPTCHA configurations.

---

## 🔬 Methodology

### 1. Challenge Generation

CAPTCHA difficulty is controlled through multiple parameters, including:

* **Warp**
* **Clutter**
* **Variation**
* **Entropy**

These parameters allow the system to generate CAPTCHA challenges with different complexity levels.

---

### 2. Multi-Agent Attacker Model

The framework simulates attackers with different capability levels, ranging from weak to strong automated agents.

The simulated bot success probability is modeled as:

```text
bot_success = exp(-12 × difficulty × strength)
```

where:

* `difficulty` represents CAPTCHA complexity.
* `strength` represents the attacker's capability.

This allows the system to evaluate CAPTCHA robustness against progressively stronger attackers.

---

### 3. Human Behavior Proxy

Human performance is modeled using:

* Accuracy
* Response time
* Cognitive load

This provides an estimate of the usability impact associated with increasing CAPTCHA difficulty.

---

### 4. Curriculum Learning

The CAPTCHA difficulty is adaptively updated according to the difference between the target ARI and the observed ARI.

The curriculum update rule is:

```text
delta = (target_ari - ari) + entropy_weight × entropy
```

This enables the framework to progressively adjust CAPTCHA complexity based on system performance.

---

### 5. Calibration

Entropy-based calibration is used to evaluate the reliability and uncertainty associated with the system's predictions and outcomes.

Calibration performance is evaluated using calibration error metrics.

---

### 6. Fairness Analysis

Human performance is evaluated across multiple CAPTCHA difficulty levels to understand how increasing complexity affects usability.

This allows the framework to analyze the trade-off between security improvements and human performance.

---

## 📁 Project Structure

```text
CAP_PROJ/
│
├── analysis/
│   ├── evaluator.py
│   ├── metrics.py
│   └── validation_metrics.py
│
├── core/
│   ├── attacker.py
│   ├── curriculum.py
│   ├── generator.py
│   ├── human_model.py
│   └── metrics.py
│
├── engine/
│   ├── simulator.py
│   └── logger.py
│
├── models/
│   └── trainer.py
│
├── plots/
├── real_captcha_samples/
├── results/
│
├── captcha_image_generator.py
├── config.py
├── human_ui.py
├── main.py
├── real_world_eval.py
├── visualization.py
├── verification_log.csv
├── requirements.txt
└── README.md
```

---

## 📊 Results

### Performance Metrics

| Metric                |       Result |
| --------------------- | -----------: |
| Mean ARI              |   **0.7775** |
| Bot Success Rate      |   **0.0646** |
| Human Accuracy        |     **~90%** |
| Average Response Time | **3.48 sec** |
| Stability (Std)       |   **0.0278** |

### Improvement Over Baseline

| Metric           | Baseline | Proposed System |
| ---------------- | -------: | --------------: |
| Bot Success Rate |     0.30 |      **0.0646** |
| Reduction        |        — |      **78.46%** |

The evaluated configuration shows a substantial reduction in simulated bot success compared with the baseline.

---

## 🛡️ Robustness & Validation

The framework was evaluated using multiple robustness and statistical validation metrics.

* **Worst-case ARI:** 0.7689
* **Calibration Error:** 0.0018
* **Effect Size (Cohen's d):** 6.14
* **95% Confidence Interval:** [0.7767, 0.7783]

These metrics provide additional evaluation beyond the overall ARI score and help assess stability, reliability, and statistical significance.

---

## ⚖️ Fairness Analysis

Human performance was evaluated across different CAPTCHA difficulty levels.

| Difficulty | Human Score |
| ---------- | ----------: |
| Easy       |      0.8631 |
| Medium     |      0.7987 |
| Hard       |      0.7654 |

The results illustrate the usability impact of increasing CAPTCHA difficulty and provide a basis for evaluating the security-usability trade-off.

---

## 🌍 Real-World OCR Evaluation

The framework was additionally evaluated using real CAPTCHA samples and **Tesseract OCR**.

### OCR Results

* **Average OCR Accuracy:** 0.0645
* **Maximum OCR Accuracy:** 0.5455
* **Human Accuracy:** ~90%

The results indicate a significant performance gap between automated OCR and human performance on the evaluated CAPTCHA samples.

> Note: OCR performance depends on the characteristics and difficulty of the evaluated CAPTCHA samples.

---

## 📈 Outputs

The project generates experimental data and visualizations for evaluating the adaptive CAPTCHA framework.

### Generated Data

```text
results/experiment.csv
results/failure_cases.csv
```

### Generated Visualizations

* ARI curve
* Calibration curve
* Stability analysis
* Fairness evaluation
* Security-usability trade-off
* Performance analysis

---

## 🛠️ Tech Stack

### Programming Language

* Python

### Machine Learning & Data Processing

* NumPy
* Pandas
* Scikit-learn
* LightGBM

### Computer Vision

* OpenCV
* Pillow

### Visualization

* Matplotlib

### OCR

* Tesseract OCR
* Pytesseract

### Interface

* Streamlit

---

## ▶️ How to Run

### 1. Clone the Repository

```bash
git clone https://github.com/BhagatMaan/adaptive-captcha-ai.git
cd adaptive-captcha-ai
```

### 2. Create a Virtual Environment

It is recommended to use a separate Python virtual environment.

#### Windows

```bash
python -m venv .venv
```

Activate it:

```bash
.venv\Scripts\activate
```

#### macOS / Linux

```bash
python3 -m venv .venv
```

Activate it:

```bash
source .venv/bin/activate
```

### 3. Install Python Dependencies

```bash
pip install -r requirements.txt
```

### 4. Run the Main Program

```bash
python main.py
```

---

## 🔤 Tesseract OCR Setup

The Python package `pytesseract` provides an interface to the Tesseract OCR engine, but the **Tesseract OCR application must also be installed separately** for the real-world OCR evaluation.

After installing Tesseract, make sure its executable is correctly configured for your operating system.

If required, update the Tesseract executable path in the project configuration/code.

---

## 💻 Running the Project Without Existing Libraries

The repository includes a `requirements.txt` file containing the Python dependencies required by the project.

You do **not** need to upload the `.venv` directory to GitHub.

After cloning the repository, create a fresh virtual environment and install the dependencies using:

```bash
pip install -r requirements.txt
```

This keeps the repository lightweight and makes the environment reproducible.

---

## 🚀 Future Work

Potential extensions of this project include:

* Replacing simulated attacker models with trained deep-learning attackers.
* Evaluating against larger and more diverse CAPTCHA datasets.
* Incorporating modern OCR and vision-language models.
* Expanding accessibility and fairness metrics.
* Deploying the adaptive CAPTCHA system as a web service.
* Exploring reinforcement learning for automatic CAPTCHA difficulty optimization.
* Evaluating adversarial robustness against continuously evolving AI-based attacks.

---

## ✨ Contributions of the Project

The major contributions of this project include:

1. An adaptive CAPTCHA framework based on curriculum learning.
2. Multi-agent adversarial modeling with varying attacker strengths.
3. The proposed Adaptive Robustness Index (ARI).
4. Human behavior modeling for usability evaluation.
5. Entropy-based calibration analysis.
6. Fairness analysis across CAPTCHA difficulty levels.
7. Robustness and stability evaluation.
8. Real-world OCR validation using Tesseract.
9. Automated visualization and performance analysis.

---

## 👨‍💻 Author

**Bhagat Maan**

GitHub: [@BhagatMaan](https://github.com/BhagatMaan)

---

## 📜 Usage

This project was developed for academic and research purposes.

If this repository incorporates code, datasets, models, or ideas from external sources, appropriate attribution should be provided according to their respective licenses and usage terms.
