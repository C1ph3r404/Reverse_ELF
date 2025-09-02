# 📝 Writeup – Reverse_ELF (TryHackMe)

---

## CrackMe1

![crackme1](screenshots/crackme1.png)

Easy start: give permission and run the binary. Simple “hello world” of reversing.

---

## CrackMe2

![crackme2](screenshots/crackme2.1.png)
![crackme2](screenshots/crackme2.2.png)

Use `strings` to show readable text in the binary. Sometimes the flag is just sitting there, waving at you.

---

## CrackMe3

![crackme3](screenshots/crackme3.1.png)
![crackme3](screenshots/crackme3.2.png)

Binary gives Base64? Decode it. Flag revealed. Easy win.

---

## CrackMe4

Need basic assembly knowledge: `MOV, LEA, CMP, ADD, SUB, PUSH, POP, JE, JMP, JNE, TEST`. Full list [here](./assembly_ops.md).

Open radare2:

```bash
r2 -d crackme4
```

To run with an argument:

```bash
r2 -d ./crackme4 <argument>
```

### Key radare2 commands

* `aaa` → analyze everything
* `afl` → list functions
* `pdf @<function>` → disassemble/view function
* `db <address>` → set breakpoint
* `dc` → continue/run
* `px @<register>` → inspect register

Run `aaa` → `afl` → `pdf @main`. Check `sym.compare_pwd` where input is compared to password. Set breakpoint at `strcmp`, check `rdi`/`rsi` for the real password.

![crackme4](screenshots/crackme4.1.png)
![crackme4](screenshots/crackme4.2.png)
![crackme4](screenshots/crackme4.3.png)

---

## CrackMe5

Same as CrackMe4: find the comparison function, set a breakpoint, inspect, extract password. Sometimes the binary is just nice enough to show it upfront.

![crackme5](screenshots/crackme5.1.png)
![crackme5](screenshots/crackme5.2.png)

---

## CrackMe6

Go to `main`, check suspicious functions (`sym.my_secure_test`). Compares input character by character. Registers show red indicators for correct characters in em.

![crackme6](screenshots/crackme6.1.png)
![crackme6](screenshots/crackme6.2.png)

---

## CrackMe7

Input is compared to a hex value (`0x7a69`). Convert to decimal → password. Sometimes reversing is just math in disguise.

![crackme7](screenshots/crackme7.1.png)
![crackme7](screenshots/crackme7.2.png)

---

## CrackMe8

Use **Ghidra** here—it’s faster than r2 for reading code.

* Import binary, check `main`.
* Ghidra makes tracing logic simple.
* r2 works too, good for practice.

![crackme8](screenshots/crackme8.png)

---

**Note:** Basics first, advanced later. Strings + Base64 + Radare2 + Ghidra covers most challenges here.

⚠️ **Disclaimer:** Only try this on legal labs or CTFs.

