# VHDL-FORGE 3.0 - System Specification

**Version:** 3.0.0
**Last Updated:** 2025-11-08
**Purpose:** System dependencies and container setup for VHDL development with CocoTB testing

---

## Overview

VHDL-FORGE is a batteries-included VHDL framework for Moku custom instrument development, featuring:
- Reusable VHDL components with GHDL simulation
- CocoTB progressive testing (98% output reduction)
- AI-assisted development workflows
- FORGE calling convention + Hierarchical Voltage Scheme (HVS)

This specification documents **system-level dependencies** for container-friendly deployment and fork workflows.

---

## System Dependencies

### Critical: GHDL (VHDL Simulator)

**Minimum Version:** GHDL 5.0.1 or later
**Reference System:**
```
GHDL 5.0.1 (4.1.0.r602.g37ad91899) [Dunoon edition]
 Compiled with GNAT Version: 14.2.0
 llvm 19.1.7 code generator
```

**Why:** GHDL is the VHDL simulator used by CocoTB for all hardware testing. GHDL 5.0+ provides:
- VHDL-2008 support (required for `forge_*` components)
- LLVM backend for faster simulation
- Stable VPI/VHPI interface for CocoTB

**Installation:**

<details>
<summary><b>Ubuntu/Debian (apt)</b></summary>

```bash
# Add GHDL PPA (for latest versions)
sudo add-apt-repository ppa:ghdl/ghdl
sudo apt update
sudo apt install ghdl ghdl-llvm

# Verify installation
ghdl --version  # Should show 5.0.1 or later
```
</details>

<details>
<summary><b>macOS (Homebrew)</b></summary>

```bash
# Install GHDL via Homebrew
brew install ghdl

# Verify installation
ghdl --version  # Should show 5.0.1 or later
```
</details>

<details>
<summary><b>Docker/Container (Recommended for CI/CD)</b></summary>

```dockerfile
# Use official GHDL image (guarantees 5.0.1+)
FROM ghdl/ghdl:ubuntu22-llvm-5.0

# Install Python + uv (for CocoTB)
RUN apt-get update && \
    apt-get install -y python3 python3-pip curl && \
    curl -LsSf https://astral.sh/uv/install.sh | sh

# Set up workspace
WORKDIR /workspace
COPY . .

# Install Python dependencies
RUN uv sync

# Verify GHDL
RUN ghdl --version
```

**Official GHDL Docker images:** https://github.com/ghdl/docker
</details>

<details>
<summary><b>From Source (Manual Build)</b></summary>

```bash
# Install build dependencies
sudo apt install gnat llvm llvm-dev zlib1g-dev

# Clone GHDL
git clone https://github.com/ghdl/ghdl.git
cd ghdl

# Checkout stable 5.0.1
git checkout v5.0.1

# Configure with LLVM backend
./configure --with-llvm-config=llvm-config --prefix=/usr/local

# Build and install
make
sudo make install

# Verify
ghdl --version
```
</details>

---

### Python Environment

**Python Version:** 3.10 or later
**Package Manager:** uv (recommended) or pip

**Why:** CocoTB requires Python 3.10+ for HDL testbenches. `uv` provides faster, reproducible installs.

**Installation:**

```bash
# Install uv (recommended)
curl -LsSf https://astral.sh/uv/install.sh | sh

# OR use pip
pip install cocotb pytest
```

**Dependencies (managed via `uv sync`):**
- `cocotb` - HDL testbench framework
- `pytest` - Python unit testing
- `pyyaml` - Configuration parsing
- Custom packages: `forge_cocotb`, `forge_platform`, `forge_tools`

---

### Optional: Wave Viewer (for debugging)

**GTKWave** - VCD/FST waveform viewer

```bash
# Ubuntu/Debian
sudo apt install gtkwave

# macOS
brew install gtkwave
```

**Why:** View GHDL simulation waveforms (`.vcd`/`.fst` files) for debugging.

---

## Environment Setup

### Quick Start (Local Development)

```bash
# 1. Clone repository
git clone https://github.com/sealablab/vhdl-forge-3v0.git
cd vhdl-forge-3v0

# 2. Verify GHDL installation
ghdl --version  # Must be 5.0.1+

# 3. Install Python dependencies
uv sync

# 4. Run tests
uv run python cocotb_tests/run.py --list
uv run python cocotb_tests/run.py forge_util_clk_divider
```

---

### Container Setup (Claude Code Web / Fork Workflow)

**Use Case:** Running VHDL-FORGE in containerized environments (Claude Code Web, GitHub Codespaces, CI/CD).

#### Option 1: Dev Container (VSCode/Claude Code Web)

Create `.devcontainer/devcontainer.json`:

```json
{
  "name": "VHDL-FORGE 3.0",
  "image": "ghdl/ghdl:ubuntu22-llvm-5.0",

  "features": {
    "ghcr.io/devcontainers/features/python:1": {
      "version": "3.11"
    }
  },

  "postCreateCommand": "curl -LsSf https://astral.sh/uv/install.sh | sh && uv sync",

  "customizations": {
    "vscode": {
      "extensions": [
        "puorc.awesome-vhdl",
        "ms-python.python"
      ]
    }
  }
}
```

**Benefits:**
- ✅ Automatic GHDL 5.0.1 setup
- ✅ Reproducible environment
- ✅ Works in Claude Code Web, GitHub Codespaces, local VSCode

#### Option 2: Docker Compose (Multi-Service)

