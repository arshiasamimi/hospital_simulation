# Hospital Bed Allocation and Patient Flow Simulation

Discrete-event simulation of a 10-bed inpatient unit with a finite queue, built for
the Computer Simulation course (Dr. Rahman Farnoosh, Spring 2026, Iran University of
Science and Technology). Patients arrive randomly, are triaged, request a bed, wait
in a finite queue if none are free, and are admitted, queued, or rejected according
to bed availability and queue capacity.

## File Structure

```
.
├── Hospital_Simulation_Full.ipynb   # Full implementation: engine, verification,
│                                     # metrics, experiments, statistical analysis
├── hospital_report.pdf              # Final report (assumptions, results, CIs,
│                                     # scenario comparison, recommendation)
├── plots and tables/                # All generated figures and CSV outputs
│                                     # (patient-level tables, hourly monitoring
│                                     # tables, replication metrics, scenario
│                                     # summaries) — produced by running the notebook
├── requirements.txt                 # Python dependencies
├── venv/                            # Local virtual environment (not tracked in git)
└── .gitignore
```

## Requirements

- Python 3.10+
- Dependencies listed in `requirements.txt` (numpy, pandas, scipy, matplotlib, and
  Jupyter)

## Setup

```bash
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

## Running the Simulation

1. Activate the virtual environment (see above).
2. Launch Jupyter and open `Hospital_Simulation_Full.ipynb`:
   ```bash
   jupyter notebook Hospital_Simulation_Full.ipynb
   ```
3. Run all cells top to bottom (**Cell → Run All**, or **Restart & Run All**).
   The notebook is self-contained and will:
   - Define and verify the discrete-event simulation engine.
   - Run the base case and generate its required visualizations.
   - Run all scenario experiments (capacity sweep, queue policy, combined
     capacity + policy, and the exponential-arrival demand stress test), each
     with 30 independent replications.
   - Build the consolidated confidence-interval comparison tables and
     practical-significance matrices.
   - Save every table (CSV) and figure (PNG) into the working directory —
     move or copy these into `plots and tables/` to reproduce that folder.

Total runtime is roughly 1-2 minutes on a typical laptop, most of it spent in the
30-replication scenario runs.

## Reproducing Results

All random seeds are derived deterministically from a scenario key and replication
index (`seed_for`), so re-running the notebook end to end reproduces the exact same
numbers reported in `hospital_report.pdf`.

## Report

`hospital_report.pdf` contains the full write-up: model assumptions, implementation
explanation, experiment design and justification, results, confidence intervals,
scenario comparisons, and the final recommendation. The LaTeX source is available on
request.

## Verification

The notebook programmatically checks, for every one of its 30-replication runs:
- No bed is double-booked.
- Occupied beds never exceed capacity; queue length never exceeds queue capacity.
- Every admitted patient has complete bed/admission/discharge records.
- Every rejected patient has a rejection reason.
- All replications use distinct random seeds.

All checks pass with zero issues across every scenario reported in this project.
