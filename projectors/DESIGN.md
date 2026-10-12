# Projector Design: From Binary to Native

A Projector is a language-specific shim that translates the Svyaz-ABI into native code.

## 1. The Projection Loop
1. **Load**: The Projector loads the `svyaz_core.so` / `.dll`.
2. **Map**: It maps the Shared Linear Memory into the language's address space.
3. **Wrap**: It provides a native API that hides the `Svyaz_Call` complexity.

## 2. Example: Python Projector
```python
# conceptual la-Svyaz python shim
class SvyazModule:
    def __init__(self, module_id):
        self.handle = svyaz_core.load_module(module_id)

    def compute_sum(self, a, b):
        # Projects Python ints to Svyaz_Params and calls the Core
        return svyaz_core.execute(self.handle, OP_SUM, [a, b])
```

## 3. Automatic Generation
Svyaz includes a **Projector Generator** that reads a JSON definition of the Core's API and automatically outputs the shim code for all supported languages.
