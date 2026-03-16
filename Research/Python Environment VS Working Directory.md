---
Date: 2026-03-16
---
**the terminal actually tracks two different contexts at the same time**:

1. **Working directory (where you are in the filesystem)**
    
2. **Environment (which tools/interpreter you are using)**
    

These are **independent concepts**.

---

# 1️⃣ Working Directory = where your files are

The **working directory** tells the shell **which folder you are currently in**.

Example:

pwd

Output:

/Users/zhang/project

Commands like these change the working directory:

cd project  
cd ..  
cd ~/Downloads

So the terminal prompt may show:

~/project %

Meaning:

current working directory = project folder

This affects:

- file paths
    
- where files are created
    
- where scripts run
    

Example:

python main.py

Python will look for `main.py` **in the current folder**.

---

# 2️⃣ Environment = which Python/tools are used

The **environment controls which executables and libraries are used**.

Example environments:

- system Python
    
- `venv`
    
- `conda env`
    

When you activate an environment:

conda activate myenv

Conda **modifies the `PATH` variable**, so the shell uses a different Python.

Example:

(myenv) user@mac project %

Now:

python

points to:

anaconda3/envs/myenv/bin/python

instead of:

/usr/bin/python

---

# 3️⃣ The key idea

These two things are **independent**.

You can have:

working directory = projectA  
environment = env1

or

working directory = projectB  
environment = env1

or

working directory = projectA  
environment = env2

---

# 4️⃣ Visual example

Suppose your computer looks like this:

projects/  
   projectA/  
      main.py  
   projectB/  
      train.py

And your conda environments:

anaconda3/envs/  
   envA  
   envB

You could run:

cd projectA  
conda activate envB  
python main.py

Meaning:

files come from → projectA  
python interpreter comes from → envB

---

# 5️⃣ Why environments exist

Without environments, all packages install globally:

system python  
 ├── numpy 1.24  
 ├── torch 2.0  
 ├── pandas

Then another project requires:

numpy 1.20

Now everything breaks.

Environments isolate dependencies:

envA  
 ├── numpy 1.20  
  
envB  
 ├── numpy 1.26

---

# 6️⃣ Mental model

Think of it like this:

Working directory → which project you're in  
Environment → which toolbox you're using

Example analogy:

Project folder = construction site  
Environment = toolbox

You can bring **different toolboxes to the same construction site**.