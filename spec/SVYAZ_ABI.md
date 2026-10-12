# Svyaz-ABI: The Universal Logic Fabric Specification

The Svyaz-ABI is the bridge between the Core and the Projectors. To ensure universal compatibility, it adheres to a strict "No-Implicit-State" model.

## 1. The Memory Model
Svyaz uses a **Shared Linear Memory** model. All data passed between the Core and a Projector is stored in a contiguous block of memory.
- **Handles**: The Core never returns raw pointers. It returns **Svyaz-Handles** (opaque 64-bit identifiers).
- **Tensors**: Large data arrays are passed as Tensors (Shape + Dtype + Offset).

## 2. The Call Convention
Every call to the Svyaz Core follows the **Svyaz-Call Standard**:
`Svyaz_Result execute(Svyaz_Handle instance, Svyaz_OpID opcode, Svyaz_Params* params)`

## 3. Type Projection
Types are projected using a **Canonical Type Map**:
- `Svyaz_Int` -> `i64` (Rust) -> `int` (C++) -> `Number` (JS).
- `Svyaz_String` -> UTF-8 encoded bytes with a length prefix.
- `Svyaz_Object` -> A handle to a kernel-managed object.
