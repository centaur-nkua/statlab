# Updating the CENTAUR website (Windows)

These instructions are for an administrator who updates website content from a Windows computer. Use **Git Bash** for all commands below.

## 1. One-time setup

1. Install [Git for Windows](https://git-scm.com/downloads/win), [Visual Studio Code](https://code.visualstudio.com/) and **Hugo Extended 0.163.3** (see [Windows installation instructions](https://gohugo.io/installation/windows/)).
2. Accept the invitation to the [`centaur-nkua` GitHub organization](https://github.com/centaur-nkua) using your GitHub account.
3. Open **Git Bash** and set your name and email (replace the examples):

   ```bash
   git config --global user.name "Your Name"
   git config --global user.email "you@example.com"
   ```

4. In Git Bash, go to the folder where you want to keep the site and clone it:

   ```bash
   cd ~/Documents
   git clone --recurse-submodules https://github.com/centaur-nkua/statlab.git
   cd statlab
   ```

5. Check that Hugo is installed:

   ```bash
   hugo version
   ```

6. Start a local preview:

   ```bash
   hugo server
   ```

   Open **http://localhost:1313** in your browser. Press **Ctrl+C** in Git Bash to stop the preview.

## 2. Start each update

Open **Git Bash** in the `statlab` folder and run:

```bash
git switch main
git pull --ff-only
git submodule update --init --recursive
```

Create a new branch for the change (choose a descriptive name, whether adding or editing content):

```bash
git switch -c news/new-talk
```

## 3. Edit and check the content

Open the `statlab` folder in **Visual Studio Code**. Edit the relevant Markdown (`.md`) files, for example:

- `content/el/news/` — Greek news
- `content/en/news/` — English news
- `content/el/people/` and `content/en/people/` — people
- `content/el/seminars/` and `content/en/seminars/` — seminars

**To add new content:** Copy a similar existing `.md` file, give the copy a new filename, and replace the details.

**To change existing content** (for example, correct an announcement or update a person’s information):

1. Find the **existing** `.md` file in the appropriate folder and open it in VS Code.
2. Change the relevant text or details and **save the same file** (`Ctrl+S`). Do not create a duplicate announcement.
3. If the item has a Greek and an English version, update both files as needed.

For an edit to existing content, use a branch name such as `content/update-person` instead of `news/new-talk`. In the Git commands below, replace `news/new-talk` with **your actual branch name**, and write an appropriate commit message (for example, `Update researcher profile`).

Preview the site in Git Bash:

```bash
hugo server
```

Open **http://localhost:1313** and check both languages and any PDF links. Press **Ctrl+C** when finished.

## 4. Save and submit the change

In Git Bash:

```bash
git status
git add .
git commit -m "Add new research talk"
git push -u origin news/new-talk
```

On GitHub, open the repository at **https://github.com/centaur-nkua/statlab**. Click **Compare & pull request**, review the changed files, and create the Pull Request (PR).

After any required review, **merge the PR into `main`**. The existing GitHub Actions workflow then publishes the update to the CENTAUR website. Check that the deployment succeeded and that the live page looks correct.

## 5. Get ready for the next update

After the PR is merged, return to Git Bash:

```bash
git switch main
git pull --ff-only
git branch -d news/new-talk
```

For the next change, repeat **Sections 2–5** with a new branch name.

**Important:** Do not edit `main` directly or manually upload files to the CENTAUR server.
