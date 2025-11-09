# Failure Analysis: forge_lut_pkg

**Status:** ❌ FAILED
**Category:** VHDL_FUNCTION_ERROR
**Date:** Sun Nov  9 03:40:40 UTC 2025

## Error Summary

/home/user/vhdl-forge-3v0-claude/cocotb_tests/cocotb_test_wrappers/forge_lut_pkg_tb_wrapper.vhd:130:25:error: no declaration for "digital_to_voltage"
/home/user/vhdl-forge-3v0-claude/cocotb_tests/cocotb_test_wrappers/forge_lut_pkg_tb_wrapper.vhd:129:41:error: cannot match function "voltage_to_pct_index" with actuals
/home/user/vhdl-forge-3v0-claude/cocotb_tests/cocotb_test_wrappers/forge_lut_pkg_tb_wrapper.vhd:130:25:error: can't associate function call, slice or indexed name with constant interface "voltage"
/home/user/vhdl-forge-3v0-claude/vhdl/packages/forge_lut_pkg.vhd:124:9:error: (type of constant interface "voltage" is real)
/home/user/vhdl-forge-3v0-claude/cocotb_tests/cocotb_test_wrappers/forge_lut_pkg_tb_wrapper.vhd:128:65:error: no overloaded function found matching "to_unsigned"
Error: Command '['ghdl', '-m', '--work=top', '--std=08', 'forge_lut_pkg_tb_wrapper']' returned non-zero exit status 1.

## Full Error Context

======================================================================
Running test: forge_lut_pkg
Category: packages
Toplevel: forge_lut_pkg_tb_wrapper
Test module: test_forge_lut_pkg_progressive
======================================================================

📦 Building HDL sources...
/home/user/vhdl-forge-3v0-claude/cocotb_tests/cocotb_test_wrappers/forge_lut_pkg_tb_wrapper.vhd:130:25:error: no declaration for "digital_to_voltage"
                        digital_to_voltage(test_voltage),  -- Convert to real
                        ^
/home/user/vhdl-forge-3v0-claude/cocotb_tests/cocotb_test_wrappers/forge_lut_pkg_tb_wrapper.vhd:129:41:error: cannot match function "voltage_to_pct_index" with actuals
                    voltage_to_pct_index(
                                        ^
/home/user/vhdl-forge-3v0-claude/cocotb_tests/cocotb_test_wrappers/forge_lut_pkg_tb_wrapper.vhd:130:25:error: can't associate function call, slice or indexed name with constant interface "voltage"
                        digital_to_voltage(test_voltage),  -- Convert to real
                        ^
/home/user/vhdl-forge-3v0-claude/vhdl/packages/forge_lut_pkg.vhd:124:9:error: (type of constant interface "voltage" is real)
/home/user/vhdl-forge-3v0-claude/cocotb_tests/cocotb_test_wrappers/forge_lut_pkg_tb_wrapper.vhd:128:65:error: no overloaded function found matching "to_unsigned"
                pct_index_output <= std_logic_vector(to_unsigned(
                                                                ^

======================================================================
❌ Test 'forge_lut_pkg' FAILED
Error: Command '['ghdl', '-m', '--work=top', '--std=08', 'forge_lut_pkg_tb_wrapper']' returned non-zero exit status 1.
======================================================================

## Diagnosis

[See terminal output above]

## Recommended Fix

[See terminal output above]

## Full Log

See: test_logs_v3/failed/forge_lut_pkg.log
