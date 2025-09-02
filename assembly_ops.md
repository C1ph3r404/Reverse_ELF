## 🔧 Common Assembly Instructions (x86/x86-64)

Here’s a quick rundown of the usual suspects you’ll see when reversing binaries:

### 📝 Data Movement
- `mov dst, src` → copy value from src → dst  
- `lea dst, [mem]` → load effective address (basically gives pointer, not value)  
- `push val` → put value on stack  
- `pop dst` → take value off stack into dst  

### ➕ Arithmetic & Logic
- `add dst, src` → dst = dst + src  
- `sub dst, src` → dst = dst - src  
- `inc dst` → dst = dst + 1  
- `dec dst` → dst = dst - 1  
- `mul src` → multiply (unsigned)  
- `imul src` → multiply (signed)  
- `div src` → divide (unsigned)  
- `idiv src` → divide (signed)  

- `and dst, src` → bitwise AND  
- `or dst, src` → bitwise OR  
- `xor dst, src` → bitwise XOR (xor eax, eax = fast zero)  
- `not dst` → bitwise NOT  
- `neg dst` → dst = -dst  

### 🔄 Shifts & Rotates
- `shl dst, n` → shift left (multiply by 2^n)  
- `shr dst, n` → logical shift right  
- `sar dst, n` → arithmetic shift right (keeps sign)  
- `rol dst, n` → rotate bits left  
- `ror dst, n` → rotate bits right  

### 🧭 Control Flow
- `jmp label` → jump to label (unconditional)  
- `call func` → call function (pushes return addr)  
- `ret` → return from function  

**Conditional jumps** (all after a `cmp a, b` or `test reg, reg`):  
- `je / jz` → jump if equal / zero  
- `jne / jnz` → jump if not equal / not zero  
- `jg / jnle` → jump if greater  
- `jl / jnge` → jump if less  
- `jge / jnl` → jump if greater or equal  
- `jle / jng` → jump if less or equal  
- `ja` → jump if above (unsigned)  
- `jb` → jump if below (unsigned)  

### 🧪 Compare & Test
- `cmp a, b` → sets flags after (a - b), doesn’t store result  
- `test a, b` → ANDs them, sets flags, doesn’t store result  

### ⚡ Misc
- `nop` → no operation (literally does nothing)  
- `int 0x80` / `syscall` → system call  
- `hlt` → halt CPU (usually not in userland stuff)  

---
💡 *Pro tip:* Most reversing comes down to spotting patterns — like `cmp` followed by a `je/jne`, or `xor eax, eax` as a fast way to clear a register.
