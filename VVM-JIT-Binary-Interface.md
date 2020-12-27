---
name: EVM JIT Binary Interface
category: 
---

# JIT C Interface

``` C
#include <stdint.h>

// JIT object opaque type
typedef struct vvm_jit vvm_jit;

// Contract execution return code
typedef int vvm_jit_return_code;

// Host-endian 256-bit integer type
typedef struct i256 i256;

// Big-endian right aligned 256-bit hash
typedef struct h256 h256;

// Runtime data struct - must be provided by external language (Go, C++, Python)
typedef struct vvm_jit_rt vvm_jit_rt;

// Runtime callback functions  - implementations must be provided by external language (Go, C++, Python)
void vvm_jit_rt_sload(vvm_jit_rt* _rt, i256* _index, i256* _ret);
void vvm_jit_rt_sstore(vvm_jit_rt* _rt, i256* _index, i256* _value);
void vvm_jit_rt_balance(vvm_jit_rt* _rt, h256* _address, i256* _ret);
// And so on...

vvm_jit* vvm_jit_create(vvm_jit_rt* _runtime_data);

vvm_jit_return_code vvm_jit_execute(vvm_jit* _jit);

void vvm_jit_get_return_data(vvm_jit* _jit, char* _return_data_offset, size_t* _return_data_size);

void vvm_jit_destroy(vvm_jit* _jit);
```

# Return Code

Informs user about contract exit status:

Code| Exit Status
----|-----
0   | Stop
1   | Return
2   | Suicide
101 | Bad Jump Destination
102 | Out Of Gas
103 | Stack Underflow
104 | Bad Instruction



# JIT Runtime Data

A set of data possibly needed by running contract, sometimes by the compiler itself. 
Can be called ExtVM data in C++, VMEnv data in Go.

Name         | Type | Access | Description
-----        |------|--------|------------
Gas          | i256 | inout  | Gas counter.
Address      | h256 | in     | Account address.
Caller       | h256 | in     | 
Origin       | h256 | in     | 
CallValue    | i256 | in     | 
CallDataSize | i256 | in     | 
GasPrice     | i256 | in     | 
PrevHash     | i256 | in     | 
CoinBase     | h256 | in     | 
TimeStamp    | i256 | in     | 
Number       | i256 | in     | 
Difficulty   | i256 | in     | 
GasLimit     | i256 | in     | 
CodeSize     | i256 | const  | 
CallData     | byte*| in     |
Code         | byte*| const  |
