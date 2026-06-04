# Guide 0: Set Up Python

This guide is for learners who have never used Python before. It helps you
install Python, understand `pip` and PyPI, create a project folder, install the
Open Data Products SDK, and verify that the `open-data-products` command works.

## What You Are Installing

- Python: the programming language used by the SDK.
- `pip`: Python's package installer.
- PyPI: the Python Package Index, where published Python packages live.
- `open-data-products`: the SDK package installed from PyPI.
- A virtual environment: a local `.venv` folder that keeps this lesson's Python
  packages separate from the rest of your computer.

## Windows

### 1. Install Python

Install Python from <https://www.python.org/downloads/windows/>.

During installation, enable the checkbox named **Add python.exe to PATH**. If
you miss it, rerun the installer and choose the option to modify your install.

Open PowerShell and check that Python works:

```powershell
py --version
py -m pip --version
```

### 2. Create a lesson folder

```powershell
mkdir odp-course
cd odp-course
```

### 3. Create and activate a virtual environment

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
```

If PowerShell blocks activation, run this command once for your current user,
then activate again:

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

### 4. Install the SDK from PyPI

```powershell
python -m pip install --upgrade pip
python -m pip install open-data-products
```

### 5. Verify the command

```powershell
open-data-products --help
```

## macOS

### 1. Install Python

Install Python from <https://www.python.org/downloads/macos/>.

You can also use Homebrew if you already have it:

```bash
brew install python
```

Open Terminal and check that Python works:

```bash
python3 --version
python3 -m pip --version
```

### 2. Create a lesson folder

```bash
mkdir -p odp-course
cd odp-course
```

### 3. Create and activate a virtual environment

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 4. Install the SDK from PyPI

```bash
python -m pip install --upgrade pip
python -m pip install open-data-products
```

### 5. Verify the command

```bash
open-data-products --help
```

## Linux

### 1. Install Python

Most Linux distributions include Python, but you may need the `venv` and `pip`
packages.

Debian or Ubuntu:

```bash
sudo apt update
sudo apt install python3 python3-pip python3-venv
```

Fedora:

```bash
sudo dnf install python3 python3-pip
```

Arch Linux:

```bash
sudo pacman -S python python-pip
```

Check that Python works:

```bash
python3 --version
python3 -m pip --version
```

### 2. Create a lesson folder

```bash
mkdir -p odp-course
cd odp-course
```

### 3. Create and activate a virtual environment

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 4. Install the SDK from PyPI

```bash
python -m pip install --upgrade pip
python -m pip install open-data-products
```

### 5. Verify the command

```bash
open-data-products --help
```

## Install Optional Extras

The normal course guides only require:

```bash
python -m pip install open-data-products
```

Some advanced workflows use optional dependencies. Install them only when a
guide asks for them:

```bash
python -m pip install "open-data-products[contracts]"
```

Use the same `python -m pip` pattern on Windows, macOS, and Linux after the
virtual environment is active.

## Start The First SDK Guide

Keep the virtual environment active. Your terminal prompt usually shows
`(.venv)` when activation worked.

Now open [Guide 1: Validate, Explain, and Summarize an ODPS Product](../01-validate-product/).

## What You Learned

- Python runs the SDK.
- `pip` installs Python packages from PyPI.
- `open-data-products` is the package name on PyPI.
- A virtual environment keeps course dependencies local to one folder.
- The `open-data-products` command is ready when `open-data-products --help`
  prints the command help.
