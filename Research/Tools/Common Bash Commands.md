# 1. Navigation Commands (move around the filesystem)

### `pwd`

**Definition:**  
Print the current working directory (shows where you are).

Example:
```bash
pwd
```


Output example:

`/Users/yourname/projects`

---

### `ls`

**Definition:**  
List the files and folders in the current directory.

Example:

`ls`

Useful variants:

ls -l

Detailed list (permissions, size, date)

ls -a

Show hidden files

---

### `cd`

**Definition:**  
Change the current directory.

Example:

cd project_folder

Go up one level:

```shell
cd ..
```


Go to home directory:

```shell
cd ~
```


---

# 2. File and Folder Management

### `mkdir`

**Definition:**  
Create a new directory.

Example:

```bash
mkdir my_project
```



### Create multiple nested folders (very useful)

Use `-p`.

mkdir -p blogs/drafts

Result:

blogs  
   drafts

You can even do:

mkdir -p research/blogs/drafts

Result:

research  
   blogs  
      drafts
      
---

### `touch`

**Definition:**  
Create an empty file.

Example:

```bash
touch train.py
```

---

### `cp`

**Definition:**  
Copy files or directories.

Example:

cp file.txt backup.txt

Copy a directory:

cp -r folder1 folder2

---

### `mv`

**Definition:**  
Move or rename files.

Rename:

mv oldname.py newname.py

Move file:

mv file.py src/

---

### `rm`

**Definition:**  
Remove files or directories.

Delete file:

rm file.txt

Delete directory:

rm -r folder

⚠️ Dangerous command (no undo)

---

# 3. Viewing File Content

### `cat`

**Definition:**  
Print the entire file content.

Example:

cat README.md

---

### `less`

**Definition:**  
View large files page-by-page.

Example:

less large_log.txt

Navigation inside:

space → next page  
q → quit

---

### `head`

**Definition:**  
Show the first lines of a file.

Example:

head file.txt

---

### `tail`

**Definition:**  
Show the last lines of a file.

Example:

tail file.txt

Useful for logs:

tail -f log.txt

---

# 4. Python / Environment Commands

### `python`

Run a Python script.

Example:

python train.py

---

### `pip`

Install Python packages.

Example:

pip install torch

Upgrade package:

pip install --upgrade numpy

List installed packages:

pip list

Save dependencies:

pip freeze > requirements.txt

---

### `python -m venv`

Create a virtual environment.

Example:

python -m venv venv

Activate environment (Mac/Linux):

source venv/bin/activate

Deactivate:

deactivate

---

# 5. Git Commands (very important)

Used with Git and GitHub.

---

### `git init`

Create a Git repository.

git init

---

### `git status`

Check repository state.

git status

---

### `git add`

Add files to staging area.

git add train.py

Add everything:

git add .

---

### `git commit`

Save a snapshot.

git commit -m "initial commit"

---

### `git clone`

Download a repository.

git clone https://github.com/user/repo.git

---

### `git pull`

Update local repository.

git pull

---

### `git push`

Upload changes.

git push

---

# 6. System / Utility Commands

### `clear`

Clear the terminal screen.

clear

---

### `history`

Show command history.

history

---

### `echo`

Print text.

Example:

```
echo "Hello"
```

Also used to write files:

echo "test" > file.txt

---

# 7. Useful Keyboard Shortcuts

| Shortcut   | Meaning          |
| ---------- | ---------------- |
| `Ctrl + C` | stop program     |
| `Ctrl + L` | clear terminal   |
| `↑`        | previous command |
| `Tab`      | auto-complete    |

---

# 8. The Typical ML Workflow in Terminal

A real workflow often looks like:

mkdir project  
cd project  
  
python -m venv venv  
source venv/bin/activate  
  
pip install torch torchvision  
  
touch train.py  
  
git init  
git add .  
git commit -m "initial commit"

---

✅ **Most important commands to memorize first**

pwd  
ls  
cd  
mkdir  
touch  
rm  
python  
pip  
git

These alone cover **80% of daily terminal usage**.