Create `docker-compose.yml`:

```yaml
version: '3.8'

services:
  vhdl-forge:
    image: ghdl/ghdl:ubuntu22-llvm-5.0
    working_dir: /workspace
    volumes:
      - .:/workspace
    command: bash -c "curl -LsSf https://astral.sh/uv/install.sh | sh && uv sync && bash"
    stdin_open: true
    tty: true
```

**Usage:**
```bash
docker-compose up -d
docker-compose exec vhdl-forge uv run python cocotb_tests/run.py --list
```

---

## Verification Checklist

Use this checklist to verify your environment is correctly configured:

```bash
# 1. Check GHDL version (must be 5.0.1+)
ghdl --version | grep "5.0"

# 2. Check Python version (must be 3.10+)
python3 --version

# 3. Check uv installation
uv --version

# 4. Install dependencies
uv sync

# 5. Run basic test (should pass in <10 seconds)
uv run python cocotb_tests/run.py forge_util_clk_divider

# 6. Expected output: ~20 lines, all tests PASS
```

**Success Criteria:**
- ✅ GHDL 5.0.1+ detected
- ✅ Python 3.10+ detected
- ✅ `uv sync` completes without errors
- ✅ `forge_util_clk_divider` P1 tests pass (~20 line output)

---

## Common Issues

### Issue 1: GHDL not found

```bash
# Symptom
ghdl: command not found

# Solution
# Install GHDL 5.0.1+ (see installation section above)
```

### Issue 2: GHDL version too old

```bash
# Symptom
GHDL 4.x detected (need 5.0.1+)

# Solution (Ubuntu)
sudo add-apt-repository ppa:ghdl/ghdl
sudo apt update
sudo apt install ghdl ghdl-llvm --reinstall
```

### Issue 3: CocoTB can't find GHDL

```bash
# Symptom
cocotb.simulator.SimulatorBase: Unable to locate GHDL

# Solution
export PATH=$PATH:/usr/local/bin  # Adjust to your GHDL install path
ghdl --version  # Verify accessible
```

### Issue 4: Python version mismatch

```bash
# Symptom
Python 3.9 or earlier detected

# Solution (Ubuntu)
sudo apt install python3.11 python3.11-venv
python3.11 -m pip install uv
```

---

## Architecture Dependencies

### VHDL Components → GHDL

All VHDL components (`vhdl/packages/`, `vhdl/components/`) require:
- GHDL 5.0.1+ for VHDL-2008 syntax
- LLVM backend for performance (recommended, not required)

### CocoTB Tests → GHDL + Python

All CocoTB tests (`cocotb_tests/`) require:
- GHDL 5.0.1+ as simulator backend
- Python 3.10+ with `cocotb` package
- `forge_cocotb` testing framework (provided)

### Python Tools → No GHDL

Python utilities (`python/forge_tools/`) work standalone:
- No GHDL required
- Used for register decoding, HVS analysis, utilities

---

## Fork Workflow

**When forking VHDL-FORGE for custom instruments:**

1. **Check system dependencies:**
   ```bash
   ghdl --version  # 5.0.1+
   python3 --version  # 3.10+
   ```

2. **Clone your fork:**
   ```bash
   git clone https://github.com/YOUR_USERNAME/vhdl-forge-3v0.git
   cd vhdl-forge-3v0
   ```

3. **Install dependencies:**
   ```bash
   uv sync
   ```

4. **Verify tests pass:**
   ```bash
   uv run python cocotb_tests/run.py --all
   ```

5. **Start developing:**
   ```bash
   # Use AI agents for new components
   # See .claude/README.md for workflow
   ```

---

## CI/CD Integration

### GitHub Actions Example

```yaml
name: VHDL Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    container:
      image: ghdl/ghdl:ubuntu22-llvm-5.0

    steps:
      - uses: actions/checkout@v3

      - name: Install uv
        run: curl -LsSf https://astral.sh/uv/install.sh | sh

      - name: Install dependencies
        run: uv sync

      - name: Run P1 tests
        run: uv run python cocotb_tests/run.py --all

      - name: Run P2 tests (comprehensive)
        run: TEST_LEVEL=P2_INTERMEDIATE uv run python cocotb_tests/run.py --all
```

---

## Documentation Hierarchy

**Tier 0 (System Setup):** `SPEC.md` (this file)
→ System dependencies, container setup, fork workflow

**Tier 1 (Quick Reference):** `llms.txt`
→ Component catalog, basic usage

**Tier 2 (Authoritative):** `CLAUDE.md`
→ Testing standards, design patterns, AI workflows

**Tier 3 (Specialized):** `docs/`
→ Deep dives (VHDL standards, CocoTB troubleshooting, etc.)

---

## Quick Reference

| Requirement | Version | Why |
|-------------|---------|-----|
| **GHDL** | 5.0.1+ | VHDL-2008 simulator, CocoTB backend |
| **Python** | 3.10+ | CocoTB testbenches |
| **uv** | Latest | Fast dependency management |
| **GTKWave** | Any | Waveform viewing (optional) |

**Container Image:** `ghdl/ghdl:ubuntu22-llvm-5.0` (recommended)
**Dev Container:** See `.devcontainer/devcontainer.json` example above
**Docker Compose:** See `docker-compose.yml` example above

---

**Maintainer:** Moku Instrument Forge Team
**Repository:** https://github.com/sealablab/vhdl-forge-3v0
**License:** See LICENSE file
