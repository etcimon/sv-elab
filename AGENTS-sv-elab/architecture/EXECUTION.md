# Execution path

`src/slang_frontend.cc` is the visitor. It includes slang's
`Compilation`, `SyntaxTree`, and `ASTVisitor`. When Yosys headers are
present it also includes `kernel/rtlil.h` and `kernel/sigtools.h`.

The pass, in order:

1. slang parses and elaborates the SystemVerilog (`third_party/slang`).
2. `builder.cc` and the visitors (`procedural.cc`, `variables.cc`,
   `lvalue.cc`, `statements.h`, `cases.cc`) walk the elaborated AST.
3. `src/backends/yosys/ir.cc` lowers what the walk produced into RTLIL
   cells and wires.
4. `src/backends/yosys/driver.cc` is the Yosys command registration.

OpenROAD's `src/syn` can call this frontend. The STA graph is built later,
from liberty arcs on the gate netlist, not from this RTLIL. Speeding the
frontend does not change `report_checks` on an already-mapped netlist.

Async and memory patterns are separate visitors (`async_pattern.cc`,
`memory.h`). They decide flip-flop and memory cells. Getting them wrong
changes the netlist, not just the runtime.
