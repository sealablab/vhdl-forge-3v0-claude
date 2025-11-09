# Requirements Workflow Summary

**Created:** 2025-11-08
**Purpose:** Documentation of new requirements gathering workflow and example specifications

---

## What Was Created

### 1. Interactive Requirements Gathering Slash Command

**File:** `.claude/commands/gather-requirements.md`

**Usage:**
```
/gather-requirements
```

**What it does:**
- Launches an interactive Q&A session
- Asks structured questions across 7 phases:
  1. Component Identification (name, category, purpose)
  2. Functionality Deep Dive (features, modes, constraints)
  3. Interface Specification (ports, generics, types)
  4. Behavior Specification (reset, enable, states)
  5. Testing Strategy (P1/P2/P3, test cases, values)
  6. Design Guidance (architecture, dependencies)
  7. Specification Generation (creates final document)

**Output:**
- Complete specification document in `workflow/specs/pending/[component].md`
- Ready-to-use "contract" for automated agent workflow
- Validates against VHDL-FORGE standards during Q&A

**Key Features:**
- ✅ One question at a time (not overwhelming)
- ✅ Provides examples and guidance for each question
- ✅ Validates answers (types, widths, naming)
- ✅ Suggests sensible defaults
- ✅ Warns about CocoTB limitations (real/boolean types)
- ✅ Enforces VHDL-FORGE standards:
  - std_logic_vector for FSM states (NOT enums)
  - Active-low reset (rst_n)
  - Standard port order
  - Progressive testing approach
- ✅ Handles special cases (unsure user, complex components, packages)

---

### 2. Four Example Requirement Documents

**Location:** `workflow/specs/pending/`

All examples follow the complete specification template and are ready for the automated agent workflow.

#### Example 1: Edge Detector
**File:** `edge_detector.md`
- **Category:** utilities
- **Complexity:** Low
- **Features:** Rising/falling edge detection with configurable modes
- **Test Level:** P1 (4 tests)
- **Use Cases:** Button press detection, clock domain crossing, trigger events

**Highlights:**
- Generic for edge type selection ("rising", "falling", "both")
- Separate outputs for each edge type
- Clean 1-cycle pulse outputs
- Demonstrates simple utility component pattern

#### Example 2: Synchronizer
**File:** `synchronizer.md`
- **Category:** utilities
- **Complexity:** Low-Medium
- **Features:** Two-stage CDC synchronizer with configurable stages
- **Test Level:** P1 (4 tests)
- **Use Cases:** Clock domain crossing, async input sync, reset synchronization

**Highlights:**
- Configurable NUM_STAGES (2-4)
- Synthesis attributes documented (ASYNC_REG, syn_preserve)
- Metastability discussion (limitations of RTL simulation)
- Industry-standard CDC approach
- Demonstrates critical safety component

#### Example 3: Debouncer
**File:** `debouncer.md`
- **Category:** utilities
- **Complexity:** Medium
- **Features:** Button debouncer with configurable time, multiple output modes
- **Test Level:** P1 (4 tests)
- **Use Cases:** UI buttons, mechanical switches, relay contacts

**Highlights:**
- Generics for CLK_FREQ_HZ and DEBOUNCE_TIME_MS (human-friendly)
- Output modes: level, rising_pulse, falling_pulse
- Counter-based stable detection algorithm
- Test strategy with accelerated timing (1MHz, 1ms for fast simulation)
- Demonstrates time-based component pattern

#### Example 4: Pulse Stretcher
**File:** `pulse_stretcher.md`
- **Category:** utilities
- **Complexity:** Medium
- **Features:** Pulse width extender with retriggerable operation
- **Test Level:** P1 (5 tests)
- **Use Cases:** CDC slow→fast crossing, LED visual feedback, trigger holdoff

**Highlights:**
- Dual mode: cycle-based or time-based (USE_TIME_MODE boolean)
- Retriggerable operation (new pulse extends output)
- Clean algorithm explanation (down-counter with edge detection)
- Real-world applications (LED blinkers, CDC)
- Demonstrates flexible configuration pattern

---

## How to Use This System

### Workflow: From Idea to Implementation

```
┌─────────────────────────────────────────────────────────────┐
│  Step 1: Requirements Gathering                             │
│  Command: /gather-requirements                              │
│  Output: workflow/specs/pending/[component].md              │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│  Step 2: Review Specification                               │
│  Check: All sections complete? Standards followed?          │
│  Edit: Refine if needed                                     │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│  Step 3: Run Automated Workflow                             │
│  Prompt: "Read workflow/specs/pending/[component].md and    │
│           execute the complete 4-agent workflow"            │
│  Agents: 1→VHDL, 2→Test Design, 3→Test Implementation       │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│  Step 4: Review Artifacts                                   │
│  Files: workflow/artifacts/vhdl/*.vhd                       │
│         workflow/artifacts/tests/*_tests/                   │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│  Step 5: Move to Codebase                                   │
│  Move: artifacts → vhdl/ and cocotb_tests/                  │
│  Commit: Git commit with complete implementation            │
└─────────────────────────────────────────────────────────────┘
```

### Quick Start Example

