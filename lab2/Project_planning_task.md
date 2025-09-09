# Plan for Developing a Console-Based Simple Calculator Application (C)

#### Done by Timur Zhaken Student ID 140314246 and Raphael Provido Student ID 122473259

## Scenario Chosen

**Develop a desktop application** — a simple **console calculator** for **Windows/macOS** built in **C**.

## Tech Stack Recommendation

* **Language**: C 
* **Interface**: Command Line Interface
* **Build system**: CMake (or simple gcc/clang commands)
* **Compiler**: GCC/Clang (macOS, Windows with MinGW or MSYS2)
* **Collaboration**: Github (Git)


## Minimum and Recommended Hardware and OS requirements

In order to create and run the simple desktop calculator app you only need to minimum requirements to run Visual Studio Code but it is best to use recommended required hardware for a much smoother experience.

### Minimum Requirements

1.6 GHz processor.

1 GB of RAM.

### Recommended Requirements

Any CPU faster than 1.6 GHz.

4 GB of RAM or more.

### OS requirements 

Windows 10 and 11 (64-bit)

macOS versions with Apple security update support. This is typically the latest release and the two previous versions.

# 1.0) IDE of Choice

### IDE Options

* **Visual Studio Code** - This IDE was chosen because it is universal meaning it can be used in MAC and Windows. It is easy to use and has a beginner friendly UI.

### How to install and setup Visual Studio Code

1) Go on [code.visualstudio.com](https://code.visualstudio.com/) and press the "Download" button on the top right corner.

2) After downloading the setup double click on it and launch it.

3) After launching the setup, follow the instructions on it and download Visual Studio Code.

### Downloading Compiler

#### Now that you have Visual Studio Code installed you have to download a compiler for it.

#### Options for the Compiler 

* **MinGW** 
* **MSYS2**

A compiler is necessary because:
Computers do not understand C code directly; they only execute machine code (binary instructions).
The compiler translates human-readable C source code (.c files) into executable programs (.exe on Windows, binary on macOS).
It also checks for errors, ensures correct syntax, and optimizes the code for performance.
Without a compiler, your C code is just text — it cannot be executed.

---

## 1.1) Options for the Compiler

### MinGW (Windows)

**MinGW** (Minimalist GNU for Windows) provides GCC (the GNU Compiler Collection) for Windows.

* **Why use it?**

  * Lightweight and focused on compiling C/C++ programs.
  * Produces native Windows executables.
