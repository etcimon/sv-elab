# Data and cost

slang's elaborated AST is the input. Symbols are slang's. Do not build a
second symbol table beside `Compilation`.

On the Yosys side the currency is `RTLIL::SigSpec` and `SigMap`. The rules
already measured in the Yosys fork:

- A `SigSpec` of one wire chunk is O(1) to alias. A bit-by-bit unpack is
  O(width).
- `SigMap::apply` returns immediately when nothing was touched.
- Abutting chunks can be coalesced. A const chunk and a wire chunk are not
  the same case.
- `$and` is not an expensive loop edge. Connections are not drivers.

`kernel/bitpattern.h` is included from the frontend. A bit pattern over a
wide wire is a set of chunks, not a vector of bits, when the Yosys kernel
is the one from the `g6lc` Yosys fork. This frontend does not reimplement
that kernel.

`fmt` is used for diagnostics. Formatting a message is fine on an error
path. Formatting inside the per-statement walk is not.
