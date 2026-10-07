# tree-sitter-peeper

Tree-sitter grammar for the current Peeper language revision.

## Current coverage

- imports
- top-level `let` / `const`
- `struct`, `interface`, and payload-aware `enum` declarations
- `impl T { ... }`
- plain function declarations
- generic type/function syntax with `<T>`
- `let` / `let mut`
- `if` / `else`
- fully named `Enum::Variant with expression` construction and `is` case tests
- statement `match` with whole-payload bindings or struct field patterns
- `*T` owned pointer types, `rawptr`, and `?T` optionals
- array literals and indexing
- postfix `++` / `--`
- named struct literals: `Point.{ x = 1, y = 2 }`, `Box<i32>.{ value = 1 }`, `geometry::Point.{ x = 1 }`
- inferred struct literals: `.{ x = 1, y = 2 }`
- field access and method calls
- `comptime` parameters and prefix expressions
- structural `struct` / `interface` / `enum` type expressions
- `!!`, `??`, `catch`

## Struct literals

Named struct literals use `Type.{ field = value }`; inferred literals use `.{ field = value }`. Fields use `=` initializers. Named types may be generic or `::`-qualified, including `pkg::Box<i32>.{ value = 1 }`.

The dot distinguishes literals from control-flow blocks, so `if Point.{ x = 1 }.ready() {}` and `for item in Box<i32>.{ value = 1 }.items() {}` parse without parentheses. Enum payload construction uses `Result<Point>::Ok with Point.{ x = 1 }` or `Result<Point>::Ok with .{ x = 1 }`.

## File extension

The grammar is configured for `.peep` files.

## Development

```bash
tree-sitter generate
tree-sitter test
```

To validate the grammar against the compiler sample file:

```bash
tree-sitter parse ../PeeperCompiler/x_test/struct_runtime.peep
```