**Scenario:** You need an edge detector component

**Option 1: Interactive (Recommended for First Time)**
```
1. Type: /gather-requirements
2. Answer questions about your edge detector
3. Review generated spec: workflow/specs/pending/edge_detector.md
4. Run: "Read workflow/specs/pending/edge_detector.md and execute the complete 4-agent workflow"
5. Review: workflow/artifacts/vhdl/forge_util_edge_detector.vhd
6. Test: uv run python cocotb_tests/run.py forge_util_edge_detector (from artifacts)
7. Move to main codebase when satisfied
```

**Option 2: Use Existing Spec (Fast)**
```
1. Review: workflow/specs/pending/edge_detector.md (already created!)
2. Customize if needed
3. Run: "Read workflow/specs/pending/edge_detector.md and execute the complete 4-agent workflow"
4. Review and integrate
```

---

## Key Design Decisions

### Why Slash Command for Requirements Gathering?

**Benefits:**
1. **Structured approach:** Ensures no requirements are missed
2. **Standards enforcement:** Validates against VHDL-FORGE rules during Q&A
3. **Educational:** Users learn VHDL-FORGE patterns through guided questions
4. **Reduces agent rework:** Complete specs = fewer iterations
5. **Reusable output:** Specs become documentation

**Alternative considered:** Agent 0 (forge-new-component)
- Agent 0 is still useful for placeholder generation
- Slash command is more interactive and educational
- Both can coexist (slash command → spec → agent 0 → placeholders)

### Why Four Example Components?

**Chosen to demonstrate different patterns:**

1. **edge_detector** - Simple utility (low complexity baseline)
2. **synchronizer** - Critical safety component (synthesis constraints, CDC)
3. **debouncer** - Time-based component (generics for human-friendly units)
4. **pulse_stretcher** - Flexible configuration (dual modes, retriggerable)

**Coverage:**
- ✅ Simple to medium complexity
- ✅ Different architectural patterns (edge detection, counters, shift registers)
- ✅ Different generic strategies (modes, timing, stages)
- ✅ Different use cases (UI, CDC, debug)
- ✅ All P1 level (fast iteration examples)

### Why workflow/specs/pending/?

**Separation of concerns:**
- `workflow/` - Staging area for AI-assisted development
- `workflow/specs/pending/` - Ready-to-implement specifications
- `workflow/artifacts/` - Generated code (gitignored, temporary)
- Main codebase - Reviewed, tested, production code

**Benefits:**
- Clear development lifecycle
- Safe experimentation (artifacts are gitignored)
- Review before integration
- Archive completed specs for reference

---

## Documentation Updates Made

1. **Created:**
   - `.claude/commands/gather-requirements.md` (slash command)
   - `workflow/specs/pending/edge_detector.md`
   - `workflow/specs/pending/synchronizer.md`
   - `workflow/specs/pending/debouncer.md`
   - `workflow/specs/pending/pulse_stretcher.md`
   - `workflow/specs/pending/README.md` (usage guide)
   - `REQUIREMENTS_WORKFLOW_SUMMARY.md` (this file)

2. **Existing files used as reference:**
   - `workflow/specs/README.md` (spec template guide)
   - `workflow/specs/examples/pwm_generator.md` (reference example)
   - `.claude/agents/forge-new-component/agent.md` (placeholder pattern)
   - `CLAUDE.md` (VHDL-FORGE standards)

---

## Next Steps for Users

### Immediate Use
1. **Try the slash command:**
   ```
   /gather-requirements
   ```
   Design a new component interactively

2. **Use existing specs:**
   ```
   Read workflow/specs/pending/edge_detector.md and execute the complete 4-agent workflow
   ```

3. **Study the examples:**
   - Read through the 4 spec files
   - Note the level of detail required
   - Use as templates for your own specs

### Future Enhancements

**Potential additions:**
1. **More examples:**
   - UART controller (complex, FSM-heavy)
   - FIFO (memory component)
   - SPI master (protocol component)
   - Package example (functions, not entity)

2. **Validation tool:**
   - Script to check spec completeness
   - Lint specs before agent workflow

3. **Spec library:**
   - Catalog of common component specs
   - Community-contributed specs

4. **Integration with Agent 0:**
   - Slash command creates spec
   - Agent 0 reads spec and creates placeholders
   - Seamless handoff

---

## Summary

**What you now have:**

✅ **Interactive requirements gathering** via `/gather-requirements` slash command
✅ **Four production-ready example specifications** demonstrating different patterns
✅ **Complete workflow** from idea → spec → implementation → testing
✅ **Standards enforcement** built into the Q&A process
✅ **Reusable templates** for future components

**How to leverage it:**

1. Use `/gather-requirements` for new components (interactive)
2. Use example specs as templates (copy and modify)
3. Feed specs to 4-agent workflow (automated implementation)
4. Review, test, and integrate (human validation)

**Key insight:**

The requirements gathering phase is where 80% of implementation quality is determined. The slash command ensures this phase is thorough, standardized, and produces specifications that agents can execute autonomously.

---

**Created by:** Claude Code
**Date:** 2025-11-08
**Status:** ✅ Ready for use
