---
Date: 2026-03-19
---
# ✅ 1. Will `"model_1.pth"` be overwritten?

## 👉 Short answer: **YES**

torch.save(model_1.state_dict(), "model_1.pth")

➡️ If `model_1.pth` already exists:

> ❗ It will be **silently overwritten**

---

## 🧠 Why?

- `torch.save()` just writes to a file
    
- It behaves like normal file writing (`open(..., "wb")`)
    

---

## ✅ How to avoid overwriting

### ✔️ Option 1: Add timestamp (most common)

import time  
  
filename = f"model_{int(time.time())}.pth"  
torch.save(model.state_dict(), filename)

---

### ✔️ Option 2: Save best model only (recommended 🔥)

best_acc = 0  
  
if test_acc > best_acc:  
    best_acc = test_acc  
    torch.save(model.state_dict(), "best_model.pth")

👉 This is **standard practice in ML**

---

### ✔️ Option 3: Use epoch naming

torch.save(model.state_dict(), f"model_epoch_{epoch}.pth")

---

## 🧠 Best practice (what you should do)

best_model.pth      ← final best  
last_model.pth      ← last epoch