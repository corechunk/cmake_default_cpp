# cmake_default_cpp

A minimal CMake learning tool and template for C++ projects.

---

## 📦 Requirements

- **CMake** (version 3.5 or newer) must be installed and available in your PATH.
- A **C++ compiler** must be installed and available in your PATH:
  - For C++ Compilers: [Visit This Link](https://github.com/corechunk/extras/blob/main/files/compilers/c_cpp/c_cpp_compilers.md)

---

## 📁 Project Structure

If you use this repository as a template, read this description!

- The `src` and `utils` folders are for organizing your `.cpp` files.
- Build directories (e.g., `bin_native`) are for your compiled output.
- Build directories *must* contain the string "bin" in their name to be excluded from source file discovery by this project's `CMakeLists.txt`. This is a specific setup for this repository, not a universal CMake rule.

```
.
├── src/            # Source files (e.g., calc.cpp)
├── utils/          # Utility source files (e.g., nPow.cpp)
│
├── bin_native/     # Default build output directory for native compilation
│
├── CMakeLists.txt  # Main CMake configuration file (required)
│
└── README.md       # This file
```

---

## 🚀 How to Build and Run

### Default Build (Native Compiler)

This is the standard way to build the project using the native `g++` compiler that you likely already have on your system. This will compile the project for your current operating system and architecture. `bin_native` is just an example name for the build directory used in this repository.

### 1. Configure the Project

Open a terminal in the project root and run:

```bash
cmake -S . -B bin_native -DCMAKE_CXX_COMPILER=g++
```

- `-S .` : Source directory (where `CMakeLists.txt` is located)
- `-B bin_native` : Build directory (where build files and cache will be generated)

### 2. Build the Project

After configuration, build the project with:

```sh
cmake --build bin_native
```

- This uses the cached settings in `bin_native` from the previous step.
- The resulting executable (e.g., `app` or `app.exe`) will be placed in the `bin_native` directory.

### 3. Run the Application

From the project root, the execution command depends on your operating system and shell:

**On Linux/macOS (Bash/Zsh):**
```bash
./bin_native/app
```
Or, if you need to pass arguments:
```bash
./bin_native/app <base> <exponent>
```

**On Windows (PowerShell):**
```powershell
.\bin_native\app.exe
```
Or, if you need to pass arguments:
```powershell
.\bin_native\app.exe <base> <exponent>
```

**On Windows (Command Prompt):**
```cmd
bin_native\app.exe
```
Or, if you need to pass arguments:
```cmd
bin_native\app.exe <base> <exponent>
```

---

## 🌐 Cross-Compilation

Cross-compilation is the process of building an executable that will run on a different operating system or architecture than the one you are building on.

### aarch64 Linux

To build for `aarch64` Linux from an `x86_64` Linux machine, you will need the `aarch64-linux-gnu-g++` cross-compiler.

```bash
cmake -S . -B binL_aarch64 -G "Unix Makefiles" -DCMAKE_CXX_COMPILER=aarch64-linux-gnu-g++
cmake --build binL_aarch64
```

### x86_64 Windows (MinGW)

To build for `x86_64` Windows from a Linux machine, you will need the MinGW-w64 toolchain, specifically the `x86_64-w64-mingw32-g++` compiler.

```bash
cmake -S . -B binW_x86_64 -G "Unix Makefiles" -DCMAKE_CXX_COMPILER=x86_64-w64-mingw32-g++
cmake --build binW_x86_64
```

### aarch64 Windows (MinGW)

**Note:** The toolchain for Windows on ARM64 is experimental and not yet available in official repositories. You will likely need to build it from source. A community effort to create this toolchain can be found at [Windows-on-ARM-Experiments/mingw-woarm64-build](https://github.com/Windows-on-ARM-Experiments/mingw-woarm64-build).

Once the `aarch64-w64-mingw32-g++` compiler is available on your system, you can use the following command:

```bash
cmake -S . -B binW_aarch64 -G "Unix Makefiles" -DCMAKE_CXX_COMPILER=aarch64-w64-mingw32-g++
cmake --build binW_aarch64
```

---

## 🛠️ Notes

- You can change the build directory name (e.g., `bin_native`, `binL_aarch64`, etc.), but remember that it *must* contain the string "bin" due to this project's `CMakeLists.txt` configuration.
- To clean the build, simply delete the corresponding build directory (e.g., `rm -rf bin_native`).
- If you change the generator or toolchain, always delete the build directory and re-run the configuration step.
- **NixOS Users:** If you are using NixOS, you might need to specify the `--sysroot` flag to point to the correct system root when running `cmake`.

---

## 💡 CMake Command Reference

- **Configure:**  
  `cmake -S <source_dir> -B <build_dir> -G <build_tool> -DCMAKE_CXX_COMPILER=<compiler>`
  - `-G <build_tool>`: if not set by default CMake uses NMake (on Windows) or Unix Makefiles (on Linux/macOS).
  - Use `-G "MinGW Makefiles"` if you don't want to use NMake and prefer the default `mingw32-make` generator that comes with your MinGW compiler.

- **Build:**  
  `cmake --build <build_dir>`

- **Clean:**  
  `cmake --build <build_dir> --target clean`

- **Verbose Build:**  
  `cmake --build <build_dir> --verbose`

---

Happy Coding! 🚀