# VHDL-FORGE Slash Commands

Quick reference for custom slash commands in VHDL-FORGE.

---

## Available Commands

### /gather-requirements

**Purpose:** Interactive requirements gathering for VHDL component development

**What it does:**
- Launches structured Q&A session (7 phases, ~15-20 questions)
- Validates answers against VHDL-FORGE standards
- Generates complete specification document
- Outputs to: `workflow/specs/pending/[component_name].md`

**When to use:**
- ✅ Starting a new VHDL component
- ✅ Requirements are unclear or incomplete
- ✅ Want guided, structured requirements capture
- ✅ Learning VHDL-FORGE standards and patterns

**When NOT to use:**
- ❌ Requirements already crystal clear (write spec manually)
- ❌ Enhancing existing component (read existing VHDL first)

**Session structure:**
1. **Component Identification** - Name, category, purpose
2. **Functionality Deep Dive** - Features, modes, constraints
3. **Interface Specification** - Ports, generics, types
4. **Behavior Specification** - Reset, enable, states
5. **Testing Strategy** - P1/P2/P3, test cases, values
6. **Design Guidance** - Architecture, dependencies
7. **Specification Generation** - Creates final document

**Output format:**
```
workflow/specs/pending/[component_name].md
```
- Complete specification following VHDL-FORGE template
- Ready for 4-agent automated workflow
- Includes: requirements, interface, tests, design notes

**Example usage:**
```
/gather-requirements

[Interactive Q&A session begins]
You: "Let's design your VHDL component together. What should we call this component?"
User: "A clock divider"
...
[15-20 questions later]
✅ Specification created: workflow/specs/pending/forge_util_clk_divider.md
```

**Next steps after completion:**
```
Option 1 (Recommended): Run full automated workflow
"Read workflow/specs/pending/[component].md and execute the complete 4-agent workflow"

Option 2: Manual implementation
Use spec as guide and implement by hand

Option 3: Refine spec first
Edit generated spec, then run workflow
```

---

## Future Commands (Planned)

### /validate-spec (Coming Soon)

Check specification completeness and standards compliance.

### /review-artifacts (Coming Soon)

Review generated VHDL and tests before integration.

### /integrate-component (Coming Soon)

Automated move from artifacts/ to main codebase with git commit.

---

## How Slash Commands Work

Slash commands in Claude Code:
1. User types `/command-name` in chat
2. Claude loads `.claude/commands/command-name.md`
3. The markdown file contains a prompt that Claude executes
4. User sees the result of executing that prompt

**Creating new commands:**
1. Create `.claude/commands/your-command.md`
2. Write prompt in markdown format
3. Include YAML frontmatter with description:
   ```yaml
   ---
   description: Short description of what this command does
   ---
   ```
4. Command available as `/your-command`

---

## See Also

- `.claude/agents/` - Specialized agents for VHDL development
- `workflow/` - Workflow guides and examples
- `CLAUDE.md` - VHDL-FORGE standards and testing guide
