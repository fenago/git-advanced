
Mastering Git Stash Workflow
============================

Git is a powerful tool that makes up for a lot of use cases on our
development workflow. One such case is to isolate the changes of a
certain branch to itself. Let me elaborate.

Suppose you are working on a branch called `admin-dashboard`
implementing ,well, an administrative dashboard. But you are not done
yet, and the project manager wants a quickfix for the login
implementation. Now you want to switch to the `login` branch and fix the
issue but don't want to carry the changes you are doing on the
`admin-dashboard` branch. Well this is where git stash comes in.

### **Git stash what?**

Git stash allows you to quickly put aside your modified changes to a
LIFO (Last In First Out) stack and re-apply them when feasible. We will
be doing a rough walkthrough to see this in action.

**Git stash walkthrough**
---------------------------

Initiate git on an empty directory. Add a file named `add.py` and put
the following code.


``` 
# add.py 

def add(a, b):
    return a + b
```


Let's add the file to git and commit it .


``` 
git add add.py && git commit -m "Add function"
```


Next let's create and checkout to a new branch called `mul` and create a
file called `mul.py`\


``` 
git checkout -b mul
```


Add the following code to the file.


``` 
# mul.py 

def mul(a, b): 
    return a * b
```


Add the file to git and commit it.


``` 
git add mul && git commit -m "Mul function"
```


Now suppose, we need to update the mul function to take in a third
argument and you just edited the function like so:\


``` 
# mul.py

def mul(a, b, c): 
    return a * b 
```


Take note that, we still haven't updated the return value with `c`.
While we were making our changes, the project manager called-in to
update the `add` function immediately with a third argument. Now you
can't waste a second on the `mul` function which you haven't completed.
**What are you going to do?**

If you try to checkout to master where add function resides, git won't
let you because you have unfinished changes that hasn't been committed.



### **Stashing Changes** 

Well this is the situation you should be using the `git stash` command.
We want to put away the changes on our current branch so that we can
come back to it later.

Stash the file with a message on the `mul` branch.


``` 
git stash save "Multiply function"
```


Now if you `git status`, the working directory will be clean and you can
jump into the master branch for the changes. We can view the items in
our stash using `git stash list`. We can view the diff of the items on
our stack using `git stash show`



Now you are in `master` branch modifying the `add` function, and comes
an even higher priority job to include a `subtraction` function.

> **Note**:\
> Project Managers in real life doesn't put forward tasks on this
> manner.

Your `add` function looks pretty much like the `mul` function now.


``` 
# add.py 

def add(a, b, c): 
    return a + b   # couldn't include `c` due to a priority task.
```


Stash it with a message.


``` 
git stash save "Add function third argument"
```



Now let's suppose we have completed our task for `subtraction` branch
and we want to continue working on other branches.

Let's move to the `master` branch first to complete our changes for
addition.

There are two ways we can re-apply those changes:

1.  `git stash pop`\
    applies the top most change stored on the stack and removes it from
    the stack.

2.  `git stash apply <item-id>`\
    applies the stash based on the index provided, keeps the applied
    item intact on the stack.

### **Popping stashed changes** 🍾

Like I mentioned earlier, stash follows the LIFO convention. The latest
item we save are always on the top. And when we use `pop`, always the
top most change is applied to the current branch. Run the following
command on `master`.


``` {.highlight .plaintext}
git stash pop
```



Complete the `add` function and commit it.

### **Applying stashed changes** 📥

Next, checkout `mul` branch. We can use `pop` here as well since there
is only one item remaining on the stack. But let's see how
`git stash apply` works.


``` 
git stash apply stash@{0}
```



When we apply from the stash, the item still remains on the stack.
Complete the changes here and commit it.

### **Create a new branch with stashed changes**

Let's do something fun. Let's say we want to add a `divide` function on
a new branch. Well it is kind of similar to our `multiple` function so
why not utilize the item in stash and create a `divide` function with
it?

We can do that with the `git stash branch` command. It takes the
`<item-id>` and a branch name, then ***applies*** those changes to that
branch.


``` 
git stash branch <branch-name> <item-id>

git stash branch divide stash@{0}
```

Now we can rename the file and change the function to perform division.

### Viewing the stashed changes

Sometimes we tend to forget what changes we stashed. What we forget can
range from which files were stashed to what changes on the files were
stashed.

To view a list of files that were stashed, we can run:\


``` 
# EXAMPLE:
# git stash show stash@{<stash-id>}

git stash show stash@{2}
```


To get a diff view of changes on the files that were stashed, we can
run:\


``` 
# EXAMPLE:
# git stash show -p stash@{<stash-id>}

git stash show -p stash@{2}
```


### **Clearing the stack** 🧹

Now that the stash has served its purpose, we can clear it. There is
again two ways of doing it:

1.  `git stash clear`
    wipes the whole stack clean.

2.  `git stash drop <item-id>`
    removes the item from stack based on provided id.


Managing Git Worktree
=====================


Git worktree helps you manage multiple working trees attached to the
same repository.

> In short, you can check out multiple branches at the same time by
> maintaining multiple clones of the same repository.

OK back to our problem! Update changes? New Feature? Hot Fix? Whatever
it is, you need to change to a different branch and work on it without
any changes to your current work directory.

Let's say it's a new feature, your workflow would look like this:

1.  create an replica of your project and switch to a new branch
2.  create a new feature
3.  push it
4.  back to previous working directory

### Create worktree

Let's say the name of your feature is `feature-x` and you want the
branch with the same name. You can create additional worktree on the
same directory or move it to a desired path, I prefer the later.

`git worktree add` command creates a worktree along with a branch that
is named after the final word in your path.


``` 
git worktree add <PATH>

# Create feature-x directory and branch with the same name.
git worktree add ../feature-x
```


### Named Branch

If you want to give you branch a unique name then you can use the `-b`
flag with the `add` command.


``` 
git worktree add -b feature-xyz ../feature-xyz
```


### List Worktrees

View the list of worktrees with `git worktree list`


### Remove Worktrees

Now that you have created a new worktree, switched to it and made your
changes and pushed it. To remove the worktree, we can run:


``` 
git worktree remove <name-of-worktree>

git worktree remove feature-x
```


### Conclusion

Git worktree is a handy feature that let\'s you context switch in your
project to try out things on a completely different environment, without
modifying your main work directory.