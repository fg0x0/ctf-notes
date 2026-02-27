# 🔍 Forensics Cheatsheet

## File Analysis
```bash
file suspicious_file        # Magic bytes check
strings -a file | grep -i "flag\|ctf\|key\|pass\|secret"
xxd file | head -20         # Hex dump
binwalk -e file             # Extract embedded files
exiftool file               # Metadata analysis
```

## Steganography
```bash
# Image
steghide extract -sf image.jpg -p ""       # Empty password
steghide extract -sf image.jpg -p password
zsteg image.png            # LSB stego PNG/BMP
stegsolve                  # GUI — bit plane analysis
outguess -r image.jpg out.txt

# Audio
sonic-visualizer            # Spectrogram — hidden text
audacity                    # Visual inspection
```

## PCAP Analysis
```bash
# Wireshark filters
http.request.method == "POST"
tcp.stream eq 0
frame contains "flag"
http contains "password"

# tshark CLI
tshark -r capture.pcap -Y "http" -T fields \
  -e http.request.method -e http.host -e http.request.uri

# Extract files from pcap
foremost -i capture.pcap -o output/
networkMiner capture.pcap
```

## Memory Forensics (Volatility)
```bash
vol.py -f memory.dmp imageinfo           # OS detection
vol.py -f memory.dmp --profile=Win7SP1x64 pslist    # Processes
vol.py -f memory.dmp --profile=Win7SP1x64 cmdline   # Commands run
vol.py -f memory.dmp --profile=Win7SP1x64 filescan  # Files
vol.py -f memory.dmp --profile=Win7SP1x64 dumpfiles -Q 0xaddr -D out/
```

## Disk Forensics
```bash
fdisk -l disk.img           # Partition table
mount -o loop,offset=$((512*2048)) disk.img /mnt/
autopsy                     # GUI forensics suite

# Recover deleted files
photorec disk.img
foremost -i disk.img -o recovered/
```
