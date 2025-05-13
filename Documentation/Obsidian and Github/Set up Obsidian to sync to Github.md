
I decided to set up Obsidian to sync to Github as I was not a fan of making the files in Github, and liked using Obsidian more.

---------------------------

Below are step-by-step instructions for setting up a sync between Obsidian and GitHub using the Obsidian Git plugin, followed by instructions for configuring a `.gitignore` file to prevent unwanted files (like `.obsidian`) from syncing. This guide assumes you have basic familiarity with Obsidian and GitHub, and it’s tailored for syncing a vault’s Markdown notes while keeping settings device-specific.

### Instructions for Setting Up Obsidian to Sync with GitHub

#### Prerequisites
- **Obsidian**: Installed on your device (desktop or mobile).
- **Git**: Installed on your system (for desktop setup). Download from [git-scm.com](https://git-scm.com/) if needed.
- **GitHub Account**: A GitHub account and a repository for your vault.
- **Obsidian Git Plugin**: This plugin automates Git operations within Obsidian.

#### Step 1: Create a GitHub Repository
1. **Log in to GitHub**:
   - Go to [github.com](https://github.com/) and sign in or create an account.
1. **Create a New Repository**:
   - Click the “+” icon in the top-right corner and select “New repository.”
   - Name it (e.g., `MyObsidianVault`).
   - Choose “Private” (recommended for personal notes) or “Public.”
   - Recommended not to have a readme file, and to use a MIT License
   - Click “Create repository.”
3. **Copy the Repository URL**:
   - On the repository page, click the green “Code” button and copy the HTTPS URL (e.g., `https://github.com/your-username/MyObsidianVault.git`).

#### Step 2: Set Up Your Obsidian Vault
1. **Create or Open a Vault**:
   - Open Obsidian and create a new vault (e.g., `MyVault`) or use an existing one.
   - Note the vault’s folder location (e.g., `/path/to/MyVault`).
2. **Initialize a Git Repository in the Vault**:
   - Open a terminal (recommended to use Git Bash on Windows) and navigate to your vault’s folder:
     ```bash
     cd /path/to/MyVault
     ```
   - Initialize Git:
     ```bash
     git init
     ```
   - Connect to your GitHub repository:
     ```bash
     git remote add origin https://github.com/your-username/MyObsidianVault.git
     ```

#### Step 3: Install and Configure the Obsidian Git Plugin
1. **Install the Plugin**:
   - In Obsidian, go to **Settings > Community plugins**.
   - If plugins are disabled, click “Turn on community plugins” (requires disabling Restricted Mode).
   - Search for “Obsidian Git” and click “Install,” then “Enable.”
2. **Configure the Plugin**:
   - Go to **Settings > Obsidian Git**.
   - Set the following:
     - **Commit message**: Customize (e.g., `Sync notes {{date}}`).
     - **Auto commit interval**: Enable “Auto save” and set an interval (e.g., 5 minutes).
     - **Auto push**: Enable to push changes to GitHub automatically after commits.
     - **Username and Email**: Set your Git username and email (same as your GitHub account):
       ```bash
       git config --global user.name "Your Name"
       git config --global user.email "your-email@example.com"
       ```
     - **Vault root**: Ensure it points to your vault folder (usually default).
   - Optionally, enable “Pull updates on startup” to fetch changes when Obsidian starts.

#### Step 4: Authenticate with GitHub
1. **Generate a Personal Access Token** (Recommended, easier):
   - Go to GitHub > Settings > Developer settings (bottom left) > Personal access tokens > Tokens (classic).
   - Click “Generate new token.”
   - Name it (e.g., `ObsidianSync`), select `repo` scope, and generate.
   - Copy the token and store it securely.
2. **Authenticate in Obsidian**:
   - In Obsidian Git settings, set the authentication method:
     - **HTTPS**: Use your GitHub username and the personal access token as the password.
     - **SSH**: If using SSH, ensure your SSH key is set up and added to GitHub (see GitHub’s SSH guide).
   - Test the connection by manually pulling or pushing (use commands like “Git: Pull” or “Git: Push” in Obsidian’s command palette).

#### Step 5: Commit and Push Initial Files
1. **Add Files to Git**:
   - In the terminal, stage all files in your vault (excluding those you’ll ignore later):
     ```bash
     git add .
     ```
2. **Commit Files**:
   - Create an initial commit:
     ```bash
     git commit -m "Initial commit of Obsidian vault"
     ```
3. **Push to GitHub**:
   - Push the commit to your GitHub repository:
     ```bash
     git push -u origin main
     ```
   - If the branch is `master`, replace `main` with `master`.
4. **Verify on GitHub**:
   - Visit your GitHub repository to ensure your Markdown files are synced.

#### Step 6: Test Sync with Obsidian Git
1. **Make a Test Change**:
   - Create or edit a note in Obsidian.
2. **Check Sync**:
   - Wait for the auto-commit interval or manually trigger a commit/push via Obsidian’s command palette:
     - Open the command palette (`Ctrl/Cmd + P` in Obsidian).
     - Run “Obsidian Git: Commit all changes” and “Obsidian Git: Push.”
   - Verify the changes appear on GitHub.
- 
(Not needed I believe) **Pull Changes on Another Device**:
   - On another device, clone the repository to a new vault folder:
     ```bash
     git clone https://github.com/your-username/MyObsidianVault.git /path/to/MyVault
     ```
   - Open the vault in Obsidian and enable the Obsidian Git plugin.
   - Pull changes automatically or via “Git: Pull” in the command palette.

### Instructions for Setting Up `.gitignore`
To prevent device-specific settings (like the `.obsidian` folder) from syncing and causing merge conflicts, create a `.gitignore` file to ignore unwanted files.

1. **Create the `.gitignore` File**:
   - Navigate to the root of your vault (e.g., `/path/to/MyVault`).
   - Create a file named `.gitignore`(In vault):
     - In a text editor, create `MyVault/.gitignore`.
     - Or in the terminal:
       ```bash
       touch .gitignore
       ```

2. **Add Entries to `.gitignore`**:
   - Open `.gitignore` in a text editor and add the following to ignore the `.obsidian` folder and other potential conflict-causing files:
     
     .obsidian/
     .trash/
     conflict-files-obsidian-git.md
     
   - **Explanation**:
     - `.obsidian/`: Ignores all Obsidian settings (plugins, workspace, etc.).
     - `.trash/`: Ignores deleted notes stored by Obsidian.
     - `conflict-files-obsidian-git.md`: Ignores conflict files generated by the Obsidian Git plugin.

3. **Stage and Commit `.gitignore`**:
   - Stage the `.gitignore` file:
     ```bash
     git add .gitignore
     ```
   - Commit it:
     ```bash
     git commit -m "Add .gitignore to ignore .obsidian and other files"
     ```

4. **Remove Previously Tracked Files (if needed)**:
   - If `.obsidian` or other ignored files were already tracked (i.e., they’re in the GitHub repository), remove them from tracking without deleting locally:
     ```bash
     git rm --cached -r .obsidian
     ```
   - Commit the removal:
     ```bash
     git commit -m "Remove .obsidian from tracking"
     ```

5. **Push Changes**:
   - Push all changes to GitHub:
     ```bash
     git push origin main
     ```
   - Replace `main` with your branch name if different.

6. **Verify**:
   - Check your GitHub repository to ensure:
     - The `.gitignore` file is present.
     - The `.obsidian` folder and other ignored files are no longer synced.
   - Future changes to ignored files won’t be tracked.

### Notes
- **Why Ignore `.obsidian`?** The `.obsidian` folder contains device-specific settings (e.g., `workspace.json`, `app.json`) that can cause merge conflicts when synced across devices. Ignoring it ensures only your notes sync.
- **Mobile Setup**: On mobile, use the Obsidian Git plugin’s commands (via the command palette) to manage commits and pushes. Edit `.gitignore` using a mobile text editor or Obsidian’s file explorer.
- **Conflict Prevention**: If you need specific settings synced (e.g., plugins), consider using the “Sync” plugin for settings instead of Git, or selectively include `.obsidian` subfiles (e.g., `community-plugins.json`) while ignoring others.
- **Backup**: Regularly back up your vault locally or on another service to prevent data loss.
- **Troubleshooting**:
  - **Authentication Issues**: Ensure your personal access token or SSH key is correctly configured.
  - **Merge Conflicts**: If conflicts occur, resolve them manually in the affected files or use the Obsidian Git plugin’s conflict resolution tools.
  - **Plugin Not Committing**: Check Obsidian Git settings for correct intervals and authentication.

With these steps, your Obsidian vault will sync with GitHub, and the `.gitignore` file will prevent unwanted files from being tracked, reducing the risk of merge conflicts. If you need help with specific steps or encounter issues, let me know!