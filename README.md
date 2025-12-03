# PCSX2 Pine IPC Python Wrapper

A Python wrapper for PCSX2's Pine IPC protocol, allowing you to read and write PS2 memory from Python scripts.

## Installation

1. **Download the release**
   - `pcsx2_pine.py` - Python module
   - 'libpcsx2_ipc_bulk_c.dll' - Modified Pine IPC DLL

2. **Enable Pine IPC in PCSX2:**
   - Open PCSX2
   - Go to Settings
   - Under Advanced, scroll down to PINE Setting, check enable. Set the port to 28011
   - Restart PCSX2

## Quick Start

```python
import pcsx2_pine as p

# Initialize connection
if p.init():
    # Read a 32-bit integer
    health = p.read_u32(0x00100000)
    print(f"Health: {health}")
    
    # Write a 32-bit integer
    p.write_u32(0x00100000, 69)
    
    # Read multiple bytes (12 bytes in this case)
    data = p.read_pcsx2_memory(0x00200000, 12)

    # Write multiple bytes (9 bytes in this case)
    my_bytes = bytes([0x11, 0x22, 0x33, 0x44, 0x55, 0x66, 0x77, 0x88, 0x99])
    data = p.write_pcsx2_memory(0x00200000, my_bytes)

    # Write a binary file to PCSX2 Memory ---
    BIN_FILENAME = "memory_patch.bin"

    # Read data from the binary file in binary mode ('rb')
    with open(BIN_FILENAME, 'rb') as f:
        file_data = f.read()
    
    # Write the file data (byte array) directly to PCSX2 memory
    if file_data:
        TARGET_ADDRESS = 0x00300000
        p.write_pcsx2_memory(0x00300000, file_data)
    
    # Cleanup
    p.shutdown()
```

## API Reference
```python
# Read single values
health = pcsx2_pine.read_u8(address)   # Read 8-bit integer
score = pcsx2_pine.read_u16(address)   # Read 16-bit integer
value = pcsx2_pine.read_u32(address)   # Read 32-bit integer
big_num = pcsx2_pine.read_u64(address) # Read 64-bit integer

# Write single values
pcsx2_pine.write_u8(address, value)    # Write 8-bit integer
pcsx2_pine.write_u16(address, value)   # Write 16-bit integer
pcsx2_pine.write_u32(address, value)   # Write 32-bit integer
pcsx2_pine.write_u64(address, value)   # Write 64-bit integer

# Read multiple bytes (returns bytes object)
data = pcsx2_pine.read_pcsx2_memory(address, num_bytes)

# Write multiple bytes
pcsx2_pine.write_pcsx2_memory(address, data_bytes)
```

## Requirements

- Python 3.6+
- PCSX2 with Pine IPC support

## Credits

- Pine by GovanifY

## Links

- PCSX2: https://pcsx2.net/
- Pine:  https://github.com/GovanifY/pine