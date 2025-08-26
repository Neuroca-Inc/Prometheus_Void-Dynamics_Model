# Prometheus Void Dynamics Model (FUVDM) — Derivation Papers Repository

**ALWAYS FOLLOW THESE INSTRUCTIONS FIRST.** Only search for additional context or run exploratory commands if the information here is incomplete or found to be in error.

## Repository Overview

This is a **papers/documentation repository** for Void Dynamics (FUVDM) research containing theoretical derivations, validation plans, and acceptance criteria. The actual Python simulation code referenced in these papers exists in a separate private codebase but is **NOT included** in this public repository.

## What This Repository Contains

- **Derivation papers**: Theoretical work in `derivation/` covering reaction-diffusion, memory steering, fluid dynamics, and EFT approaches
- **Validation documentation**: Detailed acceptance criteria and command examples for numeric validation
- **Jupyter notebooks**: Corner testbed experiments and configuration in `notebooks/`
- **Output artifacts**: Successful validation run logs and figures in `plots/logs/` and `plots/figures/`
- **Licensing**: Dual academic/commercial license requiring written permission for commercial use

## What This Repository Does NOT Contain

- **Source code**: No Python modules, packages, or executable scripts
- **Dependencies**: No requirements.txt, setup.py, or package configuration
- **Build system**: No traditional build/test infrastructure since this is papers-only

## Working with This Repository

### Environment Setup (If You Have Access to Full Codebase)

The documentation references a Python environment with these requirements:

```bash
# Create virtual environment (cross-platform)
python3 -m venv venv

# Activate virtual environment
# On Linux/Mac:
source venv/bin/activate
# On Windows (PowerShell - original dev environment):
& .\venv\Scripts\Activate.ps1

# Install core dependencies
python -m pip install matplotlib numpy

# Note: Additional packages may be needed depending on full codebase:
# python -m pip install scipy pytest jupyter
```

**CRITICAL TIMING**: The documentation indicates some builds/tests can take substantial time:
- **NEVER CANCEL** validation runs that may take 45+ minutes
- **Set timeouts to 60+ minutes** for any build commands
- **Set timeouts to 30+ minutes** for test suites
- Individual validation scripts are typically fast (< 1 minute based on logs)

### Actual Timing From Successful Runs
Based on logged results from `plots/logs/`:
- **RD Front Speed**: ~0.27 seconds (20,972 steps)
- **RD Dispersion**: ~0.07 seconds (fast linear regime)
- **Fluid LBM Benchmarks**: 15-45 minutes (15,000+ steps typical)
- **Memory Steering**: < 1 second for 512 steps

### Known Working Validation Commands

**IMPORTANT**: These commands assume access to the full `Prometheus_FUVDM` codebase. In this public repository, these commands will fail with import errors.

#### Reaction-Diffusion Validation (Fast: ~0.3 seconds)
```bash
# Front speed validation
python code/physics/rd_front_speed_experiment.py --N 1024 --L 200 --D 1.0 --r 0.25 --T 80 --cfl 0.2 --seed 42 --x0 -60 --level 0.1 --fit_start 0.6 --fit_end 0.9

# Dispersion validation  
python code/physics/rd_dispersion_experiment.py --N 1024 --L 200 --D 1.0 --r 0.25 --T 10 --cfl 0.2 --seed 42 --amp0 1e-6 --record 80 --m_max 64 --fit_start 0.1 --fit_end 0.4

# Front speed parameter sweep
python code/physics/rd_front_speed_sweep.py
```

#### Memory Steering Validation
```bash
# Memory steering acceptance test
python -m Prometheus_FUVDM.derivation.code.physics.memory_steering.memory_steering_acceptance --seed 0 --steps 512 --g 0.12 --lam 0.08
```

#### Fluid Dynamics Benchmarks (May take 15+ minutes)
```bash
# NEVER CANCEL: Fluid simulations can take 15-45 minutes
# Set timeout to 60+ minutes

# Taylor-Green vortex benchmark
python Prometheus_FUVDM/derivation/code/physics/fluid_dynamics/taylor_green_benchmark.py --nx 256 --ny 256 --tau 0.8 --steps 5000 --sample_every 50

# Lid-driven cavity benchmark  
python Prometheus_FUVDM/derivation/code/physics/fluid_dynamics/lid_cavity_benchmark.py --nx 128 --ny 128 --tau 0.7 --U_lid 0.1 --steps 15000 --sample_every 200
```

