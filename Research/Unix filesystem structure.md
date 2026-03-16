# What `/usr` means

`/usr` is a standard directory in Unix/Linux systems.

Originally it meant:

> **User system resources**

Today it basically stores **applications and libraries installed by the system or package manager**.

Typical structure:

/usr  
├── bin  
├── lib  
├── share  
└── local

Purpose:

|Directory|Purpose|
|---|---|
|`/usr/bin`|executable programs|
|`/usr/lib`|libraries used by programs|
|`/usr/share`|shared data|
|`/usr/local`|locally installed software|

So `/usr` is a place for **software that users run**.

## What `/usr/bin` is used for

`bin` means **binary executable programs**.

So:

/usr/bin

contains **system executable programs**.

**`/usr/bin` does NOT store your `.py` files.**  
It stores **executable programs**, not user scripts.

Examples:

```bash
/usr/bin/python  
/usr/bin/git  
/usr/bin/node  
/usr/bin/vim  
/usr/bin/grep
```

These are **executable files**.

For example:

```bash
/usr/bin/python
```

is the **Python interpreter program itself** (written mostly in C and compiled).

So:

/usr/bin = system commands you can run

## What `/usr/lib` is used for

`lib` means **libraries**.

Libraries are **code that programs use**.

Example:

/usr/lib

contains shared libraries like:

/usr/lib/libssl.so  
/usr/lib/libpython3.x.so

For Python specifically:

/usr/lib/python3.x/

contains Python modules such as:

/usr/lib/python3.x/  
├── os.py  
├── math.py  
├── json/  
├── datetime.py

These are **Python standard library modules**.

So:

> `/usr/lib` = libraries used by programs.