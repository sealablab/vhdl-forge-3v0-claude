# VHDL-FORGE 3.0

**Batteries-included VHDL framework for Moku custom instrument development**

FORGE provides reusable VHDL components, AI-assisted development workflows, and a proven 3-layer architecture for building custom FPGA instruments on Moku platforms (Go/Lab/Pro/Delta).

---

## 🎯 Key Features

### FORGE Calling Convention
Safe initialization handshaking via **CR0[31:29]** - a 3-bit calling convention between MCC CustomInstrument and your application logic.

```
global_enable = forge_ready AND user_enable AND clk_enable AND loader_done
```

All four conditions must be met for safe operation.

### Hierarchical Voltage Scheme (HVS)
**Batteries-included oscilloscope debugging** - Encode 14 bits of FSM state + status onto a single DAC output for visual debugging on any oscilloscope.

- 200mV state steps (human-readable)
- ±50mV status "noise" (machine-decodable)
- Fault detection via voltage sign flip
- Zero LUTs (pure arithmetic)

### 3-Layer Architecture
Clean separation of concerns:
- **Layer 3 (Main):** Application logic (MCC-agnostic, portable)
- **Layer 2 (Shim):** Register mapping + FORGE control + HVS encoder
- **Layer 1 (Loader):** BRAM initialization (future)

### AI-Assisted Development
Four specialized agents for autonomous VHDL development:
1. **forge-new-component** - Requirements elicitation
2. **forge-vhdl-component-generator** - VHDL implementation
3. **cocotb-progressive-test-designer** - Test architecture
4. **cocotb-progressive-test-runner** - Test execution

### Progressive Testing
Token-efficient CocoTB testing with **98% output reduction**:
- P1: 3-5 tests, <20 lines, <100 tokens (LLM-optimized)
- P2: 10-15 tests, comprehensive validation
- P3: 20-30 tests, production readiness

---

## 🚀 Quick Start

### Installation

```bash
git clone https://github.com/sealablab/vhdl-forge-3v0.git
cd vhdl-forge-3v0
uv sync
```

### Your First FORGE Instrument

1. **Explore the counter example:**
   ```bash
   cd examples/counter
   cat README.md
   ```

2. **Run CocoTB tests:**
   ```bash
   uv run python cocotb_tests/run.py platform_counter_poc
   ```

3. **Read the architecture docs:**
   - `docs/FORGE_CALLING_CONVENTION.md` - CR0[31:29] deep dive
   - `docs/HVS_ENCODING.md` - Hierarchical voltage scheme
   - `docs/THREE_LAYER_ARCHITECTURE.md` - FORGE pattern

4. **Adapt to your application:**
   - Replace Layer 3 counter logic with your FSM
   - Export `app_state_vector[5:0]` and `app_status_vector[7:0]`
   - Keep Layer 2 shim pattern (handles FORGE + HVS)
   - You get oscilloscope debugging for free!

---

## 📚 Documentation

**Quick Reference:** `llms.txt` - Component catalog, essential facts

**AI Agent Guide:** `CLAUDE.md` - Complete development patterns

**Documentation Directory:** `docs/` - Detailed guides
- FORGE calling convention (CR0[31:29])
- HVS encoding specification
- 3-layer architecture
- VHDL coding standards
- CocoTB testing guide

**Agent Workflows:** `.claude/` - AI-assisted development
- Four specialized agents
- Autonomous VHDL generation
- Progressive test design

---

## 🧩 Components

### VHDL Packages (`vhdl/packages/`)
- `forge_common_pkg` - FORGE control scheme ⭐
- `forge_serialization_*_pkg` - Register serialization (types, voltage, time)
- `forge_voltage_*_pkg` - Voltage domain utilities (3.3V, 5V, ±5V)
- `forge_lut_pkg` - Look-up table utilities

### VHDL Components (`vhdl/components/`)
- `forge_hierarchical_encoder` - HVS encoder ⭐
- `forge_util_clk_divider` - Programmable clock divider
- `forge_bram_loader` - BRAM initialization (future)

### Python Utilities (`python/`)
- `forge_cocotb` - Progressive testing framework
- `forge_platform` - Simulation/hardware backends
- `forge_tools` - HVS decoder, utilities

---

## 🧪 Testing

### CocoTB VHDL Tests (`cocotb_tests/`)
```bash
# Component unit tests (P1 - LLM-optimized)
uv run python cocotb_tests/run.py forge_util_clk_divider

# Platform integration tests
uv run python cocotb_tests/run.py platform_forge_control

# List all tests
uv run python cocotb_tests/run.py --list
```

### Python Unit Tests (`tests/`)
```bash
# pytest for Python utilities
pytest tests/
```

---

## 🎓 Examples

**`examples/counter/`** - The canonical FORGE example

Complete 3-layer architecture with HVS encoding. Demonstrates:
- FORGE control scheme (CR0[31:29])
- Register packing/unpacking
- HVS oscilloscope debugging
- Progressive CocoTB testing

**Start here** to learn FORGE patterns!

---

## 🤖 AI-Assisted Development

FORGE includes four specialized agents for autonomous VHDL development:

```
forge-new-component → forge-vhdl-component-generator
                   ↓
      cocotb-progressive-test-designer
                   ↓
       cocotb-progressive-test-runner
```

See `.claude/README.md` for agent workflows.

---

## 📖 Design Philosophy

1. **FORGE Control Scheme** - CR0[31:29] is mandatory for safe initialization
2. **Batteries Included** - HVS encoding is standard, not optional
3. **Train Like You Fight** - Same bitstream for development and production
4. **LLM-Friendly** - Token-efficient testing, progressive disclosure docs
5. **Type Safety** - Explicit voltage domains, function-based utilities
6. **Verilog Compatible** - No VHDL enums, records, or physical types

---

## 🔗 Related Projects

- **BPD-Dev** - Basic Probe Driver monorepo (FORGE reference implementation)
- **moku-models** - Moku platform specifications
- **forge-codegen** - YAML → VHDL code generator (dormant)

---

## 📄 License

See `LICENSE` file.

---

## 🙏 Acknowledgments

FORGE is developed for Moku platform custom instrument development.

**Version:** 3.0.0
**Status:** Active development
**Last Updated:** 2025-11-08
