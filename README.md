# GlitchCore
migrating and porting to SV fro VHDL.

small microcontroller for low lever hardware control and custom accelerators



# GlitchCore Instruction Set Documentation

Each instruction is 16 bits wide, with the following structure:
- **Bits [15:12]** – Opcode
- **Bits [11:8]** – Extended Opcode (if applicable)
- **Bits [11:0]** – Operand(s)

## Supported Operations

| Opcode     | Mnemonic       | Description                          | Operands                        | Bits used (word width)       |
|------------|----------------|--------------------------------------|---------------------------------|------------------------------|
| 0000       | ADD            | Add two registers                   | addr1, addr2, dest_addr         | 4(4), 4(4), 4(4)            |
| 0001       | SUB            | Subtract one register from another  | addr1, addr2, dest_addr         | 4(4), 4(4), 4(4)            |
| 0010       | MUL            | Multiply two registers              | addr1, addr2, dest_addr         | 4(4), 4(4), 4(4)            |
| 0011       | AND            | Bitwise AND                         | addr1, addr2, dest_addr         | 4(4), 4(4), 4(4)            |
| 0100       | OR             | Bitwise OR                          | addr1, addr2, dest_addr         | 4(4), 4(4), 4(4)            |
| 0101       | XOR            | Bitwise XOR                         | addr1, addr2, dest_addr         | 4(4), 4(4), 4(4)            |
| 0110       | LSHIFT         | Shift left                          | addr1, count, dest_addr         | 4(4), 4(4), 4(4)            |
| 0111       | RSHIFT         | Shift right                         | addr1, count, dest_addr         | 4(4), 4(4), 4(4)            |
| 1000       | COMPARE        | Compare two registers               | addr1, addr2, operator          | 4(4), 4(4), 2(4)            |
| 1001       | TGR_IO         | Branch on input bit                 | polarity, io_addr, pc           | 1(1), 3(3), 8(8)            |
| 1010       | TGR_EDGE       | Branch on input bit edge            | edge_pol, io_addr, pc           | 1(1), 3(3), 8(8)            |
| 1011       | IMM            | Load immediate value to result reg  | sint_12                         | 12(12)                      |
| 1100       | LOAD           | Load from memory                    | mem_addr, dest_addr             | 8(8), 4(4)                  |
| 1101       | STORE          | Store to memory                     | addr1, mem_addr                 | 4(4), 8(8)                  |
| 1110       | CUST_CALC      | Custom operation                    | addr1, addr2, dest_addr         | 4(4), 4(4), 4(4)            |
| 1111       | EXTENDED       | Extended operations                 | extend_op, addr1, dest_addr     |                              |
| 1111 0000  | MOVE           | Move data between registers         | addr1, dest_addr                | 4(4), 4(4)                  |
| 1111 0001  | PUBLISH        | Publish data to the fault data bus  | addr1, dest_addr                | 4(4), 4(4)                  |
| 1111 0010  | NOP            | No operation                        | (none)                          |                              |
| 1111 0011  | CLR            | Clear a register                    | dest_addr                       | 0(4), 4(4)                  |
| 1111 0100  | RET            | Return from subroutine              | (none)                          |                              |
| 1111 0101  | JMP            | Jump to a new address               | pc                              | 8(8)                        |
| 1111 0110  | BRANCH_TRUE    | Branch if result reg is non-zero    | pc                              | 8(8)                        |
| 1111 0111  | BRANCH_FALSE   | Branch if result reg is zero        | pc                              | 8(8)                        |
| 1111 1aaa  | CUST_UTIL      | Custom utilities                    | custom, addr2, dest_addr        | aaa, 4(4), 4(4)             |
