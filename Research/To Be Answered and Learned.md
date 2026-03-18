---
Date: 2026-03-17
---
What does plt.show() mean and function?
[[plt.show()]]

what is `__init__` mean

wha's the scope of `from xxx import xxx`
(eg. If I could only write from model import xxx only if it's in the same directory with me (But the torch package in the env aren't in the same directory) )

So the global variables could also be imported to other files like a module? And what is global variable, and the class, function, module itself can also be imported?

Why the imported class is dark except I use it in the program

What shortcut should I enter if I want to see the underlying program of a library/module?

Learn and practice how to identify the scope /domain of a variable/class... (for better importing)

What's the import in essence

# Consider how to organize a project from scratch(the structure)

Can I find exactly where the specific function/variable appears in a file exists in ? (Through searching, not to examining one by one)

---

Do I have to  
from dataset import FashionMNISTDataset

from model import FashionMNISTModelV0

dataset=...
model=...

do this process in each file like train.py and predict.py...?

---
	I'd be better write the`if __name__=="__main__"` in front of every file?

What's the differences between modules, class, attributes, variables and their relationship, inclusion