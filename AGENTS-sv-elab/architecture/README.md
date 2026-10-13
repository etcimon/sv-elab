# sv-elab architecture notes

This checkout is the Yosys slang frontend (`slang_frontend`), published as
`etcimon/sv-elab`. It is not the timing engine. OpenROAD builds it as
`slang_frontend` for SystemVerilog elaboration. A liberty STA run does not
call it.

| Note | What it answers |
|---|---|
| [EXECUTION.md](EXECUTION.md) | AST walk to RTLIL |
| [DATA.md](DATA.md) | What is a bit pattern and what is a net |
| [OPPORTUNITIES.md](OPPORTUNITIES.md) | Which Yosys rules apply here |

Nested libraries: `third_party/slang` (the compiler) and `third_party/fmt`
(formatting). Each has its own `AGENTS-*/architecture/` notes.
