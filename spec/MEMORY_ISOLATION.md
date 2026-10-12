# Svyaz: Memory Isolation and Hardening

To ensure that a faulty Projector cannot crash the Core, and a compromised Core cannot escape into the Projector's host process, Svyaz implements a **Strict Isolation Boundary**.

## 1. WASM-Sandboxed Core
The Svyaz Core is compiled to **WebAssembly (WASM)**. This provides:
- **Fault Isolation**: The Core runs in a linear memory sandbox. Any out-of-bounds access within the Core triggers a trap that the Projector can catch without crashing.
- **Platform Agnostic**: The same binary runs on any OS/CPU via a WASM runtime (Wasmtime, Wasmer).

## 2. Zero-Copy Safety (The Svyaz-Guard)
To maintain zero-copy performance while ensuring safety, Svyaz uses **Svyaz-Guards**:
- **Ownership Tracking**: The Core tracks which Projector "owns" a specific memory region.
- **Immutable Projections**: Data passed from Core to Projector is mapped as Read-Only unless an explicit `Mutable-Handle` is requested.
- **Boundary Validation**: Every `Svyaz_Call` is validated against a boundary-check table to prevent buffer overflows in the shared linear memory.

## 3. Concurrency Model
Svyaz utilizes a **Lock-Free Command Queue**. Projectors submit requests to the Core asynchronously. The Core processes these requests using a worker pool, ensuring that high-latency operations in one language do not block others.
