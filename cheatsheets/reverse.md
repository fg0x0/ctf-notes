# ⚙️ Reverse Engineering Cheatsheet

## Static
```bash
file bin; checksec --file=bin
strings bin | grep -i "flag\|key\|pass"
objdump -d bin
```

## GDB
```bash
b main; b *0x401234
r; ni; si
x/20x $rsp
info registers
```

## Anti-Debug Bypass
```
ptrace check:        patch JNZ → JZ
IsDebuggerPresent:   patch return → 0
Timing checks:       NOP or patch threshold
```

## Python
```bash
python -m uncompyle6 file.pyc
python -c "import dis,marshal; dis.dis(marshal.loads(open('f.pyc','rb').read()[16:]))"
```
