# Installing Rust on Windows with Visual Studio Code and MSYS2 MinGW (Optional)

This guide explains how to install Rust on Windows with Visual Studio Code and optionally MSYS2 MinGW, without requiring "Microsoft C++ Build Tools." It also provides steps to use gcc or clang tools from the MSYS2 suite for building Rust programs.

## Why This Guide?

- Avoid installing "Microsoft C++ Build Tools" (requires a large Windows SDK).
- Use MSYS2's gcc or clang compilers as an alternative.
- Run and debug Rust programs in Visual Studio Code seamlessly.

## Overview of Installations

1. Install Visual Studio Code
2. (Optional) Install MSYS2
3. Install Rust
4. Install Python if not already installed
5. Add necessary folders to the PATH variable
6. Install `rust-analyzer` and `CodeLLDB` extensions in Visual Studio Code

---

## Detailed Steps

### Part 1: Installation Steps with Details

#### 1. Install Visual Studio Code

- Download the portable version of Visual Studio Code for Windows from filehorse.com or install it through your preferred method.
- Open Visual Studio Code and disable telemetry:

  - Go to `Edit > Preferences > Settings`.
  - Type "telemetry" in the search box and disable the options:

    ```json
    "telemetry.enableCrashReporter": false,
    "telemetry.enableTelemetry": false
    ```

- Recommended Fonts: Fira Code, Consolas, DejaVu Sans Mono, Droid Sans Mono Slashed, Inconsolata-g, Bitstream Vera Sans Mono, Lucida Console, Meslo LG DZ.
- Enable font ligatures for better coding visuals in VS Code.

#### 2. (Optional) Install MSYS2

- Download and install MSYS2 from [msys2.org](https://www.msys2.org/).
- Run `pacman -Syu` to update packages.
- Open the "MSYS2 MSYS" shell (not MinGW) and run `pacman -Su`.
- For MinGW compilers:

  - Open "MSYS2 MinGW 64-bit" shell.
  - Run `pacman -S mingw-w64-x86_64-toolchain`.

  > Note: The `--needed base-devel` package is optional and may not be required for basic Rust programs.

#### 3. Install Rust

- Download `rustup-init.exe` from [rust-lang.org](https://rust-lang.org).
- Run the installer and select "Customize installation."
- Use `x86_64-pc-windows-gnu` for MSYS MinGW or `x86_64-pc-windows-msvc` for "Microsoft C++ Build Tools."

  > If Rust is already installed, switch toolchains using:
  >
  > ```bash
  > rustup toolchain install stable-x86_64-pc-windows-gnu
  > rustup default stable-x86_64-pc-windows-gnu
  > ```

#### 4. Add Folders to PATH

- Add the following directories to the Windows system PATH variable:

  ```txt
  C:\Users\user\.cargo\bin;D:\Applications\msys64;D:\Applications\msys64\mingw64\bin
  ```

- Verify PATH updates by opening a new Command Prompt or PowerShell window and running:

  ```bash
  cargo --version
  gcc --version
  rustc --version
  ```

#### 5. Install Rust Extensions for Visual Studio Code

- Install Python 3.6.3 (ensure it is added to PATH during installation).
- From the VS Code Marketplace, install:
  - `rust-analyzer` (by matklad).
  - `CodeLLDB` (by Vadim Chugunov).

#### 6. Configure Cargo for MSYS2 (Optional)

- Create a `.cargo/config` file at `C:\Users\user\.cargo\config` with one of the following configurations:

  **For clang:**

  ```toml
  [target.x86_64-pc-windows-gnu]
  linker = "D:\Applications\msys64\mingw64\bin\clang++.exe"
  ar = "D:\Applications\msys64\mingw64\bin\llvm-ar.exe"
  ```

  **For gcc:**

  ```toml
  [target.x86_64-pc-windows-gnu]
  linker = "D:\Applications\msys64\mingw64\bin\gcc.exe"
  ar = "D:\Applications\msys64\mingw64\bin\ar.exe"
  ```

---

### Part 2: Running and Debugging Rust Programs in VS Code

1. Create a folder for your Rust project and open it in VS Code.
2. Open the terminal (Ctrl+`), and run:

   ```bash
   cargo init
   cargo run
   ```

3. To debug, put a breakpoint in your code and hit `F5`. If prompted, generate the `launch.json` file.
4. Alternatively, use the `Run` and `Debug` buttons provided by `rust-analyzer`.

---

Enjoy building Rust applications on Windows with Visual Studio Code!
