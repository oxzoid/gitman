# Git Account Manager (gitman)

A beautiful cross-platform CLI tool to manage multiple GitHub accounts on the same machine. Switch between personal, work, and client accounts effortlessly with arrow key navigation, automatic SSH key management, and smart remote URL updates.

![Version](https://img.shields.io/badge/version-1.0-blue)
![Python](https://img.shields.io/badge/python-3.6+-green)
![Platform](https://img.shields.io/badge/platform-Linux%20%7C%20Windows-lightgrey)
![License](https://img.shields.io/badge/license-MIT-orange)

## ✨ Features

- 🎨 **Beautiful TUI** - Arrow key navigation, no typing needed
- ⚡ **Fast Switching** - Change accounts in seconds
- 🔐 **Auto SSH Setup** - Generates keys and configures everything
- 🔄 **Smart URL Updates** - Automatically fixes remote URLs
- 💾 **Persistent Config** - Remembers all your accounts
- 🎯 **Repo Detection** - Knows when you're in a git repository
- 🖥️ **Cross-Platform** - Works on Linux, macOS, and Windows
- 📦 **Zero Dependencies** - Single Python script, no pip install needed

## 📸 Screenshots

### Quick Switch (Arrow Keys)
```
Select Account:
────────────────────────────────────────────────────────────
→ ● personal       john@personal.com
    work           john@work.com  
    client1        john@client1.com
────────────────────────────────────────────────────────────

↑/↓ Navigate  Enter Select  q Cancel
```

### Interactive TUI
```
╔════════════════════════════════════════════════════════╗
║           Git Account Manager v1.0                     ║
╚════════════════════════════════════════════════════════╝

✓ In git repository
  Account: personal
  Current: John Doe <john@personal.com>

Quick Actions:
  s. Switch account (arrow key selection)
  w. Show status (who am I?)

Account Management:
  l. List all accounts
  a. Add account
  r. Remove account

  q. Exit
```

## 🚀 Installation

### Linux / macOS

#### Option 1: Quick Install (Recommended)
```bash
# Download and install
curl -o ~/bin/gitman https://raw.githubusercontent.com/oxzoid/gitman/main/gitman
chmod +x ~/bin/gitman

# Add ~/bin to PATH if not already there
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc

# Or for zsh
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

#### Option 2: Manual Install
```bash
# Create bin directory
mkdir -p ~/bin

# Download the script (or copy-paste the code)
nano ~/bin/gitman
# Paste the gitman code, save with Ctrl+O, Enter, Ctrl+X

# Make executable
chmod +x ~/bin/gitman

# Add to PATH
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

#### Verify Installation
```bash
gitman help
```

### Windows

#### Option 1: Using Git Bash (Recommended)
```bash
# In Git Bash
mkdir -p ~/bin
curl -o ~/bin/gitman https://raw.githubusercontent.com/oxzoid/gitman/main/gitman
chmod +x ~/bin/gitman

# Add to PATH
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc

# Verify
gitman help
```
#### Option 2: Using PowerShell
```powershell
# Create directory
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\bin"

# Download the script
Invoke-WebRequest -Uri "https://raw.githubusercontent.com/oxzoid/gitman/main/gitman" -OutFile "$env:USERPROFILE\bin\gitman.py"

# Create wrapper batch file
$batchContent = @"
@echo off
python "%USERPROFILE%\bin\gitman.py" %*
"@
Set-Content -Path "$env:USERPROFILE\bin\gitman.bat" -Value $batchContent

# Add to PATH (User level - no admin needed)
$currentPath = [Environment]::GetEnvironmentVariable("Path", "User")
if ($currentPath -notlike "*$env:USERPROFILE\bin*") {
    [Environment]::SetEnvironmentVariable("Path", "$currentPath;$env:USERPROFILE\bin", "User")
}

# Restart PowerShell, then verify
# Close and reopen PowerShell
gitman help
```

#### Option 3: Direct Python Execution
```bash
# Save the script anywhere
python C:\path\to\gitman.py help

# Or add an alias
doskey gitman=python C:\path\to\gitman.py $*
```

#### Windows Requirements
- **Python 3.6+** (Download from [python.org](https://www.python.org/downloads/))
- **Git for Windows** (includes OpenSSH) - [Download](https://git-scm.com/download/win)
- **OpenSSH Client** (Windows 10+ has it built-in, or comes with Git)

## 📖 Quick Start

### First Time Setup

Run the setup wizard - it does everything for you:

```bash
gitman setup
```

This will:
1. ✅ Ask for your account details
2. ✅ Generate SSH keys automatically
3. ✅ Configure SSH hosts
4. ✅ Add keys to ssh-agent
5. ✅ Show you the public key to add to GitHub
6. ✅ Test the connection

**Just follow the prompts and paste the public key to GitHub!**

### Adding More Accounts

```bash
gitman add
# Choose option 2 for auto-setup
```

### Switch Accounts

```bash
# In any git repository
gitman

# Use arrow keys to select account
# Press Enter to switch
```

## 🎯 Usage

### Commands

```bash
gitman setup             # Complete setup wizard (first time)
gitman                   # Quick switch (arrow key selection)
gitman status            # Show current git identity
gitman switch            # Switch with arrow keys
gitman switch <account>  # Switch to specific account
gitman list              # List all accounts
gitman add               # Add new account
gitman remove            # Remove account (arrow keys)
gitman remove <account>  # Remove specific account
gitman help              # Show help
```

### Aliases

```bash
gitman who               # Same as 'status'
gitman s                 # Same as 'switch'
gitman ls                # Same as 'list'
gitman l                 # Same as 'list'
gitman a                 # Same as 'add'
gitman rm <account>      # Same as 'remove'
gitman r                 # Same as 'remove'
```

### Interactive Mode Shortcuts

When in the TUI (run `gitman` without arguments):
- `s` - Switch account
- `w` - Show status (who am I?)
- `l` - List all accounts
- `a` - Add account
- `r` - Remove account
- `q` - Quit

## 📁 File Locations

### Linux / macOS

```
~/.gitmanager/
└── config.json                 # Account configurations

~/.ssh/
├── config                      # SSH host configurations
├── id_ed25519_personal         # Personal private key
├── id_ed25519_personal.pub     # Personal public key
├── id_ed25519_work             # Work private key
├── id_ed25519_work.pub         # Work public key
└── ...

~/bin/
└── gitman                      # The script
```

### Windows

```
C:\Users\YourName\.gitmanager\
└── config.json                 # Account configurations

C:\Users\YourName\.ssh\
├── config                      # SSH host configurations
├── id_ed25519_personal         # Personal private key
├── id_ed25519_personal.pub     # Personal public key
├── id_ed25519_work             # Work private key
├── id_ed25519_work.pub         # Work public key
└── ...

C:\Users\YourName\bin\
└── gitman.py                   # The script
```

## 🎓 Complete Workflow Example

### Scenario: Developer with Personal and Work Accounts

```bash
# 1. Install gitman
curl -o ~/bin/gitman https://raw.githubusercontent.com/oxzoid/gitman/main/gitman
chmod +x ~/bin/gitman

# 2. Setup personal account
gitman setup
# Answer prompts:
# - Account name: personal
# - Display name: John Doe
# - Email: john@personal.com
# - GitHub username: johndoe
# Copy the SSH key to GitHub

# 3. Setup work account
gitman add
# Choose option 2 (auto-setup)
# - Account name: work
# - Display name: John Doe
# - Email: john@company.com
# - GitHub username: johndoe-work
# Copy the SSH key to GitHub

# 4. Clone a personal project
git clone git@github.com-personal:johndoe/my-project.git
cd my-project

# 5. Verify identity
gitman status
# Shows: personal account

# 6. Switch to work project
cd ~/work/company-project

# 7. Switch account
gitman
# Use arrows to select 'work', press Enter

# 8. Verify
gitman status
# Shows: work account

# 9. Commit and push
git add .
git commit -m "Update feature"
git push
# Uses work account identity!
```

## 🔧 Manual SSH Setup (Advanced)

If you prefer to set up SSH manually instead of using auto-setup:

### 1. Generate SSH Keys

```bash
# Personal account
ssh-keygen -t ed25519 -C "personal@email.com" -f ~/.ssh/id_ed25519_personal

# Work account
ssh-keygen -t ed25519 -C "work@email.com" -f ~/.ssh/id_ed25519_work
```

### 2. Configure SSH (~/.ssh/config)

```bash
nano ~/.ssh/config
```

Add:
```ssh
# Personal GitHub Account
Host github.com-personal
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_personal
    IdentitiesOnly yes

# Work GitHub Account
Host github.com-work
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_work
    IdentitiesOnly yes
```

### 3. Add Keys to GitHub

```bash
# Copy personal key
cat ~/.ssh/id_ed25519_personal.pub

# Copy work key
cat ~/.ssh/id_ed25519_work.pub
```

Go to GitHub → Settings → SSH and GPG keys → New SSH key

### 4. Add to gitman

```bash
gitman add
# Choose option 1 (manual setup)
```

### 5. Test Connections

```bash
ssh -T git@github.com-personal
ssh -T git@github.com-work
```

Expected: `Hi username! You've successfully authenticated...`

## 🎨 How It Works

### SSH Host Aliases

Each account uses a unique SSH host alias:
- `github.com-personal` → Uses personal SSH key
- `github.com-work` → Uses work SSH key
- `github.com-client1` → Uses client1 SSH key

### Repository-Level Git Config

gitman sets `user.name` and `user.email` at the **repository level**, never touching global config:

```bash
cd ~/my-repo
gitman switch personal

# Sets:
# git config user.name "John Doe"
# git config user.email "john@personal.com"
```

### Automatic Remote URL Updates

When switching accounts, gitman automatically updates remote URLs:

```bash
# Before: git@github.com-work:user/repo.git
gitman switch personal
# After:  git@github.com-personal:user/repo.git
```

This ensures pushes use the correct SSH key!

## 🆚 Comparison

### vs Traditional Methods

| Feature | gitman | Manual | Git Config | Other Tools |
|---------|--------|--------|------------|-------------|
| Visual UI | ✅ Arrow keys | ❌ CLI only | ❌ CLI only | ⚠️ Varies |
| Auto SSH setup | ✅ Yes | ❌ Manual | ❌ Manual | ⚠️ Some |
| Remote URL fix | ✅ Automatic | ❌ Manual | ❌ Manual | ⚠️ Some |
| Cross-platform | ✅ Win/Mac/Linux | ✅ Yes | ✅ Yes | ⚠️ Limited |
| Zero dependencies | ✅ Just Python | ✅ Just Git | ✅ Just Git | ❌ Need packages |
| Account storage | ✅ Persistent | ❌ Remember | ❌ Scripts | ⚠️ Varies |


## 🐛 Troubleshooting

### "Not in a git repository"
**Solution:** Navigate to a git repository before switching accounts.
```bash
cd ~/your-project
gitman switch personal
```

### "Account not found"
**Solution:** List and add accounts.
```bash
gitman list          # See available accounts
gitman add           # Add new account
```

### Remote URL Not Updating
**Problem:** Remote URL stays the same after switching.
**Solution:** Check SSH config has the correct host.
```bash
cat ~/.ssh/config
# Should have entries like:
# Host github.com-personal
#     HostName github.com
#     ...
```

### SSH Connection Failed
**Problem:** `ssh -T git@github.com-personal` fails
**Solutions:**
1. Check SSH key is added to GitHub
2. Verify SSH config syntax
3. Ensure ssh-agent is running
4. Check key permissions (should be 600)

```bash
# Start ssh-agent
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519_personal

# Fix permissions
chmod 600 ~/.ssh/id_ed25519_personal
chmod 644 ~/.ssh/id_ed25519_personal.pub
chmod 600 ~/.ssh/config
```

### "ssh-keygen: command not found" (Windows)
**Solution:** Install Git for Windows or OpenSSH.
- Git for Windows: https://git-scm.com/download/win
- Or enable OpenSSH in Windows Features

### Arrow Keys Don't Work
**On Windows CMD/PowerShell:** Use Git Bash or Windows Terminal instead.
**On Linux:** Check if terminal supports ANSI escape sequences.

### Colors Don't Show (Windows)
**Solution:** Use Windows Terminal or Git Bash instead of old CMD.
```powershell
# Install Windows Terminal (recommended)
winget install Microsoft.WindowsTerminal
```

### Python Version Issues
**Problem:** `python3: command not found`
**Solution:** Use `python` instead, or install Python 3.6+
```bash
# Check version
python --version
python3 --version

# If needed, download from python.org
## 💡 Tips & Best Practices

### Naming Conventions
Use descriptive account names:
- ✅ `personal`, `work`, `freelance`, `client-acme`
- ❌ `acc1`, `test`, `temp`

### Clone with Correct Host
Always clone using the appropriate SSH host:
```bash
# Personal projects
git clone git@github.com-personal:username/repo.git

# Work projects
git clone git@github.com-work:username/repo.git
```

### Check Before Committing
Get in the habit of checking your identity:
```bash
cd ~/project
gitman status        # Quick check
git commit -m "..."  # Now commit safely
```

### Multiple Clients
For freelancers with many clients:
```bash
gitman add  # client-acme
gitman add  # client-techcorp
gitman add  # client-startup
# Each gets its own SSH key and config
```

### Backup Your Keys
```bash
# Backup SSH keys
cp -r ~/.ssh ~/backup-ssh-$(date +%Y%m%d)

# Backup gitman config
cp ~/.gitmanager/config.json ~/backup-gitman-$(date +%Y%m%d).json
```

## 🤝 Contributing

Contributions welcome! Feel free to:
- Report bugs
- Suggest features
- Submit pull requests
- Improve documentation

## 📄 License

MIT License - feel free to use and modify

## 🙏 Credits

Created by **oxzoid** for developers managing multiple GitHub accounts efficiently.

## 📚 Additional Resources

- [GitHub SSH Documentation](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)
- [Git Config Documentation](https://git-scm.com/docs/git-config)
- [Multiple SSH Keys Guide](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
- [Windows OpenSSH](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse)

## ❓ FAQ

### Does this work with existing repos?
Yes! Run `gitman switch <account>` in any repo to update its identity and remote URL.

### Can I have more than 2 accounts?
Absolutely! Add as many as you need - personal, work, clients, open source, etc.

### Will this mess up my global git config?
No! gitman only sets repository-level config. Your global config remains untouched.

### What if I already have SSH keys?
The setup wizard will detect them and offer to use existing keys or generate new ones.

### Can I use HTTPS instead of SSH?
gitman is designed for SSH key management. For HTTPS, you'd need to use Git credential managers instead.

---

**Made with ❤️ for developers juggling multiple GitHub accounts**

If this tool helped you, give it a ⭐ on GitHub!