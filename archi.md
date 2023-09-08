# GIGA Architecture

* Subset of 6502 architecture
* Fixed-length (3 byte) opcodes<br>
* 8-bit with 16-bit addressing

## Addressing modes
* Address modes are defined by bytes 4-6 in the opcode.
* Bytes 4-6 are treated as a 3-bit integer and decoded into 8 different addressing modules.<br>

| **Bytes 4-6** |                    **Addressing mode**    |
| ------------: |                    :------------------    |
| `000` (`0`)   |                        [Implied](#implied)|
| `001` (`1`)   |                    [Immediate](#immediate)|
| `010` (`2`)   |                          [Direct](#direct)|
| `011` (`3`)   |     [Direct, x-indexed](#direct-x-indexed)|
| `100` (`4`)   |                      [Indirect](#indirect)|
| `101` (`5`)   | [Indirect, x-indexed](#indirect-x-indexed)|
| `110` (`6`)   |               Illegal, treated as implied |
| `111` (`7`)   |               Illegal, treated as implied |

### Implied
* Implied addressing has no operands, bytes 2-3 of the instruction don't matter to the execution of the instruction.
* Examples are `nop` and `inc`

### Immediate
* Immediate addressing means the operand comes directly from the instruction, bytes 2-3 of the instruction are used as the operand
* Examples are `lda #` and `adc #`

### Direct
* Direct addressing means the operand comes from memory, bytes 2-3 of the instruction are an address to the operand in memory.
* Examples are `sta` and `ldx`

### Direct X indexed
* Direct x-indexed addressing is simlar to direct addressing, but the address to the operand is offset by the X register.
* `add_rX_instruction_addr -> read_operand`
* Examples are `lda addr,x` and `adc addr,x`

### Indirect
* Indirect addressing means the operand comes from memory, indexed by another memory address. Bytes 2-3 of the instruction are an address to the memory that holds the address to the operand.
* Examples are `lda [addr]` and `sta[addr]`

### Indirect X indexed
* Indirect x-indexed addressing is similar to indirect addressing, but the address to the operand is offset by the X register.
* `read_addr -> add_rX -> read_operand`
* Examples are `lda [addr],x` and `sta[addr],x`