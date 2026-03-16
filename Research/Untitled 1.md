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