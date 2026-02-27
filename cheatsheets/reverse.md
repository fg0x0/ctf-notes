# ⚙️ Reverse Engineering Cheatsheet

## Static Analysis
```bash
# Binary info
file binary
checksec --file=binary
readelf -h binary          # ELF header
objdump -d binary          # Disassembly
strings binary | grep -i "flag\|key\|pass"

# Ghidra headless
analyzeHeadless /tmp/proj myproject \
  -import binary -postScript PrintAST.java
```

## Dynamic Analysis (GDB)
```bash
gdb -q ./binary
b main                     # Breakpoint
b *0x401234                # Breakpoint at address
r arg1 arg2                # Run with args
ni / si                    # Next/step instruction
x/20x $rsp                 # Examine memory
info registers             # Register values
finish                     # Run until return
```

## Anti-Debug Bypass
```
ptrace check:    patch JNZ → JZ (or NOP)
IsDebuggerPresent: patch return value → 0
Timing checks:  NOP the check or patch threshold
CPUID tricks:   patch hypervisor bit check
```

## Python Reversing
```python
import dis
import marshal
import py_compile

# .pyc decompile
python -m uncompyle6 file.pyc   # pip install uncompyle6

# Bytecode
import dis; dis.dis(func)
```

## Common Patterns
```
strcmp → compare flag directly
strncmp(input, flag, len) → patch len to 0
Custom encoding: XOR, ROT, base custom
VM/interpreter: trace opcode execution
Anti-tamper: checksum of own code → patch out
```
