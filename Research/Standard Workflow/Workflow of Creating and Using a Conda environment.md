---
Date: 2026-03-16
---

# 1️⃣ Create the environment

First create a new environment with a specific Python version.

conda create -n myenv python=3.10

Explanation:

- `conda create` → create environment
    
- `-n myenv` → environment name
    
- `python=3.10` → install Python version
    

Example output conceptually:

myenv  
 ├── python 3.10  
 ├── pip  
 └── basic libraries

# 2️⃣ Activate the environment

conda activate myenv

Your terminal will change to something like:

(myenv) user@computer %

Now **everything you install goes into this environment**.

---

# 3️⃣ Install packages

Prefer installing with **conda first**, especially for scientific libraries.

Example:

conda install numpy pandas matplotlib

Conda installs:

numpy  
+ BLAS  
+ LAPACK  
+ compiled binaries

This prevents the **“failed building wheel”** problem.

---

# 4️⃣ Install packages with pip (if needed)

Some packages exist only on PyPI.

Then you can still use pip **inside the conda environment**:

pip install transformers

Rule many researchers follow:

conda install → first  
pip install → only if necessary

---

# 5️⃣ Verify environment packages

conda list

Example output:

numpy  
pandas  
python  
scipy  
pip

---

# 6️⃣ Deactivate environment

When you're done:

conda deactivate

---

# 7️⃣ Remove environment (optional)

conda remove -n myenv --all

---

# 8️⃣ Typical **ML / research project workflow**

When starting a project (like reproducing a paper):

### Step 1 — create project folder

mkdir project  
cd project

---

### Step 2 — create environment

conda create -n project_env python=3.10

---

### Step 3 — activate

conda activate project_env

---

### Step 4 — install dependencies

Example:

conda install pytorch torchvision -c pytorch  
pip install transformers datasets

---

### Step 5 — run code

python main.py

---

# 9️⃣ Visual structure

Your system becomes something like:

anaconda3/  
   envs/  
      project_env/  
         bin/python  
         lib/python3.10  
         numpy  
         pandas

Your **code project is separate**:

project/  
   main.py  
   train.py  
   dataset/

Environment ≠ project folder  
They are **two different things**.

---

✅ **Simple mental model**

Project folder = your code  
Conda environment = tools used to run the code

Like:

Recipe = project  
Kitchen = environment

---

💡 Since you were earlier asking about **reproducing research projects**, the **standard workflow researchers actually use** is:

git clone repo  
conda create -n env python=3.x  
conda activate env  
pip install -r requirements.txt  
python main.py

---

If you'd like, I can also show you something extremely useful:

**the “golden workflow” researchers use to reproduce ML projects without dependency hell (conda + pip + requirements + environment.yml).**

It will save you **hours when reproducing papers.**