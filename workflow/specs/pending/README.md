# Pending Component Specifications

This directory contains component specifications ready for the automated agent workflow.

## Current Specifications

### ✅ Ready for Implementation

1. **edge_detector.md** - Edge detection utility
   - Category: utilities
   - Complexity: Low
   - Test Level: P1 (4 tests)
   - Features: Rising/falling edge detection with configurable modes

2. **synchronizer.md** - Two-stage synchronizer
   - Category: utilities
   - Complexity: Low-Medium
   - Test Level: P1 (4 tests)
   - Features: CDC metastability mitigation, configurable stages

3. **debouncer.md** - Button debouncer
   - Category: utilities
   - Complexity: Medium
   - Test Level: P1 (4 tests)
   - Features: Configurable debounce time, multiple output modes

4. **pulse_stretcher.md** - Pulse width extender
   - Category: utilities
   - Complexity: Medium
   - Test Level: P1 (5 tests)
   - Features: Retriggerable stretching, time/cycle modes

## How to Use These Specs

### Option 1: Full Automated Workflow

```bash
# Pick a spec and run the complete 4-agent workflow
# Example for edge_detector:
```

**In Claude Code:**
```
Read workflow/specs/pending/edge_detector.md and execute the complete 4-agent workflow:
1. Generate VHDL component
2. Design test architecture
3. Implement and run CocoTB tests
```

### Option 2: Manual Implementation

1. Read the specification
2. Implement VHDL manually in `vhdl/components/utilities/`
3. Implement tests manually in `cocotb_tests/components/`
4. Mark spec as completed (move to `workflow/specs/completed/`)

### Option 3: Partial Automation

Use individual agents:
- **Agent 1 only:** Generate VHDL, write tests manually
- **Agents 2-3:** Design and run tests for existing VHDL
- **Agent 0 first:** Refine spec before implementation

## Specification Quality

All specs in this directory include:
- ✅ Complete port lists with types and widths
- ✅ Reset and enable behavior documented
- ✅ Test level and required tests specified
- ✅ Design notes and architectural guidance
- ✅ Agent-specific instructions
- ✅ Example behaviors and use cases

## Creating New Specifications

### Method 1: Use Slash Command (Recommended)

```
/gather-requirements
```

This launches an interactive session that:
- Asks structured questions about your component
- Validates answers against VHDL-FORGE standards
- Generates a complete specification document
- Provides next steps for implementation

### Method 2: Manual Authoring

1. Copy `workflow/specs/examples/pwm_generator.md` as template
2. Fill in all sections (see `workflow/specs/README.md`)
3. Validate with checklist in specs README
4. Save in this directory

## Specification Lifecycle

```
pending/          → Implementation → completed/
├── component.md      (agents 1-3)     ├── component.md
```

**States:**
- **pending/** - Ready for implementation
- **completed/** - Implemented and tested (archive for reference)

## Next Steps After Implementation

1. **Review artifacts:**
   ```bash
   ls workflow/artifacts/vhdl/
   ls workflow/artifacts/tests/
   ```

2. **Move to main codebase:**
   ```bash
   mv workflow/artifacts/vhdl/[component].vhd vhdl/components/utilities/
   mv workflow/artifacts/tests/[component]_tests cocotb_tests/components/
   ```

3. **Archive specification:**
   ```bash
   mv workflow/specs/pending/[component].md workflow/specs/completed/
   ```

4. **Commit to git:**
   ```bash
   git add vhdl/components/utilities/[component].vhd
   git add cocotb_tests/components/[component]_tests
   git commit -m "feat: Add [component] with CocoTB tests"
   ```

## See Also

- `workflow/specs/README.md` - Specification writing guide
- `workflow/specs/examples/` - Reference examples
- `.claude/commands/gather-requirements.md` - Interactive spec generator
- `workflow/README.md` - Complete workflow guide
