# Success Analysis: forge_voltage_5v0_pkg

**Status:** ✅ PASSED
**Date:** Sun Nov  9 03:39:57 UTC 2025

## What This Test Validates

Running test: forge_voltage_5v0_pkg
Category: packages
Toplevel: forge_voltage_5v0_pkg_tb_wrapper
Test module: test_forge_voltage_5v0_pkg_progressive
======================================================================

📦 Building HDL sources...
analyze /home/user/vhdl-forge-3v0-claude/vhdl/packages/forge_voltage_5v0_pkg.vhd
analyze /home/user/vhdl-forge-3v0-claude/cocotb_tests/cocotb_test_wrappers/forge_voltage_5v0_pkg_tb_wrapper.vhd
elaborate forge_voltage_5v0_pkg_tb_wrapper

🧪 Running CocotB tests...
loading VPI module '/home/user/vhdl-forge-3v0-claude/.venv/lib/python3.11/site-packages/cocotb/libs/libcocotbvpi_ghdl.so'
     -.--ns INFO     gpi                                ..mbed/gpi_embed.cpp:93   in _embed_init_python              Using Python 3.11.9 interpreter at /home/user/vhdl-forge-3v0-claude/.venv/bin/python3
     -.--ns INFO     gpi                                ../gpi/GpiCommon.cpp:79   in gpi_print_registered_impl       VPI registered
VPI module loaded!
     0.00ns INFO     cocotb                             Running on GHDL version 4.1.0 (Ubuntu 4.1.0+dfsg-0ubuntu2.1) [Dunoon edition]
     0.00ns WARNING  gpi                                vpi_iterate returned NULL for type vpiInstance for object NULL
     0.00ns INFO     cocotb                             Seeding Python random module with 1762659504
     0.00ns INFO     cocotb                             Initialized cocotb v2.0.0 from /home/user/vhdl-forge-3v0-claude/.venv/lib/python3.11/site-packages/cocotb

## Assertions Passed

✅ Test 'forge_voltage_5v0_pkg' PASSED

## VHDL Components Tested

analyze /home/user/vhdl-forge-3v0-claude/vhdl/packages/forge_voltage_5v0_pkg.vhd
analyze /home/user/vhdl-forge-3v0-claude/cocotb_tests/cocotb_test_wrappers/forge_voltage_5v0_pkg_tb_wrapper.vhd

## Warnings (if any)

     0.00ns WARNING  gpi                                vpi_iterate returned NULL for type vpiInstance for object NULL

## Full Log

See: test_logs_v3/passed/forge_voltage_5v0_pkg.log
