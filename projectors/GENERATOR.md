# The Universal Projector Generator (UPG)

The UPG is the engine that makes "every single language" possible. Instead of manual coding, the UPG treats language bindings as a **Code Generation Problem**.

## 1. The Template System
The UPG uses **Language-Specific Templates**. A template defines how an IDL function is projected into a specific language.

### Example: Rust Template
`fn {{name}}({{params}}) -> {{return_type}} { ... }`

### Example: Python Template
`def {{name}}(self, {{params}}): ...`

## 2. The Generation Loop
1. **Parse**: The UPG parses the `.svyaz` IDL file into an Abstract Syntax Tree (AST).
2. **Map**: It maps IDL types to the target language's native types using a **Type-Map Configuration**.
3. **Emit**: It iterates through the AST and fills the templates, producing a complete, type-safe library in the target language.

## 3. Language Support Matrix
Svyaz achieves universality by supporting three categories of languages:
- **Tier 1 (Native)**: Direct mapping to C-ABI (C, C++, Rust, Zig).
- **Tier 2 (Managed)**: Mapping via FFI/JNI (Java, C#, Go, Swift).
- **Tier 3 (Dynamic)**: Mapping via a bridge (Python, JS, Ruby, Lua).
