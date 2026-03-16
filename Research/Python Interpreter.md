# 2. What is a **Python interpreter (本质)**

The interpreter is:

> **A program that reads Python code and executes it.**

At the OS level:

**The Python interpreter is just a compiled executable program.**

Example:

/usr/bin/python3

or inside venv:

venv/bin/python

This file is a **binary executable**, written in **C (CPython)**.

Its job:

Python code (.py)  
        ↓  
Python interpreter  
        ↓  
convert to bytecode  
        ↓  
execute instructions

Simplified pipeline:

hello.py  
   ↓  
Python Interpreter  
   ↓  
Bytecode (.pyc)  
   ↓  
Python Virtual Machine  
   ↓  
CPU instructions

So the **interpreter itself is a program written mostly in C**.

Example:

print("hello")

Interpreter process:

1. parse syntax
    
2. compile to bytecode
    
3. run bytecode on Python VM


# Environment Variable


# Python Standard Library

The **Python standard library** is the set of modules that come **built into Python** when you install it.

You **do NOT install them with `pip`**. They are already included.

Examples of commonly used modules:

| Module       | What it does                       |
| ------------ | ---------------------------------- |
| `os`         | interact with the operating system |
| `sys`        | access Python runtime information  |
| `math`       | mathematical functions             |
| `datetime`   | work with dates and time           |
| `json`       | read/write JSON data               |
| `random`     | generate random numbers            |
| `re`         | regular expressions                |
| `pathlib`    | manipulate file paths              |
| `subprocess` | run other programs                 |
| `itertools`  | advanced iteration tools           |

Location (example):


```
/usr/lib/python3.x/
```

Inside you'll find files like:

os.py  
json/  
datetime.py

# Third-Party Packages

These are **libraries created by other developers** and distributed through **package repositories**.

Most Python packages come from  
Python Package Index (PyPI).

You install them using:

```bash
pip install package_name
```

Examples:

| Package        | Purpose               |
| -------------- | --------------------- |
| `numpy`        | numerical computing   |
| `pandas`       | data analysis         |
| `matplotlib`   | plotting              |
| `torch`        | deep learning         |
| `scikit-learn` | machine learning      |
| `requests`     | HTTP requests         |
| `flask`        | web development       |
| `transformers` | large language models |

Example:

```python
import numpy  
import pandas  
import torch
```

These only work **after installation**.

Location inside a **virtual environment**:

venv/lib/python3.x/site-packages/

Example folder:

site-packages/  
├── numpy  
├── pandas  
├── torch