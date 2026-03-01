# 🔍 Forensics Cheatsheet

## File Analysis
```bash
file f; strings -a f | grep -i "flag\|key\|pass"
xxd f | head -20
binwalk -e f
exiftool f
```

## Stego
```bash
steghide extract -sf img.jpg -p ""
zsteg img.png
stegsolve          # bit plane GUI
sonic-visualizer   # audio spectrogram
```

## PCAP
```bash
# Wireshark filters
http.request.method == "POST"
frame contains "flag"

# Extract files
foremost -i cap.pcap -o out/
```

## Memory (Volatility)
```bash
vol.py -f mem.dmp imageinfo
vol.py -f mem.dmp --profile=Win7SP1x64 pslist
vol.py -f mem.dmp --profile=Win7SP1x64 cmdline
```
