# IIoT Task Scheduling System

A comprehensive framework for optimizing task scheduling in Industrial Internet of Things (IIoT) environments using advanced evolutionary algorithms.

## Overview

This project implements multiple scheduling algorithms including Enhanced EPO-CEIS (an evolutionary scheduler built on Puma Optimizer operators; see [Algorithm and attribution](#algorithm-and-attribution)), Genetic Algorithm, Particle Swarm Optimization, Min-Min heuristic, and First-Fit heuristic.

## Key Features

- **Multi-algorithm scheduling framework** with comprehensive evaluation
- **Enhanced EPO-CEIS algorithm** for optimal task scheduling
- **Fog-cloud computing support** with resource optimization
- **Automated performance analysis** and visualization
- **Scalable architecture** for large-scale IIoT deployments

## Performance Results

The Enhanced EPO-CEIS algorithm demonstrates superior performance:

- **27.8% lower cost** compared to Genetic Algorithm
- **50.3% lower cost** compared to First-Fit heuristic
- **85.9% deadline hit rate** (54.9% improvement over First-Fit)
- **Consistent performance** across varying workload sizes and scenarios

## Quick Start

### Prerequisites
- Java 8+
- Python 3.8+
- 4GB RAM minimum

### Installation
```bash
# Clone the repository
git clone https://github.com/amirhosseinkho/iiot-fog-scheduling.git
cd iiot-fog-scheduling

# Install Python dependencies
pip install -r requirements.txt
```

### Running the System
```bash
# Compile Java code
javac -cp "libs/*;src" src/evaluation/MainEvaluation.java

# Run evaluation
java -cp "libs/*;src" evaluation.MainEvaluation

# Generate visualizations
python analyze_results.py
```

## Project Structure

```
iiot-fog-scheduling/
├── src/
│   ├── algorithms/          # Scheduling algorithms
│   ├── core/               # Core data structures
│   ├── evaluation/         # Evaluation framework
│   ├── simulation/         # Simulation components
│   └── utils/              # Utility functions
├── data/                   # Evaluation scenarios and datasets
├── evaluation_results/     # Evaluation results
├── analysis_plots/         # Generated visualizations
└── test/                   # Evaluation suites
```

## Algorithms

1. **Enhanced EPO-CEIS**: Primary algorithm with multi-objective optimization
2. **Genetic Algorithm**: Population-based evolutionary approach
3. **Particle Swarm Optimization**: Swarm intelligence method
4. **Min-Min Heuristic**: Greedy scheduling approach
5. **First-Fit Heuristic**: Simple resource allocation

## Results

The system generates comprehensive performance analysis including:
- Algorithm comparison charts
- Performance heatmaps
- Correlation analysis
- Statistical summaries
- Scalability analysis

All visualizations are saved in high-resolution (300 DPI) PNG format.

## Documentation

For detailed information, see [PROJECT_REPORT.md](PROJECT_REPORT.md) which includes:
- Complete system architecture
- Implementation details
- Performance analysis
- Technical specifications
- Future enhancements

## Algorithm and attribution

This repository was developed as a **course project**. The scheduling algorithm is not taken from a single paper; it combines published components as follows.

- **Search operators.** The four operators in `src/algorithms/EnhancedEPOCEIS.java` (random jump and social forage for exploration, ambush and sprint for exploitation) are discrete adaptations of the phases of the **Puma Optimizer (PO)** of Abdollahzadeh et al. (2024). "EPO" in the name refers to this enhanced Puma Optimizer. The operators run inside a genetic-algorithm loop with tournament selection and elitism (population 100, 200 generations, 10 elites).
- **Base scheduler.** `src/algorithms/CEISAlgorithm.java` is a greedy list scheduler: it visits tasks in topological order and assigns each one to the node with the lowest cost. `EPOBasedCEIS.java` is the first evolutionary version; `EnhancedEPOCEIS.java` is the final one.
- **What "Enhanced" adds:** opposition-based initialisation (Tizhoosh, 2005) mixed with random, greedy, and hybrid individuals; an exploration rate that decreases linearly and adapts to population diversity; a multi-pass deadline repair (time shift, node migration, aggressive and emergency strategies); and hill climbing on the elite solutions.
- **Objective.** For each task, cost = (execution time + transfer time + link latency) × the node's cost per second. Each missed deadline adds a penalty of 1000 × the lateness in seconds. The fitness is the sum over all tasks.

Known limitations: the fitness evaluates each task independently, so two tasks placed on the same node at overlapping times are not penalised; energy is reported but is not part of the objective; and the random generators are not seeded, so runs are not exactly repeatable.

```bibtex
@article{abdollahzadeh2024puma,
  title   = {Puma optimizer ({PO}): a novel metaheuristic optimization algorithm and its application in machine learning},
  author  = {Abdollahzadeh, Benyamin and Khodadadi, Nima and Barshandeh, Saeid and Trojovský, Pavel and Gharehchopogh, Farhad Soleimanian and El-kenawy, El-Sayed M. and Abualigah, Laith and Mirjalili, Seyedali},
  journal = {Cluster Computing},
  volume  = {27},
  number  = {4},
  pages   = {5235--5283},
  year    = {2024},
  doi     = {10.1007/s10586-023-04221-5}
}

@inproceedings{tizhoosh2005opposition,
  title     = {Opposition-Based Learning: A New Scheme for Machine Intelligence},
  author    = {Tizhoosh, Hamid R.},
  booktitle = {International Conference on Computational Intelligence for Modelling, Control and Automation (CIMCA)},
  pages     = {695--701},
  year      = {2005},
  doi       = {10.1109/CIMCA.2005.1631345}
}
```

## Citation

If you use this project in your research, please cite:

```bibtex
@software{iiot_scheduler,
  title={IIoT Task Scheduling System},
  author={Amirhossein Khoshbakht},
  year={2025},
  note={Course project},
  url={https://github.com/amirhosseinkho/iiot-fog-scheduling}
}
```

## License

MIT License. See [LICENSE](LICENSE).
