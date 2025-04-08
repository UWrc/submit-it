# submit-it
A UW-IT Research Computing community-driven collection of Slurm job submission scripts for all kinds of computing tasks—from quick tests to complex workflows on multi-GPU nodes.

This repository is intended to help researchers, analysts, and students quickly adopt and adapt Slurm scripts for their own use on Hyak.

---

## 📁 Repository Structure

Scripts are organized by **category**, with each category containing example scripts and a README:
```bash
submit-it/
├── python/
│   ├── basic-python.slurm
│   └── README.md
├── gpu/
│   ├── pytorch-training.slurm
│   ├── tensorflow.slurm
│   └── README.md
├── mpi/
│   ├── openmpi-job.slurm
│   └── README.md
├── array-jobs/
│   ├── batch-processing.slurm
│   └── README.md
└── template/
    ├── slurm-template.slurm
    └── README.md
```

## ✍️ How to Contribute

To add a new script:

1. **Choose or create a category** folder (e.g., `gpu/`, `r/`, `array-jobs/`)
2. Add your `.slurm` script and name it descriptively (e.g., `blast-array.slurm`)
3. Include header comments in your script (see below)
4. Update or create the `README.md` in that folder to explain:
   - What the script does
   - How to run it
   - Any dependencies or modules required
5. Open a pull request!

---

## ✅ Script Header Checklist

Please include these details as **comments at the top of your Slurm script**:

```bash
#!/bin/bash
#SBATCH --job-name=<your_job_name>
#SBATCH --output=logs/%x_%j.out
#SBATCH --error=logs/%x_%j.err
# %x and %j are shorthand for the job name and the job ID, great details for organizing job output files. Additionally, storing all output and error files in a logs/ directory is good practice.
#
#SBATCH --account=<your_account>
#SBATCH --partition=ckpt 
# Using ckpt as the default partition will keep your script generalized for all users
#SBATCH --nodes=1
#SBATCH --ntasks=<N>
#SBATCH --mem=<N>G # always include units - MB is default
#SBATCH --time=<time in day-hour:min:sec format, 0-00:00:00>
# 
# Description: Brief explanation of what this job does.
# Author: Your Name (optional)
# Cluster Notes: Optional notes about required resources or compatibility.
#
# Usage:
# sbatch your_script.slurm
#
# Dependencies:
# - module load xyz
# - NOTE, scripts calling conda environments require: eval "$(conda shell.bash hook)"
# - container used
# - requires input_data.csv
# - Clearly indicate where users should modify variables.