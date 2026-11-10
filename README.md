# 🔐 Multi-Algorithm Encryption & Decryption System

A console-based **encryption suite written entirely in x86 Assembly (MASM)** using the **Irvine32** library. Encrypt and decrypt text with four different ciphers, process files, analyse letter frequencies and get an instant **encryption strength rating**, all from an animated, menu-driven interface.

---

## ✨ Features

- **Four cipher algorithms** to choose from
- **Text mode:** type a message (up to 255 characters) and encrypt it
- **File Encryption Mode:** read a file, encrypt it, and save the result to a new file
- **Decryption** of the last encrypted message with the matching algorithm
- **Algorithm verification:** trying to decrypt with the wrong algorithm is detected and rejected
- **Frequency Analysis:** letter-by-letter (A–Z) count of the ciphertext
- **Encryption Strength Meter:** rates each result as *Weak*, *Medium* or *Strong*
- **Operation summary:** shows the algorithm used and the key after every encryption
- **Polished console UI:** typing-effect welcome screen, centred bordered menus and input prompts

---

## 🔑 Supported Algorithms

| # | Algorithm | How it works | Key |
|---|---|---|---|
| 1 | **Caesar Cipher** | Shifts each letter forward in the alphabet, preserving case; non-letters are untouched | User-chosen shift 1–25 (Enter / invalid input falls back to the default of 3) |
| 2 | **XOR Cipher** | XORs every byte with a single-byte key | User-entered numeric key |
| 3 | **Substitution Cipher** | Replaces each letter using a fixed 26-letter mapping table (`QWERTYUIOPASDFGHJKLZXCVBNM`), preserving case | Built-in substitution table |
| 4 | **One-Time Pad (OTP)** | XORs each byte with a **randomly generated** key of the same length as the message | Random key, displayed in hex |

For the OTP, both the **ciphertext and the key are printed in hexadecimal**.

---

## 📊 Encryption Strength Meter

After each encryption the program scores the result out of 100 and prints a rating. The score combines:

1. **Algorithm score:** Caesar 10, XOR 15, Substitution 30, OTP 90
2. **Key length score:** longer keys score higher (capped)
3. **Diversity score:** the number of unique bytes in the key and in the ciphertext (capped)

| Score | Rating |
|---|---|
| below 40 | Weak |
| 40 – 74 | Medium |
| 75 and above | Strong |

---

## 🖥️ Program Flow

```
   Welcome animation
          │
   ┌──────▼───────────────────────────┐
   │  ADVANCED ENCRYPTION SUITE       │
   │  [1] Encrypt Message             │
   │  [2] Decrypt Message             │
   │  [3] File Encryption Mode        │
   │  [4] Frequency Analysis          │
   │  [5] Exit                        │
   └──────────────────────────────────┘
```

- **[1] Encrypt:** enter text, choose an algorithm, supply a key if needed, then see the ciphertext, summary and strength rating.
- **[2] Decrypt:** choose the algorithm used; the program remembers the algorithm and key from the last encryption, validates the choice and prints the recovered plaintext.
- **[3] File mode:** enter an input file name, pick an algorithm, and enter an output file name to save the encrypted data.
- **[4] Frequency analysis:** prints how many times each letter appears in the ciphertext.
- **[5] Exit:** closes the program.

---

## 📁 Project Structure

```
Multi-Algorithm-Encryption-Decryption-System/
└── Encryption_system.asm     # Complete source code
```

### Main procedures

| Procedure | Purpose |
|---|---|
| `IntroAnimation` | Typing-effect welcome screen |
| `PrintMENU`, `printAlgo`, `WriteCentered` | Menus and centred text layout |
| `EncryptCaesar` / `DecryptCaesar` | Caesar cipher |
| `EncryptXor` / `DecryptXor` | XOR cipher |
| `encryptSub` / `decryptSub` | Substitution cipher |
| `encryptOTP` / `decryptOTP` | One-Time Pad with random key generation |
| `FrequencyAnalysis` | A–Z letter counter |
| `StrengthMeter` | Strength scoring and rating |
| `PrintSummary`, `ResultEnc`, `ResultDec` | Result and summary output |
| `ReadFileToBuffer`, `WriteBufferToFile` | File input and output |

---

## 🛠️ Tech Stack

- **Language:** x86 Assembly (MASM, 32-bit)
- **Library:** [Irvine32](http://programmedlessons.org/AssemblyTutorial/) (from *Assembly Language for x86 Processors* by Kip Irvine)
- **Platform:** Windows console
- **Recommended setup:** Visual Studio with the MASM Irvine32 project template

---

## 🚀 Getting Started

### Prerequisites
- Windows
- Visual Studio with the **Desktop development with C++** workload (includes MASM)
- The **Irvine32 library** set up for your project (`Irvine32.inc`, `Irvine32.lib`, `Kernel32.lib`)

### Build and run (Visual Studio)
1. Create a new **Empty Project** configured for MASM (Build Customizations → *masm*) with the Irvine32 include and library paths set.
2. Add `Encryption_system.asm` to the project.
3. Set the platform to **x86 (Win32)**.
4. Build and run with **Ctrl + F5**.

### Build from the command line (alternative)
From a Visual Studio *x86 Native Tools* prompt, with the Irvine32 files in the same folder or on the include/lib path:
```bash
ml /c /coff Encryption_system.asm
link /SUBSYSTEM:CONSOLE Encryption_system.obj irvine32.lib kernel32.lib user32.lib
Encryption_system.exe
```

---

## 🎮 Example Session

```
Select Option: ====> 1
Enter plaintext (max 255 chars) =====>  Hello World

Choose Algorithm ====> 1
Enter key (1 to 25 => press Enter for default 3): 5

---------------SUMMARY------------------
 Encrypted string ====>>: Mjqqt Btwqi
 [Summary] Encryption Completed Successfully
 Algorithm ====>> Caesar Cipher
 Key Used  ====>> 5
 Strength ====>> Weak
----------------------------------------------
```

Then choose **[2] Decrypt Message**, select the same algorithm, and the original text is restored.

---

## 🎓 Concepts Demonstrated

- Low-level string and byte manipulation in assembly
- Procedures, stack frames and parameter passing
- Lookup-table based substitution
- Pseudo-random number generation (`Randomize`, `RandomRange`)
- File I/O (`OpenInputFile`, `ReadFromFile`, `CreateOutputFile`, `WriteToFile`)
- Building interactive console UIs with Irvine32 (`Gotoxy`, `Clrscr`, `Delay`)

---

## 👤 Author

**Abdullah Karim**
