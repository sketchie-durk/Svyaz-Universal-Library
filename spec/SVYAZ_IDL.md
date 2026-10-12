# Svyaz-IDL: Interface Description Language

To support every language, Svyaz uses a language-agnostic **Interface Description Language (IDL)**. The IDL is the single source of truth from which all Projectors are generated.

## 1. Type System
Svyaz-IDL defines a set of universal types that map to the Svyaz-ABI:
- `u8`, `i32`, `i64`, `f32`, `f64` -> Standard numeric types.
- `string` -> UTF-8 encoded bytes.
- `blob` -> Raw binary data.
- `handle<T>` -> An opaque reference to a Core-managed object of type T.
- `tensor<T>` -> Multi-dimensional array of type T.

## 2. Module Definition
A module is a collection of functions grouped by a common intent.

```svyaz
module Crypto {
    // returns a handle to a cipher state
    function create_aes_context(key: blob) -> handle<AesContext>;
    
    // performs encryption on a blob
    function encrypt(ctx: handle<AesContext>, data: blob) -> blob;
}
```

## 3. The Compilation Pipeline
`IDL File` -> `Svyaz-Compiler` -> `(Svyaz-ABI Header + Projector Source Code)`