#### Test Suite (Non-interference validation)
```bash
# NEVER CANCEL: Test suite may take 30+ minutes
# Set timeout to 45+ minutes
pytest -q .\Prometheus_FUVDM\derivation\code\tests\fluid_dynamics\test_walkers_noninterference.py
```

### Expected Output Locations

All validation scripts output to these standardized locations:
- **Figures**: `derivation/code/outputs/figures/{module}/`
- **Logs**: `derivation/code/outputs/logs/{module}/`  
- **Filenames**: `{script_name}_{YYYYMMDDTHHMMSSZ}.{json,png}`

### Validation Acceptance Criteria

#### Reaction-Diffusion (Fast validation)
- **Front speed**: `rel_err ≤ 0.05`, `R² ≥ 0.98`
- **Dispersion**: `med_rel_err ≤ 0.10`, `R²_array ≥ 0.98`
- **Expected times**: 0.1-0.3 seconds per run

#### Fluid Dynamics (Long-running validation)
- **Taylor-Green**: `|ν_fit - ν_th| / ν_th ≤ 5%`
- **Lid cavity**: `max_t ‖∇·v‖₂ ≤ 1e-6`
- **Expected times**: 15-45 minutes per benchmark
- **NEVER CANCEL**: These are normal run times, not hangs

#### Memory Steering
- **Step response**: `|p_fit - p_pred| ≤ 0.02`
- **Canonical void**: `|M_final - 0.6| ≤ 0.02` 
- **SNR improvement**: `SNR_out - SNR_in ≥ 3 dB`

### Manual Validation Scenarios

Since this is primarily a documentation repository, validate changes by:

1. **Review validation documentation completeness**:
   ```bash
   # Check all validation files exist and are complete
   ls derivation/reaction_diffusion/*validation*.md
   ls derivation/memory_steering/*acceptance*.md  
   ls BENCHMARKS_FLUIDS.md
   ```

2. **Test Jupyter notebooks** (if Jupyter available):
   ```bash
   cd notebooks/
   jupyter notebook VDM_Corner_Testbed.ipynb
   # Verify config loads: check first cell runs without error
   # Verify geometry figure displays: VDM_Corner_Geometry.png
   ```

3. **Validate log file structure**:
   ```bash
   # Check successful run artifacts exist
   ls plots/logs/reaction_diffusion/*.json
   ls plots/logs/fluid_dynamics/*.json
   ls plots/logs/memory_steering/*.json
   ```

4. **Verify YAML configuration accessibility**:
   ```bash
   # Basic file validation (PyYAML not required in this papers-only repo)
   python -c "
   with open('notebooks/VDM_corner_config.yaml') as f:
       content = f.read()
       print(f'✓ Config accessible: {len(content)} chars, {len(content.splitlines())} lines')
   "
   ```

### Cross-Platform Considerations

- **Documentation uses PowerShell syntax**: `& .\venv\Scripts\Activate.ps1`
- **On Linux/Mac use**: `source venv/bin/activate`
- **Adapt file paths**: Windows paths in logs use backslashes, adapt as needed
- **Python module imports**: Commands assume Windows-style package structure

### Key Project Structure

```
derivation/
├── FUVDM_Overview.md              # Main program overview
├── reaction_diffusion/            # RD validation (canonical baseline)
│   ├── rd_front_speed_validation.md
│   ├── rd_dispersion_validation.md
│   └── rd_validation_plan.md
├── memory_steering/               # Memory steering layer
│   └── memory_steering_acceptance_verification.md
├── fluid_dynamics/               # LBM→Navier-Stokes benchmarks
└── foundations/                  # Theoretical foundations

notebooks/
├── VDM_Corner_Testbed.ipynb     # Interactive corner test
├── VDM_corner_config.yaml       # Single source of truth config
└── VDM_Corner_Geometry.png      # Reference geometry

plots/
├── logs/                        # Validation run outputs (JSON)
└── figures/                     # Generated plots (PNG)
```

### Common Pitfalls

- **Do not try to run Python validation commands** in this repository - they will fail with import errors
- **Do not assume build/test infrastructure exists** - this is a papers-only repository  
- **Do not cancel long-running commands** - 45+ minute runtimes are normal for fluid simulations
- **Cross-platform paths**: Adapt Windows-style paths in documentation to your platform
- **Documentation focus**: Changes should prioritize theoretical accuracy and reproducibility

### License Requirements

- **Academic use permitted** for non-commercial research
- **Commercial use requires written permission** from Justin K. Lietz
- **Cite appropriately**: Reference specific validation papers when using results
- **Ethical requirements**: No weapons, surveillance, or harmful applications

Always reference the LICENSE.md file for complete terms and novel patent-pending processes.