# Damage-Maturity-Survival-Network-Learning-When-Battery-Degradation-Happens-and-How-It-Manifests
DMSN (Damage-Maturity Survival Network) is a process-interpretable battery SOH framework. This repo provides standardized XJTU data, training/eval code, and results for reproduction.

## 1. Authors

**Cong Wang**  
School of Computer Science and Engineering, Chongqing University of Science and Technology, Chongqing 401331, China

---

## 2. Background

Accurate state-of-health (SOH) estimation is essential for reliable battery management, yet existing data-driven sequence models often achieve strong fitting performance without respecting the physical characteristics of battery degradation. Two issues remain insufficiently addressed: measured capacity is non-monotonic due to reversible recovery, and damage generated in a historical cycle may only manifest much later. Enforcing monotonicity suppresses recovery information, while assigning damage to the generation cycle ignores delayed manifestation.

This repository provides the implementation of the **Damage-Maturity Survival Network (DMSN)**, a process-interpretable framework for battery SOH estimation. 

---

## 3. Repository Contents

### 3.1 Dataset

The `data/` directory contains the standardized **XJTU** battery aging dataset used in this work. It covers six operating subsets:

| Subset | Description |
|---|---|
| XJTU-2C | Fixed 2C charging rate |
| XJTU-3C | Fixed 3C charging rate |
| XJTU-R2.5 | Variable-rate discharge, 2.5 V cutoff |
| XJTU-R3 | Variable-rate discharge, 3.0 V cutoff |
| XJTU-RW | Random-walk discharge protocol |
| XJTU-Satellite | Simulated GEO satellite cycling protocol |

Each subset includes 3σ-cleaned cycle records, SOH-normalized capacity, and battery-level train/validation/test splits. No window from a test battery is used for training, validation, feature normalization, or hyperparameter selection.

### 3.2 Data Processing

The `preprocessing/` directory contains scripts for:

- Capacity-to-SOH normalization using the reference capacity of each cell.
- Three-standard-deviation outlier removal within each battery trajectory.
- Sliding-window construction with configurable window length `L`.
- Battery-level split generation with a validation ratio of 0.125 drawn only from the training pool.
- Feature normalization using statistics computed exclusively from training batteries.

### 3.3 Model

The `models/` directory contains the DMSN implementation:

---

## 4. Results and Conclusion

DMSN achieves competitive or superior SOH estimation performance compared with data-driven, Transformer-based, and physics-informed baselines. On the heterogeneous XJTU operating conditions, DMSN obtains the best overall ranking across the evaluated subsets and metrics. Process-level validation further shows that the learned matured damage is positively correlated with irreversible SOH drop, the irreversible health component exhibits zero monotonicity violation, the learned damage remains nonnegative, and the recovery branch captures residual reversible deviations.

**Conclusion figures will be placed here.**

<!-- Figure placeholder: overall prediction comparison -->
<!-- Figure placeholder: damage-maturity consistency -->
<!-- Figure placeholder: irreversible monotonicity and recovery fitting -->

---

## 5. License and Citation

This project is released under the **Apache License 2.0**. You are free to use, modify, and distribute the code, provided that the copyright notice and license text are retained. The Apache 2.0 license also grants an express patent license from contributors.

If you use this repository or the standardized XJTU data in your research, please cite:

```bibtex
@article{wang2025dmsn,
  title   = {Damage-Maturity Survival Network: Learning When Battery Degradation Happens and How It Manifests},
  author  = {Wang, Cong},
  journal = {Preprint},
  year    = {2025}
}
```

For questions or issues, please open an issue in this repository.
