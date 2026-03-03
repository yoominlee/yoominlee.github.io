---
layout: page
title: LC-2K Assembler & Simulator
description: Full assembler and pipeline simulator for the LC-2K ISA — built from scratch in C, including data forwarding, hazard detection, and branch prediction.
importance: 3
category: tech
tags: [C, Computer Architecture, Pipeline, Assembler, Simulator]
giscus_comments: true
---

**Role**: Individual &nbsp;·&nbsp; **Course**: Computer Architecture &nbsp;·&nbsp; **Year**: 2022

---

### Overview

Built a complete toolchain for the **LC-2K** instruction set architecture — a minimal 32-bit ISA used to teach the core concepts of computer architecture.

The project covered the full stack from source to execution:

1. **Assembler** — converts LC-2K assembly (`.as`) into machine code, resolving labels and encoding all 8 instruction types
2. **Behavioral Simulator** — executes machine code instruction-by-instruction, maintaining register file and memory state
3. **Pipeline Simulator** — 5-stage in-order pipeline (IF → ID → EX → MEM → WB) with structural hazard handling
4. **Data Forwarding** — resolves RAW hazards by bypassing results from EX/MEM stages directly to dependent instructions
5. **Branch Prediction** — implements a simple prediction scheme to reduce control hazard stalls

---

### LC-2K ISA

LC-2K is an 8-instruction reduced architecture:

| Instruction | Type | Operation |
|---|---|---|
| `add` | R | regA + regB → destReg |
| `nand` | R | ~(regA & regB) → destReg |
| `lw` | I | mem[regA + offset] → regB |
| `sw` | I | regB → mem[regA + offset] |
| `beq` | I | if regA == regB: PC += offset + 1 |
| `jalr` | J | PC → regB, regA → PC |
| `halt` | O | stop execution |
| `noop` | O | no operation |

Its simplicity makes every design decision visible — there's nowhere to hide when a hazard is mishandled.

---

### Key Challenges

**Hazard detection** requires tracking in-flight instructions across all pipeline stages simultaneously. A single off-by-one in the forwarding logic produces silent wrong answers — hard to debug without careful state logging.

**`jalr` in a pipeline** is tricky: it reads and writes the PC and a register in the same instruction, creating a potential structural hazard that needs explicit handling.

---

**Stack**: C · GCC · Makefile
