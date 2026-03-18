---
Date: 2026-03-18
---
This is a **very good question**, because it touches a key idea in structuring ML projects:  
👉 _how different modules (model / dataset / training script) share information cleanly._

---

## 🧠 Core Issue

Right now:

- `class_names` is defined inside `dataset.py`
    
- You are trying to use it in your training/testing script
    

So the real question is:

> ❓ _How do I access variables defined in another file?_

---

## ✅ Solution 1 (Most standard): Import it explicitly

If in your `dataset.py` you have something like:

```python
class_names = ["T-shirt", "Trouser", "Pullover", ...]
```

Then in your main file:

```python
from dataset import FashionMNISTDataset, class_names
```

Now you can directly use:

```python
len(class_names)
```

✔️ This is the **simplest and most common approach**

---

## ✅ Solution 2 (Better design): Put it inside the Dataset class

A more **modular and scalable** way:

### In `dataset.py`

```python
class FashionMNISTDataset:
    def __init__(self):
        self.class_names = ["T-shirt", "Trouser", "Pullover", ...]
```

### In your main file:

```python
dataset = FashionMNISTDataset()
class_names = dataset.class_names

model_0 = FashionMNISTModelV0(
    input_shape=784,
    hidden_units=10,
    output_shape=len(class_names)
)
```

✔️ This is **better design** because:

- Data-related info stays with the dataset
    
- Avoids global variables
    
- Easier to extend later (e.g., multiple datasets)
    

---

## ✅ Solution 3 (Even cleaner for research projects)

If you want **clean architecture (very important for your future projects)**:

Create a separate config file:

### `config.py`

```python
CLASS_NAMES = ["T-shirt", "Trouser", ...]
```

### Then:

```python
from config import CLASS_NAMES

len(CLASS_NAMES)
```

✔️ This is useful when:

- Multiple modules need the same constants
    
- You scale to bigger projects
    

---

## 🚨 Common Beginner Mistake (what to avoid)

Don't do this:

```python
import dataset
dataset.class_names  # ❌ fragile if not defined globally
```

It _can_ work, but:

- Breaks easily if structure changes
    
- Not explicit
    

---

## 🧠 Thinking Model (important for you)

When you face this type of problem, think in layers:

### 1. **Where does this data belong?**

- class_names → dataset domain
    

### 2. **Who needs it?**

- model (output size)
    
- evaluation (label decoding)
    

### 3. **How should it flow?**

- Explicit import ✅
    
- Or pass via object ✅
    
- Avoid hidden/global coupling ❌
    

---

## 💡 My Recommendation for You

Since you're moving toward **research + reproducible pipelines**, go with:

👉 **Solution 2 (Dataset class attribute)**

It will align perfectly with:

- PyTorch `Dataset` design
    
- future `DataLoader`
    
- cleaner pipelines
    

---

If you want, next step I can help you refactor your whole project into a **research-grade structure (train.py / dataset.py / model.py / config.py)** — that’s a _huge upgrade_ for your current level.