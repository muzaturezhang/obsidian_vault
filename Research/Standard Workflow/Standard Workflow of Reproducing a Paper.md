---
Date: 2026-03-16
---

# 1️⃣ Create the project folder

First create a folder for the project.

In terminal:

mkdir cnn-cifar10-baseline  
cd cnn-cifar10-baseline

Now your project root is:

cnn-cifar10-baseline/

---

# 2️⃣ Create a Python environment

You should **always isolate environments**.

Two common tools:

- `venv`
    
- `conda`
    

### Using venv (simple)

python3 -m venv venv

Activate it:

Mac/Linux

source venv/bin/activate

Windows

venv\Scripts\activate

Now your terminal shows something like:

(venv) user@computer

Meaning the environment is active.

### Using conda

 [[Workflow of Creating and Using a Conda environment]]

---

# 3️⃣ Install required packages

For a CNN project you usually install:

pip install torch torchvision matplotlib numpy

Later you can save them:

```shell
pip freeze > requirements.txt
```

This file records all packages.

---

# 4️⃣ Open the project in VSCode

Open VSCode:

File → Open Folder

Select

cnn-cifar10-baseline

Inside VSCode choose the Python interpreter:

Command Palette → Python: Select Interpreter

Choose

venv/bin/python

---

# 5️⃣ Create basic project files

Typical ML structure:

cnn-cifar10-baseline  
│  
├── main.py  
├── model.py  
├── train.py  
├── dataset.py  
├── requirements.txt  
└── README.md

Simplest starting point:

main.py  
model.py  
train.py

---

# 6️⃣ Get the dataset

For **MNIST / CIFAR10** you usually **do NOT download manually**.

PyTorch downloads automatically.

Example:

from torchvision import datasets, transforms  
  
trainset = datasets.CIFAR10(  
    root="./data",  
    train=True,  
    download=True,  
    transform=transforms.ToTensor()  
)

When you run the program it downloads:

cnn-cifar10-baseline  
   data/  
       cifar-10-batches-py

---

# 7️⃣ Implement the baseline model

In `model.py`:

Example CNN:

import torch.nn as nn  
  
class CNN(nn.Module):  
    def __init__(self):  
        super().__init__()  
  
        self.conv = nn.Sequential(  
            nn.Conv2d(3, 32, 3),  
            nn.ReLU(),  
            nn.MaxPool2d(2)  
        )  
  
        self.fc = nn.Linear(32*15*15, 10)  
  
    def forward(self, x):  
        x = self.conv(x)  
        x = x.view(x.size(0), -1)  
        x = self.fc(x)  
        return x

---

# 8️⃣ Run the program

From terminal:

python main.py

If the model trains successfully:

✔ dataset loads  
✔ model trains  
✔ loss decreases

You have **跑通 baseline**.

---

# 9️⃣ Initialize Git

Inside project:

git init

Add files:

git add .  
git commit -m "initial cnn cifar10 baseline"

---

# 🔟 Push to GitHub

Create repo on GitHub:

cnn-cifar10-baseline

Then:

git remote add origin https://github.com/yourname/cnn-cifar10-baseline.git  
git branch -M main  
git push -u origin main

---

# 🧠 What “reproducing a paper” actually means

Typical research pipeline:

1 read paper  
2 find code (GitHub usually)  
3 set up environment  
4 run baseline  
5 verify results  
6 modify experiment  
7 analyze results