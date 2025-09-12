## 🔧 Common Assembly Instructions (x86/x86-64)

Here’s a quick rundown of the usual suspects you’ll see when reversing binaries:

On x86-64 (a.k.a. AMD64), you’ve got **16 general-purpose 64-bit registers** 👇

```
RAX  RBX  RCX  RDX
RSI  RDI  RBP  RSP
R8   R9   R10  R11
R12  R13  R14  R15
```

---

📝 Quick breakdown:

* **RAX, RBX, RCX, RDX** → classic ones (used since 16-bit days).
* **RSI, RDI, RBP, RSP** → for source/dest indexes, base/frame pointer, stack pointer.
* **R8–R15** → added when 64-bit mode came in (extra breathing room).

Each has "sub-registers":

* 64-bit: `RAX`
* 32-bit: `EAX`
* 16-bit: `AX`
* 8-bit: `AL` (low) and `AH` (high, for the old ones only)

⚡ For `R8–R15`, you get `R8D` (32-bit), `R8W` (16-bit), `R8B` (8-bit). No AH/BH/CH/DH mess there.

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
