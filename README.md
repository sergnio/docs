# docs

## PiHole tutorial
1. Download pi os and ssh into pi  
https://www.youtube.com/watch?v=upY4Fusi4zI

1. Configure pihole software  
https://www.youtube.com/watch?v=UE2sO8d3sx8

## Homebrew without xcode
### Install Command Line Tools

```
xcode-select --install  
```

When this is finished, you can install homebrew!

### Install Homebrew
```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
Voila

## multiple github accounts same computer
### 🔐 SSH Setup for Personal GitHub Projects (`sergn.io`)

This project uses a **dedicated SSH key** and SSH alias (`github.com-sergnio`) to ensure Git pushes and pulls are made under my **personal GitHub account** (`sergnio`), not my work account.

#### ✅ 1. `~/.ssh/config` setup

Ensure the following is in your `~/.ssh/config`:

```ssh
# Personal GitHub account (for sergn.io projects)
Host github.com-sergnio
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_sergnio
  IdentitiesOnly yes

# Default GitHub (work account)
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519
  AddKeysToAgent yes
  UseKeychain yes
  IdentitiesOnly yes
```

#### ✅ 2. Set the Git remote to use the SSH alias

For this project:

```bash
git remote set-url origin git@github.com-sergnio:sergnio/sergn.io-v2.git
git config user.email sergnioa@gmail.com
git config user.name sergnio           
```

This ensures Git uses the personal SSH key for all operations.

#### ✅ 3. Test authentication

```bash
ssh -T git@github.com-sergnio
# Should return: Hi sergnio! You've successfully authenticated...

ssh -T git@github.com
# Should return: Hi snajera-livefront! You've successfully authenticated...
```

#### ✅ 4. Add your key to the SSH agent (if needed)

```bash
ssh-add ~/.ssh/id_rsa_sergnio
```

---

This setup lets you use multiple GitHub identities cleanly:

- **Personal repos** → `git@github.com-sergnio:...`
- **Work repos** → `git@github.com:...`
