# Investigating Different Constraints for Neural Human Motion Prediction: Motion Quality & Computational Cost

## Overview

Neural networks for human motion prediction frequently suffer from physically implausible artifacts, such as foot-sliding (skating) and high-frequency jitter, especially when trained solely on kinematic data. While the research community has proposed various solutions, ranging from soft contact constraints to complex physics-informed models, their diverse formulations make direct, fair comparisons incredibly difficult.

This repository provides a **unified framework** to evaluate and improve these approaches across varied movement scenarios. By standardizing the data pipeline, network architecture, and evaluation metrics, this project investigates the critical trade-offs between:

1. **Prediction Accuracy** (e.g., joint position/rotation error)
2. **Physical Plausibility** (e.g., foot contact, bone length violations)
3. **Computational Cost** (e.g., training time, inference FPS)
4. **Human-Perceived Motion Quality** 

A core focus of this repository is an evidence-based comparison between **training-time regularisation** (e.g., loss penalties) and **external correction methods** (e.g., post-processing Inverse Kinematics).

## Key Features

* **Unified Evaluation Framework:** A standardised pipeline to plug and play different constraints and correction methods on a baseline prediction model.
* **Constraint Modules:** Implementations of various constraints including:
  * Velocity-based foot-skating penalties
  * Ground-penetration penalties
  * Acceleration & Jerk regularisation
  * Temporal velocity conservation
* **Comprehensive Metrics:** Tools to measure both standard kinematic metrics (MPJPE, NPSS) and physics-based metrics (Foot-skate ratio, penetration depth).
* **Performance Benchmarking:** Automated scripts to log computational overhead (training time, memory usage, inference latency) for each constraint type.

## Repository Structure

```text
├── configs/                 # YAML configuration files for different constraints and experiments
├── data/                    # Data loaders and preprocessing scripts (e.g., LAFAN1, AMASS)
├── model/                   # Baseline neural network architecture (MLP)
├── constraints/             # Implementations of physical constraints and regularisation methods
│   ├── losses.py            # Training-time regularisation (soft constraints)
│   └── external.py          # External correction methods (hard constraints, IK)
├── evaluation/              # Scripts for calculating accuracy, plausibility, and cost metrics
├── scripts/                 # Training and evaluation entry points
├── vis/                     # Visualization tools for generating MP4/GIFs of predicted motions
├── requirements.txt         # Project dependencies
└── README.md                # This file
```

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/sulsrk/neural-motion-prediction-constrained.git
   cd motion-prediction-constraints
   ```

2. Create and activate a virtual environment:
   ```bash
   conda create -n motion-constraints python=3.10
   conda activate motion-constraints
   ```

3. Install the dependencies:
   ```bash
   pip install -r requirements.txt
   ```

## Dataset Setup

This framework is built to be dataset-agnostic, but includes out-of-the-box support for standard datasets (e.g., LAFAN1, AMASS). 
* Please refer to `data/README.md` for instructions on downloading and preprocessing the motion capture files into the `.npy` arrays expected by the data loaders.

## Citation

If you use this code or framework in your research, please cite:

```bibtex
@misc{motion_constraints_2026,
  author = {Suleman Rahman Khan},
  title = {Investigating Different Constraints for Neural Human Motion Prediction: Motion Quality & Computational Cost},
  year = {2026},
  publisher = {GitHub},
  journal = {GitHub repository},
  howpublished = {\url{https://github.com/yourusername/motion-prediction-constraints}}
}
```