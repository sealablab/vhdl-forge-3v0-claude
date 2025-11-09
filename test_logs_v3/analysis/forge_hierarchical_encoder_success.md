# Success Analysis: forge_hierarchical_encoder

**Status:** ✅ PASSED
**Date:** Sun Nov  9 03:39:56 UTC 2025

## What This Test Validates

Running test: forge_hierarchical_encoder
Category: debugging
Toplevel: forge_hierarchical_encoder
Test module: forge_hierarchical_encoder_tests.P1_forge_hierarchical_encoder_basic
======================================================================

📦 Building HDL sources...
analyze /home/user/vhdl-forge-3v0-claude/vhdl/components/debugging/forge_hierarchical_encoder.vhd
elaborate forge_hierarchical_encoder

🧪 Running CocotB tests...
loading VPI module '/home/user/vhdl-forge-3v0-claude/.venv/lib/python3.11/site-packages/cocotb/libs/libcocotbvpi_ghdl.so'
     -.--ns INFO     gpi                                ..mbed/gpi_embed.cpp:93   in _embed_init_python              Using Python 3.11.9 interpreter at /home/user/vhdl-forge-3v0-claude/.venv/bin/python3
     -.--ns INFO     gpi                                ../gpi/GpiCommon.cpp:79   in gpi_print_registered_impl       VPI registered
VPI module loaded!
     0.00ns INFO     cocotb                             Running on GHDL version 4.1.0 (Ubuntu 4.1.0+dfsg-0ubuntu2.1) [Dunoon edition]
     0.00ns WARNING  gpi                                vpi_iterate returned NULL for type vpiInstance for object NULL
     0.00ns INFO     cocotb                             Seeding Python random module with 1762659506
     0.00ns INFO     cocotb                             Initialized cocotb v2.0.0 from /home/user/vhdl-forge-3v0-claude/.venv/lib/python3.11/site-packages/cocotb
Traceback (most recent call last):

## Assertions Passed

✅ Test 'forge_hierarchical_encoder' PASSED

## VHDL Components Tested

analyze /home/user/vhdl-forge-3v0-claude/vhdl/components/debugging/forge_hierarchical_encoder.vhd

## Warnings (if any)

     0.00ns WARNING  gpi                                vpi_iterate returned NULL for type vpiInstance for object NULL

## Full Log

See: test_logs_v3/passed/forge_hierarchical_encoder.log
