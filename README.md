# system-installation-cource-#  My Git + VS Code + GitHub Setup Guide

How  to set up Git, GitHub, and VS Code and push your first project.

## 1. Create a GitHub Account

First things first, head over to [GitHub](https://github.com) and create an account.

Its simple  just click **Sign up**, enter your details, verify your email, and boom  youre in!

 ![GitHub signup page](github_account_creation.png)


## 2. Install Chocolatey (Windows Only)

If youre on **Windows**, Chocolatey is a package manager that makes it super easy to install stuff.

1. Open **PowerShell** as Administrator.  
2. Paste this command and press **Enter**:

   ## 2. Install Chocolatey (Windows Only)

If youre on **Windows**, Chocolatey is a package manager that makes it super easy to install stuff.

1. Open **PowerShell** as Administrator.  
2. Paste this command and press **Enter**:

   ```powershell
   Set-ExecutionPolicy Bypass -Scope Process -Force; `
   [System.Net.ServicePointManager]::SecurityProtocol = `
   [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; `
   iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
   ```

3. Once its done, restart PowerShell.

 ![PowerShell showing Chocolatey installation](images/chocolatey_installation.png)

## 3. Install Windows Terminal

After Chocolatey is ready, type this command in PowerShell:

```bash
choco install microsoft-windows-terminal -y

This gives you a nice modern terminal for running commands.

## 4. Install Git

Still in PowerShell, install Git:

```bash
choco install git -y

Once its done, check if it installed correctly:

```bash
git --version

 ![Git installation check](images/git_command_test.png)

## 5. Install Visual Studio Code (VS Code)

Lets grab VS Code  your main coding workspace.

```bash
choco install vscode -y

Or if you prefer, download it manually from  
 [https://code.visualstudio.com](https://code.visualstudio.com)

## 6. Create a Workspace Folder

Create a place on your computer where all your projects will live.

```bash
mkdir C:\workspace
cd C:\workspace

Thats it! You now have a home for your projects.


## 7. Install VS Code Extensions

Now open VS Code (you can type `code .` in your terminal if youre inside the workspace folder).

Once open:
- Go to the **Extensions tab** (icon on the left or `Ctrl+Shift+X`)
- Search and install these:
  - **GitHub Pull Requests and Issues**
  - **GitLens  Git supercharged**
  - **Markdown All in One**
  - (Optional) **Python** if youll use Python later

 ![VSCode extensions installed](images/vscode_material_icon_extension.png)

## 8. Install SSH

You might already have SSH, but lets check just to be sure.

In PowerShell, run:
```bash
ssh -V

If it says something like `OpenSSH_for_Windows_8.x`, youre good!  
If not, install it:
```bash
choco install openssh -y
## 9. Generate SSH Keys

This key will let your computer connect to GitHub securely without needing your password every time.

Run this command (replace your email):

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"

Just press **Enter** for each prompt unless you want to add a passphrase.

 ![SSH keygen command output](images/ssh_keygen_success.png)

## 10. Start and Setup the SSH Agent

In PowerShell (run as Administrator):

```powershell
sc.exe config ssh-agent start=auto
net start ssh-agent

Now add your private key to the agent:

```powershell
ssh-add C:\Users\HP\.ssh\id_ed25519

 ![SSH agent confirmation](images/ssh_authentication_success.png)

## 11. Add Your Public Key to GitHub

Lets connect your computer to GitHub!

1. Run this to see your **public key**:
   ```bash
   Get-Content ~/.ssh/id_ed25519.pub

2. Copy everything from `ssh-ed25519` to the end of your email.
3. Go to **GitHub  Settings  SSH and GPG Keys  New SSH key**.
4. Paste the key, give it a name (like My Laptop), and save.

 ![GitHub SSH key addition](images/github_dashboard.png)

## 12. Test Your Connection

Now test if your key works:

```bash
ssh -T git@github.com

If you see:
```
Hi your-username! You've successfully authenticated, but GitHub does not provide shell access.


then  youre good to go!

 ![SSH connection success message](images/ssh_authentication_success.png)

## 13. Try Some Simple Git Commands

Create a test folder and initialize Git:

bash
mkdir test-repo
cd test-repo
git init


Then create a file:
bash
echo "# My First Repo" > README.md
git add README.md
git commit -m "First commit"

 ![Git init and first commit](images/05_git_command_test.png)

## 14. Create a Repository on GitHub

Go to [GitHub](https://github.com), click **New Repository**,  
name it (like *test-repo*), and keep it empty (no README).

Copy the SSH link (itll look like this):

git@github.com:your-username/test-repo.git

## 15. Link and Push Your Local Repo

Now connect your local project to the GitHub one:
bash
git remote add origin git@github.com:your-username/test-repo.git
git branch -M main
git push -u origin main

Then check GitHub  your README file should appear there 

## 16. Clone an Existing Repo

If you ever want to download a repo from GitHub:

bash
git clone git@github.com:username/repo-name.git

## 17. Create a Markdown Document

Markdown files are just text files with `.md` extensions  great for notes or documentation.

In VS Code:
1. Click **New File**
2. Save it as `Installation Guide.md`
3. Write something like:
    markdown
   # Installation Guide
   Heres how to set up Git and GitHub...

## 18. Push Your Changes

Once youve typed your markdown document, go to terminal then type
bash
git add .
git commit -m "Added installation guide"
git push
Now check your GitHub repo  your new Markdown file should be there!
