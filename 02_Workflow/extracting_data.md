# Extracting data

## Getting data out of images

### Check Metadata
```bash
exiftool IMAGE
```

### Search for hidden files
```bash
binwalk IMAGE

# If something was found, extract
binwalk -e IMAGE

# If this failes, use the offset to extract manually
dd if=IMAGE of=extracted.zip bs=1 skip=OFFSET
```
