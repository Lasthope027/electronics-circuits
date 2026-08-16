# Pipelined Multiplier

<img width="1312" height="539" alt="image" src="https://github.com/user-attachments/assets/0e5a5f36-6523-413e-a1c7-e5a22b22d6cf" />

## Overview

This project presents the design and implementation of a **processor-style pipelined multiplier** in Logisim. Rather than treating multiplication as an isolated arithmetic block, the design integrates the multiplier into a structured CPU-style datapath to demonstrate instruction flow, operand handling, pipeline timing, and result write-back.

The datapath follows the classical five-stage pipeline:

**Fetch → Decode → Execute → Memory → Write-Back**

The multiplication operation is performed during the Execute stage using a combinational multiplier, while pipeline registers control the transfer of data between successive stages.

## Architecture

The design models the execution of a multiplication instruction through the following stages:

### 1. Instruction Fetch (IF)

The Program Counter (PC) addresses the instruction memory and retrieves the multiplication instruction. The instruction is then stored in the Instruction Register for further processing.

### 2. Instruction Decode (ID)

The instruction fields are decoded to identify the source and destination registers. The corresponding operands are read from the register file and prepared for execution.

### 3. Execute (EX)

The decoded operands are supplied to a **combinational multiplier**, which generates the product.

The computed result is stored in the **EX Result Register**, allowing it to be transferred to the next pipeline stage on the appropriate clock edge.

### 4. Memory (MEM)

Since multiplication does not require a memory access, the Memory stage acts primarily as a **pipeline buffer**. The computed result is forwarded to the next stage without modification.

### 5. Write-Back (WB)

The multiplication result reaches the Write-Back stage and is written into the destination register specified by the instruction.

## Datapath Flow

```text
        ┌─────────┐
        │  FETCH  │
        │ PC + IM │
        └────┬────┘
             │
             ▼
        ┌─────────┐
        │ DECODE  │
        │ RegFile │
        └────┬────┘
             │
             ▼
        ┌─────────┐
        │ EXECUTE │
        │   ×     │
        └────┬────┘
             │
             ▼
        ┌─────────┐
        │  MEMORY │
        │ Buffer  │
        └────┬────┘
             │
             ▼
        ┌──────────┐
        │WRITE-BACK│
        │ RegFile  │
        └──────────┘
```

## Pipeline Registers

Clock-controlled registers are used between the pipeline stages to maintain stage-wise data flow.

These registers allow the datapath to operate synchronously and demonstrate how information moves through a processor pipeline on successive clock cycles.

## Key Components

The Logisim implementation uses digital building blocks including:

* Program Counter
* Instruction Memory
* Instruction Register
* Register File
* Multiplexer
* Combinational Multiplier
* Pipeline Registers
* Clock
* Control and data-routing logic

## Objectives

The project demonstrates:

* Integration of an arithmetic operation into a CPU-style datapath
* Five-stage instruction execution
* Operand fetching and register-file interaction
* Clock-controlled pipeline data transfer
* Combinational multiplication
* Result forwarding and register write-back
* The relationship between datapath structure and instruction timing

## Tools and Technologies

* **Logisim** — digital circuit design and simulation
* **Digital Logic Design** — registers, multiplexers, memory, datapaths, and arithmetic units
* **Sequential Logic** — clocked pipeline registers and synchronous data transfer


## Conclusion

The project demonstrates how a multiplication instruction can be incorporated into a processor-style pipelined datapath rather than implemented as an isolated multiplier. By separating instruction execution into Fetch, Decode, Execute, Memory, and Write-Back stages, the design provides a practical representation of instruction flow and synchronous datapath operation.

The implementation serves as a compact study of **processor datapaths, pipelining, arithmetic execution, and clock-controlled digital systems**.
