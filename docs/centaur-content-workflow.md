# CENTAUR website — Content updates

Repository: https://github.com/centaur-nkua/statlab

## 2. First-time setup (only once)

1. Accept the GitHub organization invitation.
2. Install **Git**, **Hugo Extended 0.163.3**, and a text editor (e.g. VS Code).
3. Open a terminal and run:

   ```bash
   git clone --recurse-submodules https://github.com/centaur-nkua/statlab.git
   cd statlab
   git config --global user.name "Your Name"
   git config --global user.email "your-email@example.com"
   hugo server
   ```

4. Open http://localhost:1313 to check the website. Press **Ctrl+C** in the terminal to stop Hugo.

## 3. Every time you update content

### Step 1 — Get the latest version

Open a terminal in the `statlab` folder:

```bash
git switch main
git pull --ff-only
git submodule update --init --recursive
```

### Step 2 — Create a branch

Choose a short name describing your change:

```bash
git switch -c news/new-talk
```

Use a **new branch name for every change**.

### Step 3 — Edit the content

Open `statlab` in your editor. Website content is under:

- `content/el/` — Greek
- `content/en/` — English

For a new announcement, **copy a similar existing Markdown file**, rename it, and update its contents. Normally update both languages.

### Step 4 — Check locally

```bash
hugo server
```

Open http://localhost:1313. Check both language versions and any links or PDFs. Stop Hugo with **Ctrl+C**.

### Step 5 — Save your changes on GitHub

```bash
git status
git add .
git commit -m "Add new research talk"
git push -u origin news/new-talk
```

Change the commit message and branch name to match your update. GitHub may ask you to sign in.

### Step 6 — Create and merge a Pull Request

1. Open https://github.com/centaur-nkua/statlab.
2. Click **Compare & pull request** for your new branch (or go to **Pull requests → New pull request**).
3. Check that the destination branch is `main`, and click **Create pull request**.
4. For routine content changes, merge once checks have passed. Ask the other administrator to review changes to templates, configuration, or deployment.
5. Confirm that the deployment action succeeds and check the live CENTAUR site.

### Step 7 — Prepare for next time

```bash
git switch main
git pull --ff-only
git branch -d news/new-talk
```

You can also delete the branch on GitHub after merging.

## Important rules

- **Do not edit `main` directly.** Use a branch and Pull Request.
- **Do not upload files directly to the CENTAUR server.** Merging into `main` triggers deployment.
- If Git reports a conflict or an unfamiliar error, **stop and ask** rather than forcing a command.
