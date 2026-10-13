# Opportunities

This frontend is off the measured STA path. Optimize it only with an
elaboration profile (CVA6 `read_slang` or `src/syn`), not with the
TinyRocket `repair_timing` callgrind.

- Do not walk every bit of a `SigSpec` when `as_chunk()` is one wire.
  That was the Yosys `check` regression, and this file includes `sigtools.h`.
- Do not add a hash of statements on top of slang's symbol table and
  Yosys's `SigMap`. Two maps of the same net is the extra `opt_merge` table.
- Memory and async visitors must stay exact. A faster visitor that drops a
  clock enable changes the gate netlist the timer will see.
- slang's unroll limit is a compile-time knob in the slang library, not
  here. CVA6 `g6lc_iq` needs a large unroll. Lowering it does not leave a
  loop as a cell. It fails elaboration. See the slang notes.
