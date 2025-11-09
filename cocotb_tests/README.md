# CocoTB VHDL Simulation Tests

VHDL component and platform testing using CocoTB + GHDL.

## Directory Structure

**components/** - Component unit tests (VHDL simulation)
- Individual VHDL component testing in isolation
- Progressive test levels (P1/P2/P3)
- Each component has its own subdirectory with constants + test files

**platform/** - Platform integration tests (VHDL simulation)
- Tests with platform backend (simulation or real MCC hardware)
- FORGE control scheme validation
- Oscilloscope capture and routing tests

**cocotb_test_wrappers/** - VHDL test wrappers
- Wrappers for VHDL packages (CocoTB can't test packages directly)
- Expose package functions/constants as signals for testing

## Running Tests

**Default (P1 - LLM-optimized, <20 line output):**
```bash
uv run python cocotb_tests/run.py <component_name>
```

**P2 (comprehensive validation):**
```bash
TEST_LEVEL=P2_INTERMEDIATE uv run python cocotb_tests/run.py <component_name>
```

**List all available tests:**
```bash
uv run python cocotb_tests/run.py --list
```

## Progressive Testing Philosophy

**P1 - BASIC** (Default, 3-5 tests, <20 line output)
- Essential functionality only
- Fast iteration for AI-assisted development

**P2 - INTERMEDIATE** (10-15 tests, <50 line output)
- Edge cases and standard validation

**P3 - COMPREHENSIVE** (20-30 tests, full coverage)
- Boundary values, stress testing
- Production readiness

See `docs/COCOTB_GUIDE.md` for detailed testing patterns.
