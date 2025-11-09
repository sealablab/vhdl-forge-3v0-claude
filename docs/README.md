# FORGE Documentation

Comprehensive guides for FORGE architecture, VHDL development, and testing.

## Core Concepts

**FORGE_CALLING_CONVENTION.md** ⭐
- CR0[31:29] control scheme deep dive
- The 4-condition enable pattern
- Deployment handshaking

**HVS_ENCODING.md** ⭐
- Hierarchical Voltage Scheme specification
- 14-bit state + status encoding
- Oscilloscope debugging patterns

**THREE_LAYER_ARCHITECTURE.md**
- FORGE 3-layer pattern (Loader → Shim → Main)
- Layer responsibilities
- Integration patterns

## Getting Started

**GETTING_STARTED.md**
- Tutorial using counter example
- Step-by-step FORGE development
- From VHDL to deployment

## Development Guides

**VHDL_CODING_STANDARDS.md**
- Mandatory VHDL rules for FORGE
- Port order, signal naming, FSM patterns
- Verilog compatibility guidelines

**COCOTB_GUIDE.md**
- Progressive testing (P1/P2/P3)
- CocoTB best practices
- Test structure patterns

**COCOTB_TROUBLESHOOTING.md**
- Common CocoTB issues and solutions
- GHDL debugging tips
- Type constraint workarounds

## Navigation

Start with **GETTING_STARTED.md** for tutorials, or jump to **FORGE_CALLING_CONVENTION.md** and **HVS_ENCODING.md** for core architecture concepts.
