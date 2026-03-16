# 3️⃣ `$`

The `$` tells the shell:

> "substitute the value of this variable".

So:

$HOME

means:

the value stored in the variable HOME

Without `$`, the shell treats it as plain text.

Example:

echo HOME

Output:

HOME

But:

echo $HOME

Output:

/Users/alex

because the shell replaces the variable with its value.

# `HOME`

`HOME` is an **environment variable**.

It stores the **path of your home directory**.

Example values:

Linux / Mac:

HOME=/home/alex

or

HOME=/Users/alex

You can check it with:

echo $HOME

Example output:

/Users/alex

That means your personal folder is:

/Users/alex