# Extracting data

## Getting data out of images

### Check Metadata and file information
```bash
exiftool IMAGE
binwalk IMAGE
steghide info IMAGE
```

### Search for hidden files
```bash
binwalk IMAGE

# If something was found, extract
binwalk -e IMAGE

# If this failes, use the offset to extract manually
dd if=IMAGE of=extracted.zip bs=1 skip=OFFSET
```

### Extract data using `steghide`
```bash
# Extract simple data
steghide extract -sf IMAGE

# Extract password protected data
steghide extract -sf IMAGE -p PASSPHRASE
```
