# Another important thing: **DO NOT upload datasets**

GitHub is **not for datasets**.

Bad:

datasets/  
   cifar10/

Good:

cnn-cifar10  
   train.py  
   model.py  
   README.md

In README:

Dataset: CIFAR10  
Download automatically using torchvision

Example code:

from torchvision import datasets  
  
trainset = datasets.CIFAR10(  
    root='./data',  
    train=True,  
    download=True  
)

---

# 5️⃣ A clean GitHub example structure

Your repo:

ml-research-practice

ml-research-practice  
│  
├── cnn-cifar10-baseline  
├── fgsm-adversarial-attack  
├── lime-explanation  
├── notes  
│   └── trustworthy_ai_notes.md  
└── README.md

This looks **very clean for recruiters / professors**.

---

# 6️⃣ Your first 3 projects (perfect for you)

Since you want **Trustworthy AI**, start with:

ml-practice  
│  
├── cnn-cifar10-baseline  
├── fgsm-adversarial-attack  
└── lime-explanation

These correspond exactly to:

1️⃣ baseline model  
2️⃣ adversarial robustness  
3️⃣ explainability

Which are **core topics of trustworthy AI**.

---

# 7️⃣ Small professional tip

Name folders like this:

cnn-cifar10-baseline  
fgsm-adversarial-attack  
lime-explanation

Use **kebab-case** (hyphen style).

This is standard in ML repos.

---

✅ If you want, I can also show you:

**The exact step-by-step workflow researchers use to**

train model  
save checkpoint  
log experiment  
push to GitHub

It will make your **first ML repo look like a real research repo instead of homework**.