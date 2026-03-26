---
Date: 2026-03-18
---
What you’re seeing is actually a **classic Python behavior issue**, not a PyTorch problem.

---

## 🧠 What’s happening

When you run:

```bash
python model_test.py
```

and the output is:

```
PyTorch version: 2.10.0
torchvision version: 0.25.0
```

👉 That means **those print statements are being executed somewhere automatically during import**.

Most likely:

### 🔍 Your `model.py` or `dataset.py` contains something like:

```python
print("PyTorch version:", torch.__version__)
print("torchvision version:", torchvision.__version__)
```

So when you do:

```python
from model import FashionMNISTModelV0
```

Python **executes the entire file (`model.py`) once**, including those print statements.

---

## 🚨 Key Concept (VERY important)

### 👉 Import ≠ just “getting a class”

It actually means:

> **Run the whole file, then extract the requested objects**

---

## ✅ Why your model isn’t printing

You expected:

```python
print(model_0)
```

But you **never actually printed it**.

Python doesn’t automatically display objects like Jupyter Notebook does.

---

## ✅ Fix

Just add:

```python
print(model_0)
```

at the end of your script.

---

## ✅ Clean Fix for the version printing issue

In `model.py` (or wherever you wrote those prints), change this:

```python
print("PyTorch version:", torch.__version__)
print("torchvision version:", torchvision.__version__)
```

to:

```python
if __name__ == "__main__":
    print("PyTorch version:", torch.__version__)
    print("torchvision version:", torchvision.__version__)
```

---

## 🧠 Why this works

This line:

```python
if __name__ == "__main__":
```

means:

|Situation|`__name__` value|
|---|---|
|Run file directly|`"__main__"` ✅|
|Imported as module|`"model"` ❌|

So:

- Running `python model.py` → prints versions ✅
    
- Importing `model` → **no prints** ✅
    

---

## 🧠 Thinking Model (this is the real takeaway)

Whenever you see “weird output”:

### Step 1: Ask

> Where could this print come from?

### Step 2: Check imports

- Python executes imported files
    

### Step 3: Separate concerns

- “definition code” (classes, functions)
    
- vs “execution/debug code” (prints, tests)
    

---

## 💡 Pro-level structure (what you’re approaching)

Every file should look like:

```python
# definitions (safe to import)
class MyModel: ...
def helper(): ...

# testing / debugging
if __name__ == "__main__":
    # only runs when file is executed directly
```

---
## Which kind of code should be put under __main__

Top-level code → definitions (always loaded)
↓
__main__ block → execution (only when run directly)


---

If you want, I can next show you a **clean PyTorch project template (train/test split + dataset + model + config)** — that will eliminate these issues permanently and match real research workflows.
