# Git/GitHub Workshop: A Step by Step Guide


Fell behind during the live demo? No worries! Follow the steps here at your own pace. If you get stuck, raise your hand and a board member will help you!


## Before the Workshop
If you haven't done these yet, do it now:
1. **Make a [GitHub](https://github.com) account** (if you don't have one already, otherwise you're good!)
2. **Fork the workshop repository** -> open this [link](https://github.com/nlacan/acm-git-workshop/tree/main) and click on **Fork** at the top right. GitHub will redirect you to your own copy of the repo at `github.com/your-username/acm-git-workshop`


## Workshop Day Setup
1. Open Visual Studio Code on your lab computer
2. At the top right, click **Sign In** and login with your GitHub account
3. Make sure you have VSCode's integrated terminal open. It should say `PS C:\Users\your-user ` in your terminal at the bottom! If you don't see a terminal, you can open one using `` Ctrl + Shift + ` ``

If you decided to bring your own machine, please use Visual Studio Code's terminal! It keeps things consistent and will allow helpers to troubleshoot faster.


## Demo Start!

### Step 1: Clone the Forked Repository
On your forked repository on the GitHub website, press the green Code button and copy the URL. Make sure you are copying the forked repository's URL, not the original repository's! The URL should have your GitHub username. 

Then, run the following commands in the terminal:

    git clone [paste the URL here]    // makes a copy of the remote repo
    cd acm-git-workshop               // change to the newly made repo folder
    code .                            // opens new VSCode window with repo

---

### Step 2: Commit a New File (No Merge Conflicts)
You will now make your first commit! Note that right now, we are on the `main` branch.

Let's first create a new file. Right click on the empty space on the left, and create a new file called `newFile.txt`. Leave it empty or type anything in it!

Then, run the following commands in the terminal:

    git add newFile.txt                     // stages your changes
    git commit -m "committing newFile.txt"   // saves local snapshot of changes
    git push                                // uploads to remote repo

Note: It might prompt you to login back again.

If you go back to the repository on the GitHub website, you should be able to see your changes!

---

### Step 3: Create and Work on a Branch
It is best practice to create your own branch to work on your own code independently. Any changes you make to your new branch will not affect `main`. Run the following commands in the terminal to branch off `main` and to see what branch you are at:

    git checkout -b my-branch     // creates a new branch called my-branch
    git branch                    // current local branches

When you run `git branch`, you should see an asterisk (*) next to `my-branch`. The asterisk indicates your current branch!

Now, let's edit the file called `editme.txt`. Answer the question in the file, and commit your changes using the following commands. **Important: do *not* push!** Since we have not pushed, your changes stay on your local machine.

    git add editme.txt
    git commit -m "committing editme.txt"

---

### Step 4: Simulate a Merge Conflict
Usually, `main` might have new commits from a teammate who merged their new code while you were working on your branch. This can lead to something called a **merge conflict**.

A **merge conflict** occurs when a teammate changed the same exact line of code you did. Git does not know which one to keep, so you need to resolve it before pushing!

Since you are working solo today, we need to simulate a merge conflict. Switch to `main` using the command:

    git checkout main

Edit `editme.txt` again but with a **different** answer. This simulates a teammate who pushed different code to `main`!

Push these changes to the remote repository:

    git add editme.txt
    git commit -m "simulate merge conflict"
    git push

Return back to your branch:

    git checkout my-branch

Now, run the following command to merge `main` into `my-branch`:

    git merge main

You will get a warning in your terminal that says the merge failed! That is because `main` has newly updated code that differs from what you have in your branch and Git doesn't know which one to choose. Don't panic, we will resolve this in the next step!

---

### Step 5: Resolve the Merge Conflict
Open `editme.txt`. You'll see something like this:

    <<<<<<< HEAD
    your answer
    =======
    main's answer
    >>>>>>> main

Everything between `<<<<<<< HEAD` and `=======` is what's on **your branch**. Everything between `=======` and `>>>>>>> main` is what's on **main**.

Edit the file by hand to fix it. Delete the `<<<<<<<`, `=======`, and `>>>>>>>` lines, and keep whichever answer you want (or combine both)! Then run:

    git add editme.txt
    git commit -m "resolve merge conflict"

---

### Step 6: Push Your Resolved Branch to Remote

    git push -u origin my-branch     // -u sets up tracking so future pushes are just "git push"

---

### Step 7: Open a Pull Request

A **pull request** is a proposal to submit changes to a repository. Typically, your teammates can look over your pull request to review your code. This is best practice to avoid merging changes that break your code!

To open a pull request:
1. Go to your forked repository on the GitHub website
2. You should see a banner prompting you to open a Pull Request for `my-branch`. Click it! (Or go to the **Pull Requests** tab and click **New Pull Request**)
3. Make sure it's set to merge `my-branch` into `main`
4. Click **Create Pull Request**, then **Merge Pull Request**

---

### Step 8: Pull the Merge Down Locally
Your local `main` doesn't know about the merge you just did on GitHub yet! Let's sync up your local `main` to the remote one:

    git checkout main
    git pull                    // downloads and merges changes from remote

This is a step you'll do often on a real team. Anytime someone else's pull request gets merged, you `pull` to bring those changes into your own local repository!

---

### You're done!
You just went through the full loop: clone repository → make a feature branch → commit changes → likely merge conflict → resolve → PR → pull. This is genuinely most of what you'll use day-to-day working on a team!