* **How to install:**

  1. Download **MSYS2** (which includes MinGW) from [msys2.org](https://www.msys2.org/).
  2. Open the **MSYS2 MinGW x64** shell.
  3. Update packages:

     ```bash
     pacman -Syu
     ```
  4. Install the compiler toolchain:

     ```bash
     pacman -S --needed mingw-w64-x86_64-toolchain
     ```
  5. Verify installation:

     ```bash
     gcc --version
     g++ --version
     gdb --version
     ```

### MSYS2 (Windows)

**MSYS2** is a broader development environment for Windows that includes **MinGW** and additional tools.

* **Why use it?**

  * Provides not only GCC but also package management (`pacman`) to install tools like CMake, Git, and libraries.
  * Easier to maintain and update than standalone MinGW.
* **How to install:**

  1. Download installer from [msys2.org](https://www.msys2.org/).
  2. Install MSYS2 and open the *MSYS2 MSYS* shell.
  3. Update core system packages:

     ```bash
     pacman -Syu
     ```

     Close and reopen shell if prompted.
  4. Install development tools:

     ```bash
     pacman -S --needed base-devel git mingw-w64-x86_64-toolchain cmake
     ```

  5. Verify installation:

     ```bash
     gcc --version
     g++ --version
     gdb --version
     ```
  
  6. Use the **MSYS2 MinGW x64** shell to build C projects.

### Clang (macOS)

**Clang** is the default C/C++ compiler on macOS.

* **Why use it?**

  * Comes with Xcode Command Line Tools.
  * Optimized for Apple platforms.
* **How to install:**

  1. Open Terminal.
  2. Run:

     ```bash
     xcode-select --install
     ```
  3. Verify installation:

     ```bash
     clang --version
     ```

---

## 1.2) Adding Compiler to PATH (Editing System Environment Variables)

To use the compiler (`gcc`, `g++`, or `clang`) from any terminal window, its installation folder must be included in your system **PATH environment variable**.

### Windows (MinGW/MSYS2)

1. Find the compiler binaries, e.g.:

   * `C:\msys64\mingw64\bin`
2. Copy this path.
3. Open **System Properties** → **Advanced system settings** → **Environment Variables**.
4. Under *System variables*, select `Path` → **Edit**.
5. Click **New** and paste the path.
6. Click **OK** to save and restart your terminal.
7. Test by opening *Command Prompt* and running:

   ```bash
   gcc --version
   ```

   If it prints the version, PATH is set correctly.

### macOS (Clang)

* Usually Clang is already on PATH after installing Xcode Command Line Tools.
* To check:

  ```bash
  which clang
  ```

  If it shows a path like `/usr/bin/clang`, you’re ready.
* If needed, you can add a path manually:

  1. Open `~/.zshrc` (default shell) with a text editor.
  2. Add:

     ```bash
     export PATH="/usr/local/bin:$PATH"
     ```
  3. Save and run `source ~/.zshrc`.

---

## 1.3) Extensions for Visual Studio Code

* **C++/C Microsoft**
* **Code Runner**

**C++/C Microsoft** - provides IntelliSense which is needed for code completion and suggestions for C and C++ and enables debugging right in VS Code.

**Code Runner** - it lets you quickly run code in many languages with one click, showing the output directly in the editor without extra setup. It’s fast, lightweight, and good for testing small programs or snippets.

### Now that you have installed VS Code and set it up you can now proceed making the project.

# 2.0) GitHub Setup for Collaboration

Since the project will be developed by 2 people, using GitHub ensures smooth collaboration, version control, and backup.

# Steps to Set Up GitHub for the Team:

## 2.1)Install Git

### On Windows:
Download Git from https://git-scm.com/downloads
 and install with default settings.

### On macOS:
Run in terminal:

```
brew install git
```

## 2.2) Create GitHub Accounts

Each team member should create a free GitHub account at https://github.com/

## 2.3) Create a Repository

1) One member creates a new repository (e.g., console-calculator) on GitHub.

2) Set it to public (or private and invite the collaborator).

3) Add a README file for documentation.

## 2.4) Clone the Repository
Each member clones the repository to their local machine.
```
git clone https://github.com/username/console-calculator.git
```
## 2.5)Basic Git Workflow for 2 Developers

Before making changes:
```
git pull
```
Create a new branch for features:
```
git checkout -b feature-branch
```

After editing code:
```
git add .
git commit -m "Added new feature"
git push origin feature-branch
```

* **Create a Pull Request (PR) on GitHub.**

* **The other teammate reviews and merges it into main.**

## 2.6) Handling Merge Conflicts

* **If both edit the same file, GitHub will highlight conflicts.**

* **Resolve conflicts manually in VS Code, then commit and push again.**

## 2.7) Recommended Branching Model

```main``` → stable, working code only.

```feature-*``` → branches for new features/changes.

Always merge into ```main``` via Pull Request for review.

# 3.0) Making the Desktop CLI Calculator using C

The calculator must be able to do basic operations (+, −, ×, ÷), integer & float input, clear, exit and some advanced operations like power (^), modulo, square root.


## 3.1) Error Handling

### 1) Invalid Input
Users may type letters or symbols instead of numbers.
This could cause the program to crash or behave unexpectedly.

### 2) Division by Zero
If the user tries to divide a number by zero, it will cause a runtime error.

### 3) Floating-point Errors
Operations like 1/3 or large powers may show inaccurate results due to floating-point precision limits.

### 4) Negative Numbers in Square Roots
Entering a negative number for the square root function may cause math errors or undefined results.

### 5) Overflow and Underflow
Very large numbers (e.g., in powers) or very small numbers may exceed data type limits, leading to incorrect results.

### 6) Operation Misuse
Users might enter unexpected sequences (e.g., multiple operators without numbers), causing calculation errors.

# 4.0) Collaboration and Realistic Timing 

Judging by the simplicity of the project it is fair to assume that the project can be done in one day.