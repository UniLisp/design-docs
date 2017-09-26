# LispAsm overview

## Bytecode & VM (may be changed later)
* Register machine
* 256 general registers
* 32-bit for now
* Instructions are 4 bytes wide, 8 bits for the op, and 8 for each operand. For some ops, you'll have one big operand, or one medium and one small.


## Assembly
The 8 bit operands are X, Y, and Z. A `$` indicates a register, otherwise it is a immediate value.
Any combination such as YZ or XYZ indicates a larger immedieate value taking up 16 or 24 bits.

* Op table:

| Op    | Operands    | Description |
|-------|-------------|-------------|
| LOAD  | $X, YZ      | Loads signed value YZ into $X, performing sign extension |
| LOADU | $X, YZ      | Loads unsigned value YZ into $X |
| ADD   | $X, $Y, Z   | Adds $Y to Z and stores it in $X (signed) |
| ADD   | $X, $Y, $Z  | Adds $Y to $Z and stores it in $X (signed) |
| ADDU  | $X, $Y, Z   | Adds Y to Z and stores it in $X (unsigned) |
| ADDU  | $X, $Y, $Z  | Adds $Y to $Z and stores it in $X (unsigned) |
| SUB   | $X, $Y, Z   | Subtracts Z from $Y and stores it in $X (signed) |
| SUB   | $X, $Y, $Z  | Subtracts $Z from $Y and stores it in $X (signed) |
| SUBU  | $X, $Y, Z   | Subtracts Z from $Y and stores it in $X (unsigned) |
| SUBU  | $X, $Y, $Z  | Subtracts $Z from $Y and stores it in $X (unsigned) |
| LDB   | $X, $Y, $Y  | Sets $X to the byte pointed to by $Y + $Z, performing sign extension |
| LDBU  | $X, $Y, $Z  | Sets $X to the byte ponited to by $Y + $Z |
| LDW   | $X, $Y, $Y  | Sets $X to the wyde pointed to by $Y + $Z, performing sign extension |
| LDWU  | $X, $Y, $Z  | Sets $X to the wyde ponited to by $Y + $Z |
| LDT   | $X, $Y, $Y  | Sets $X to the tetra pointed to by $Y + $Z, performing sign extension |
| LDTU  | $X, $Y, $Z  | Sets $X to the tetra pointed to by $Y + $Z |
| LDA   | $X, *Label* | Same as the first LDTU, except the assembler finds an appropriate static register and value for the address of *Label* (Error if no valid combination can be found) |
| JMP   | *Label*     | Jumps to 26-bit relative address *Label* (separate ops for fowards and backwards) |
| CMP   | $X, $Y, $Z  | $Y < $Z -> -1, $Y = $Z -> 0, $Y > $Z -> 1 |
| CMPU  | $X, $Y, $Y  | Same but unsigned |
| BZ    | $X, *Label* | Jumps to 18-bit relative address *Label* if $X is 0 |
| BNZ   | $X, *Label* | Jumps to 18-bit relative address *Label* if $X is not 0 |
| BP    | $X, *Label* | Jumps to 18-bit relative address *Label* if $X is positive |
| BNP   | $X, *Label* | Jumps to 18-bit relative address *Label* if $X is not positive |
| BN    | $X, *Label* | Jumps to 18-bit relative address *Label* if $X is is negative |
| BNN   | $X, *Label* | Jumps to 18-bit relative address *Label* if $X is not negative |
| LSH   | $X, $Y, Z   | Shift $Y left by Z, filling with 0 and storing it in $X |
| LSH   | $X, $Y, $Z  | Shift $Y left by $Z, filling with 0 and storing it in $X |
| LASH  | $X, $Y, Z   | Shift $Y left by Z, filling with 0 and storing it in $X |
| LASH  | $X, $Y, $Z  | Shift $Y left by $Z, filling with 0 and storing it in $X |
| RSH   | $X, $Y, Z   | Shift $Y left by Z, filling with 0 and storing it in $X |
| RSH   | $X, $Y, $Z  | Shift $Y left by $Z, filling with 0 and storing it in $X |
| RASH  | $X, $Y, Z   | Shift $Y left by Z, filling with the leftmost bit and storing it in $X |
| RASH  | $X, $Y, $Z  | Shift $Y left by $Z, filling with the leftmost bit and storing it in $X |
