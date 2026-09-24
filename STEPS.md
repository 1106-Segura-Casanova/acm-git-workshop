# Git/GitHub Workshop: A Step by Step Guide


Fell behind during the live demo? No worries! Follow the steps here at your own pace. If you get stuck, raise your hand and a board member will help you!


## Setup
1. If you don't already have one, create a **[GitHub](https://github.com)** account. Then, make sure you're signed in.
2. Open this [link](https://github.com/nlacan/acm-git-workshop/tree/main) and click **Fork** at the top right. GitHub will redirect you to your own copy of the repo at `github.com/your-username/acm-git-workshop`
3. Open Visual Studio Code on your lab computer, click **Sign In** at the top right, and login with your GitHub account
4. Make sure you have VS Code's integrated terminal open. It should say `PS C:\Users\your-user` at the bottom! If you don't see a terminal, you can open one using `` Ctrl + Shift + ` ``

If you decided to bring your own machine, please use Visual Studio Code's terminal! It keeps things consistent and will allow helpers to troubleshoot faster. However, we do recommend using the lab computers as the workshop material is made based on those rather than personal machines.


## Demo Start!

### Step 1: Clone the Forked Repository
**What is cloning?** Cloning downloads a copy of a remote repository (from GitHub) onto your own machine, so you can work on the code locally.

On your forked repository on the GitHub website, press the green Code button and copy the URL. Make sure you are copying the forked repository's URL, not the original repository's! The URL should have your GitHub username. 

Then, run the following commands in the terminal:

    git clone [paste the URL here]    // makes a copy of the remote repo
    cd acm-git-workshop               // change to the newly made repo folder
    code .                            // opens new VSCode window with repo

---

### Step 2: Commit a New File (No Merge Conflicts)
**What is a commit?** A commit is a snapshot of your current changes to your local project history, along with a message describing what changed. Think of it as a save point you can always come back to.

You will now make your first commit! Note that right now, we are on the `main` branch. `main` is where the shared team code lives.

Let's first create a new file. Right click on the empty space on the left, and create a new file called `newFile.txt`. Leave it empty or type anything in it! Make sure to save your changes with `Ctrl + S`.

Then, run the following commands in the terminal:

    git add newFile.txt                     // stages your changes, kind of like a pre-commit
    git commit -m "add newFile.txt"         // saves local snapshot of changes
    git push                                // uploads your commit to remote repo

Note: It might prompt you to login back again. If it does, choose the sign in with browser option.

If you go back to the repository on the GitHub website, you should be able to see your new file in there!

---

### Step 3: Create and Work on a Feature Branch
**What is branching?** Branching creates a separate, independent copy of your code where you can make changes without affecting the `main` branch. This is how teams work on multiple features at once without stepping on each other's work.

It is best practice to create your own "feature branch" every time you start a new feature. Run the following commands in the terminal to branch off `main` and to see what branch you are at:

    git checkout -b my-branch     // creates a new branch called my-branch
    git branch                    // shows current local branches

When you run `git branch`, you should see an asterisk (*) next to `my-branch`. The asterisk indicates your current branch!

Now, let's edit the file called `editme.txt`. Answer the question in the file, and commit your changes using the following commands. Remember your answer! **Important: do *not* push!** Since we have not pushed, your changes stay on your local machine.

    git add editme.txt
    git commit -m "modify editme.txt"

---

### Step 4: Simulate a Merge Conflict
Usually, the `main` branch might have new commits from a teammate who merged their new code while you were working on your branch. This can lead to something called a **merge conflict**.

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

💡 Bonus tip: VS Code also shows clickable buttons right above the conflict markers: Accept Current Change, Accept Incoming Change, or Accept Both Changes. They do this resolution for you automatically. It's good to understand how to resolve conflicts by hand first (like we just did!), but once you're comfortable, these buttons are usually the faster way to do it day-to-day.

---

### Step 6: Push Your Resolved Branch to Remote

    git push -u origin my-branch     // -u sets up tracking so future pushes are just "git push"

---

### Step 7: Open a Pull Request

A **pull request** is a proposal to submit changes to a repository. Typically, your teammates can look over your pull request to review your code. This is best practice to avoid merging changes that break your code!

To open a pull request:
1. Go to your forked repository on the GitHub website
2. Click **Pull requests**, then **New pull request**
3. Change the base repository to your forked repository. It should say `base repository: your-username/acm-git-workshop`.
4. It should redirect you to a **Comparing changes** page. In that page, change `compare: main` to `compare: my-branch`.
5. Click **Create pull request**
6. Optionally, add a title and description. It is good to include them! However, for now you can just press **Create pull request**
7. It should redirect you to the pull request page itself. Typically, you should *not* be accepting your own pull request. Someone else will take a look! However, for learning purposes, add a comment to simulate someone reviewing your code, then press **Merge pull request** and confirm the merge.

If you go back to your forked repository's `main` branch, you should see your merged code in `editme.txt`!

---

### Step 8: Pull the Merge Down Locally
Your local `main` doesn't know about the merge you just did on GitHub yet! Let's sync up your local `main` to the remote one:

    git checkout main
    git pull                    // downloads and merges changes from remote

This is a step you'll do often on a real team. Anytime someone else's pull request gets merged, you `pull` to bring those changes into your own local repository!

---

### Step 9: Clean up Feature Branches
It is best practice to delete your feature branches after merging into `main`. Run the following commands to delete them from your local machine and from the remote repository:

    git branch -d my-branch                // deletes local branch
    git push origin --delete my-branch     // deletes remote branch

---

### You're done!
You just went through the full loop: clone repository → make a feature branch → commit changes → merge conflict → resolve → PR → pull → clean up feature branches. This is genuinely most of what you'll use day-to-day working on a team!
