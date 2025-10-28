# Term Paper QAOA Demo — Max-Cut

This project demonstrates the Quantum Approximate Optimization Algorithm (QAOA) for a small Max-Cut instance using both Qiskit and PennyLane. It includes a classical baseline (MaxSAT via PySAT RC2 if available, or a brute-force fallback), optimization with Nelder–Mead, and sampling plots.

## Files

- Term_paper_demo.ipynb — Recommended. A narrated, step-by-step notebook where each sub-process is explained and run one at a time.

## Requirements

- Python 3.9–3.12 (tested with 3.10)
- Recommended: A virtual environment (venv or conda)
- Jupyter (Notebook or Lab)

### Python packages

- qiskit
- qiskit-aer
- pennylane
- python-sat (optional, for RC2 MaxSAT exact solver)
- networkx
- numpy
- scipy
- matplotlib
- jupyter (to run notebooks)

You can install everything at once:

```bash
pip install -U qiskit qiskit-aer pennylane python-sat networkx numpy scipy matplotlib jupyter
```

If you don’t want MaxSAT (RC2) and are fine with brute-force for small graphs, you can omit `python-sat`.

## Setup

### Option A: Python venv

```bash
python -m venv .venv
# Windows
.venv\Scripts\activate
# macOS/Linux
source .venv/bin/activate

pip install -U pip
pip install -U qiskit qiskit-aer pennylane python-sat networkx numpy scipy matplotlib jupyter
```

### Option B: Conda

```bash
conda create -n qaoa-demo python=3.10 -y
conda activate qaoa-demo
pip install -U qiskit qiskit-aer pennylane python-sat networkx numpy scipy matplotlib jupyter
```

## How to run

1) Launch Jupyter:

```bash
jupyter lab
# or
jupyter notebook
```

2) Open Term_paper_demo.ipynb (recommended for first run).

3) Run cells from top to bottom:
   - Setup and imports
   - Graph creation and visualization
   - Classical optimum (RC2 MaxSAT if python-sat is installed; otherwise brute force)
   - QAOA with Qiskit: build circuit → estimate expectation → optimize → sample
   - QAOA with PennyLane: expectation QNode → optimize → sample

4) Alternatively, open Term_paper_demo_clean.ipynb if you prefer a streamlined version with a single experiment runner cell.

## Configuration

Both notebooks expose simple configuration points:

- Graph size: n (default 6)
- Random seed: seed (default 42)
- QAOA depth: p (default 1)
- Shots for sampling: shots (default 2000)
- Optimizer iterations: qiskit_maxiter / pl_maxiter (default 80)
- Qiskit expectation mode: use_statevector (True for exact expectation; False to estimate via sampling)

Notes:
- For small n and p=1, statevector is fast and exact. For larger instances, sampling may be preferable.
- If python-sat is installed, the classical solver uses RC2 MaxSAT; otherwise it falls back to brute force.

## Troubleshooting

- qiskit-aer install errors:
  - Ensure you’re on a supported Python version and platform; most platforms have prebuilt wheels.
  - Upgrade pip: `pip install -U pip`
- PySAT (python-sat) issues:
  - If installation fails, omit `python-sat` and rely on the included brute-force baseline for small graphs.
- Backend mismatch or import errors:
  - Restart the kernel after installing dependencies.
  - Verify versions: `python --version`, `pip list | grep -E "qiskit|pennylane|python-sat|networkx|numpy|scipy|matplotlib"`

## Expected runtime

- With defaults (n=6, p=1, ~80 optimizer iterations), each framework typically completes in seconds to a couple of minutes on a laptop CPU.

## License

Academic/demo use. Adapt as needed for your term paper or experiments.
