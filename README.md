# Check CRC32

Python script to check and/or add the CRC32 hash of a file to the filename. I wanted something like [RapidCRC](https://rapidcrc.sourceforge.net/index.html) in script form for Linux, so I made this small script to do something similar.

## Usage

To check CRC32 hashes:
```bash
$ check-crc32 file1.txt "file2 [1234ABCD].txt" "file3 [FFFF1111].txt"
 × file.txt
 ○ file [1234ABCD].txt
 × file [FFFF1111].txt
```

To append a CRC32 hash:
```bash
$ check-crc32 -a file1.txt file2 [A2A2A2A2].txt 
 + file1.txt -> file1 [1F1F1F1F].txt
 ○ file2 [A2A2A2A2].txt
```

Append a CRC32, even if incorrect one is found:
```bash
$ check-crc32 -a -f file [1F1F1F1F].txt
 ! file [1F1F1F1F].txt -> file [1F1F1F1F] [A2A2A2A2].txt
```

Help menu:
```
$ check-crc32 --help
usage: check-crc32 [-h] [-v] [-q] [-d] [-c CHUNK_SIZE] [-f] [-a]
                   [src [src ...]]

Check the CRC32 hash of a file in form of a hexadecimal string in brackets.
The '-a' flag can be used to append the CRC32 hash to the filename if it is
not found. See the optional arguments for more options.

positional arguments:
  src                   input files

optional arguments:
  -a, --append          append CRC32 hash to filename
  -c CHUNK_SIZE, --chunk-size CHUNK_SIZE
                        chunk size in bytes when reading files
  -d, --dry-run         run without modifying files
  -f, --force           append even if an incorrect CRC32 hash is found
  -h, --help            show this help message and exit
  -q, --quiet           suppress output
  -v, --version         print version
```