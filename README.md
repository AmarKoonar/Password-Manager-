#  Password Manager (C)

A lightweight command-line password manager written in C. It securely stores your login credentials using file I/O and encrypts passwords with OpenSSL.

## Features

-   password protection (hashed using SHA256)
-  File-based local storage
-  AES encryption for stored credentials
-  Add, retrieve, and delete password entries
-  Cross-platform support (Linux, macOS, Windows with some setup)

---

##  Requirements

Make sure you have the following installed:

- `gcc` or any C compiler
- `openssl` development libraries  
  - **Linux:** `sudo apt install libssl-dev`
  - **macOS:** `brew install openssl`
  - **Windows:** Download from [https://slproweb.com/products/Win32OpenSSL.html](https://slproweb.com/products/Win32OpenSSL.html) and configure paths manually

---

##  Build and Run

### 1. Clone the repo

```bash
git clone https://github.com/yourusername/password-manager-c.git
cd password-manager-c
