---
Date: 2026-03-16
---
Here are the **most commonly used `conda` commands**. I’ll organize them into a **typical workflow**, because that’s how you’ll actually use them in practice. 🧑‍💻

---

# 1️⃣ Creating environments

Create a new environment:

```bash
conda create -n myenv python=3.10
```

Meaning:

- `create` → create environment
    
- `-n myenv` → environment name
    
- `python=3.10` → Python version
    

You can also install packages during creation:

```bash
conda create -n ml_env python=3.10 numpy pandas matplotlib
```

---

# 2️⃣ Activate / deactivate environments

Activate:

```bash
conda activate myenv
```

Deactivate:

```bash
conda deactivate
```

Your terminal will show something like:

```
(myenv) user@computer %
```

---

# 3️⃣ Listing environments

Show all environments:

```bash
conda env list
```

or

```bash
conda info --envs
```

Example output:

```
base        *  /Users/you/anaconda3
myenv          /Users/you/anaconda3/envs/myenv
ml_env         /Users/you/anaconda3/envs/ml_env
```

`*` means the **current active environment**.

---

# 4️⃣ Installing packages

Install packages inside the environment:

```bash
conda install numpy
```

Install multiple packages:

```bash
conda install numpy pandas scipy
```

Install from a specific **channel**:

```bash
conda install pytorch -c pytorch
```

Channel = repository for packages.

Common channels:

- `defaults`
    
- `conda-forge`
    
- `pytorch`
    

---

# 5️⃣ Listing installed packages

```bash
conda list
```

Shows everything installed in the current environment.

---

# 6️⃣ Updating packages

Update a specific package:

```bash
conda update numpy
```

Update conda itself:

```bash
conda update conda
```

Update everything in the environment:

```bash
conda update --all
```

---

# 7️⃣ Removing packages

Remove a package:

```bash
conda remove numpy
```

Remove multiple:

```bash
conda remove numpy pandas
```

---

# 8️⃣ Deleting environments

Delete an entire environment:

```bash
conda remove -n myenv --all
```

This removes:

```
python
all installed packages
environment folder
```

---

# 9️⃣ Exporting environments (important for research)

Export environment configuration:

```bash
conda env export > environment.yml
```

This saves all packages and versions.

Example:

```
name: myenv
dependencies:
  - python=3.10
  - numpy
  - pandas
  - pytorch
```

---

# 🔟 Recreating environments

Someone else can recreate your environment:

```bash
conda env create -f environment.yml
```

This is **very common in GitHub projects**.

---

# 1️⃣1️⃣ Searching packages

Search for packages:

```bash
conda search numpy
```

---

# 1️⃣2️⃣ Cleaning cache (optional)

Conda caches downloaded packages.

Clean them:

```bash
conda clean --all
```

---

# 🧠 Minimal commands you should memorize

In practice you only need about **7 commands**:

```bash
conda create -n env python=3.10
conda activate env
conda install package
conda list
conda deactivate
conda env list
conda remove -n env --all
```

---

💡 Since you were earlier asking about **project workflows and reproducing research code**, the **real pipeline researchers follow** is usually:

```bash
git clone project_repo
cd project_repo

conda create -n project_env python=3.10
conda activate project_env

pip install -r requirements.txt
python main.py
```

Understanding this pipeline will make **90% of ML GitHub repositories immediately understandable**.

---

If you'd like, I can also show you something extremely useful:

**the difference between `conda install` and `pip install` inside a conda environment (and when mixing them breaks environments).**

This is something many beginners learn the hard way.