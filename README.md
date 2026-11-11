# 🍳 PanPan

> A mobile cooking assistant that helps you make better use of the food you already have.

PanPan is a mobile application that helps users manage the food in their home, keep track of expiry dates, discover meals they can make with their existing ingredients, and identify what they still need to buy.

The project is being developed as part of the **CS6005 Software Design and Development** module.

---

## 📖 Overview

Food is often forgotten at the back of a cupboard or fridge, while deciding what to cook can involve manually checking ingredients and searching through recipes.

PanPan aims to simplify this process by maintaining a digital inventory of the food a user already owns.

Users will be able to add ingredients through methods such as:

- receipt scanning using OCR;
- cupboard or food scanning;
- manual confirmation and correction of recognised items and quantities.

PanPan can then use this inventory to:

- track ingredients;
- monitor best-before dates;
- recommend recipes based on available ingredients;
- identify ingredients missing from a recipe; and
- generate a shopping list containing those missing ingredients.

The longer-term concept introduces **PanPan**, a friendly pan character. Users could drag food emojis or ingredients into PanPan to request a recipe incorporating those ingredients.

---

## 🎯 Core Scope

The initial implementation focuses on three areas:

### 1. Reliable food inventory

Maintain an accurate representation of ingredients owned by the user.

Where OCR or image recognition is used, recognised food should be presented to the user for confirmation rather than being assumed to be correct.

### 2. Date tracking

Store and monitor expiry or best-before information associated with inventory items.

This can be used to help users identify ingredients that should be consumed soon.

### 3. Recipe selection and shopping lists

Recommend suitable recipes based on the ingredients currently available.

Where ingredients required by a recipe are unavailable, PanPan should identify the missing ingredients and allow them to be incorporated into a shopping list.

---

## 🔭 Additional and Stretch Features

After the core system is working reliably, the project may explore:

- 🍳 drag-and-drop interaction with the PanPan character;
- 📷 vision-based quantity estimation;
- 🥽 AR-assisted recipe guidance;
- ⌚ smartwatch support; and
- 🥽 Meta Quest support.

These features are considered extensions and are subject to feasibility, available development time and testing.

The reliability of the inventory, date-tracking and recipe-selection functionality takes priority over the stretch features.

---

## 📱 Target Environment

### Platform

- Android and/or iOS
- Camera-equipped smartphone

### Potential additional hardware

- Smartwatch
- Meta Quest headset

### Software capabilities

The project is expected to make use of technologies including:

- OCR;
- local data storage;
- a recipe catalogue;
- camera/image processing; and
- optionally, an AR SDK.

The exact libraries, frameworks and architecture should be documented here as they are selected during the design and implementation phases.

---

## 👥 Team

| Team Member | Primary Implementation Area |
|---|---|
| Arjan | Inventory |
| Yaksh | OCR |
| Aleena | Recipes |
| Jevon | Storage and date tracking |
| Zayn | UI / PanPan interaction |

These areas represent the proposed allocation rather than strict ownership. Integration, testing, design, requirements and documentation are collaborative responsibilities.

---

## 🗓️ Development Plan

| Task | Description | Effort | Duration | Dependency |
|---|---|---:|---:|---|
| T1 | Planning and scoping | 10 person-days | 5 days | None |
| T2 | Requirements and acceptance tests | 10 person-days | 5 days | T1 |
| T3 | Architecture, class and sequence design | 15 person-days | 5 days | T2 |
| T4 | Core inventory, OCR and recipe implementation | 20 person-days | 10 days | T3 |
| T5 | Core testing and defect resolution | 10 person-days | 5 days | T4 |
| T6 | Shopping lists, date tracking and PanPan interaction | 15 person-days | 5 days | T5 |
| T7 | End-to-end system testing | 10 person-days | 5 days | T6 |
| T8 | Demonstration, report and submission | 10 person-days | 5 days | T7 |

---

# 🛠️ Development Setup

## Prerequisites

Before working on PanPan, each team member should have:

- Git installed;
- a GitHub account;
- access to the PanPan GitHub repository; and
- an SSH key associated with their GitHub account.

Check that Git and SSH are available using:

```cmd
git --version
ssh -V
```

---

# 🔑 GitHub SSH Setup on Windows

Some team members may already use SSH for a corporate Bitbucket account.

**Do not replace or delete your existing corporate SSH key.**

GitHub can use a separate SSH key, allowing corporate Bitbucket and personal/project GitHub access to coexist on the same machine.


---

## 1. Check your existing SSH configuration

Open **Command Prompt** and run:

```cmd
dir "%USERPROFILE%\.ssh"
```

If you already use corporate Bitbucket, you might see files such as:

```text
id_rsa
id_rsa.pub
known_hosts
```

Do not delete or overwrite these files.

---

## 2. Generate a separate GitHub SSH key

Create a new Ed25519 key specifically for GitHub:

```cmd
ssh-keygen -t ed25519 -C "YOUR_GITHUB_USERNAME" -f "%USERPROFILE%\.ssh\id_ed25519_github"
```

For example:

```cmd
ssh-keygen -t ed25519 -C "steveprocoder" -f "%USERPROFILE%\.ssh\id_ed25519_github"
```

You will be asked whether you want a passphrase.

Afterwards, your `.ssh` directory should contain files similar to:

```text
id_rsa
id_rsa.pub

id_ed25519_github
id_ed25519_github.pub

known_hosts
```

`id_ed25519_github` is your **private key**.

**Never share, upload or commit this file.**

`id_ed25519_github.pub` is the corresponding public key and can safely be added to GitHub.

---

## 3. Add the public key to GitHub

Display the public key:

```cmd
type "%USERPROFILE%\.ssh\id_ed25519_github.pub"
```

Copy the entire output, which should start with:

```text
ssh-ed25519
```

In GitHub, navigate to:

**Settings → SSH and GPG keys → New SSH key**

Choose **Authentication Key** and paste the public key.

---

## 4. Configure SSH to use the GitHub key

If you do not already have an SSH `config` file:

```cmd
notepad "%USERPROFILE%\.ssh\config"
```

Add:

```text
Host github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_github
    IdentitiesOnly yes
```

### ⚠️ Windows Notepad warning

Notepad may save the file as:

```text
config.txt
```

OpenSSH requires it to be named exactly:

```text
config
```

Check with:

```cmd
dir "%USERPROFILE%\.ssh"
```

If you see `config.txt`, rename it:

```cmd
rename "%USERPROFILE%\.ssh\config.txt" config
```

---

## 5. Test GitHub authentication

Run:

```cmd
ssh -T git@github.com
```

The first connection may produce a message asking whether you trust the GitHub host.

After successful authentication you should receive a message similar to:

```text
Hi YOUR_USERNAME! You've successfully authenticated, but GitHub does not provide shell access.
```

A message such as:

```text
Permission denied (publickey).
```

means SSH authentication is not yet configured correctly.

For additional diagnostic information, use:

```cmd
ssh -vT git@github.com
```

---

# 📥 Clone PanPan

Once GitHub SSH authentication works:

```cmd
git clone git@github.com:steveprocoder/PanPan.git
```

Then:

```cmd
cd PanPan
```

---

# 👤 Configure Your Git Commit Identity

SSH authentication and Git commit identity are separate.

**SSH determines whether you can access the repository.**

**Git's `user.name` and `user.email` determine who is recorded as the author of your commits.**

Check your existing configuration:

```cmd
git config user.name
git config user.email
```

If you use the computer for corporate development as well, avoid changing your global corporate Git configuration.

Instead, configure PanPan locally:

```cmd
git config user.name "YOUR NAME"
git config user.email "YOUR GITHUB EMAIL"
```

These commands only affect the current repository when `--global` is not specified.

If you do not want your personal email address to appear in commits, GitHub provides a private `@users.noreply.github.com` address under:

**GitHub → Settings → Emails**

Use the exact noreply address shown by GitHub.

Verify the configuration with:

```cmd
git config user.name
git config user.email
```

You only need to configure this **once for this local clone**.

---

# 🌿 Git Workflow

Avoid implementing features directly on the main branch.

Start by updating your local copy:

```cmd
git checkout main
git pull
```

Create a branch for your task:

```cmd
git checkout -b feature/short-description
```

Examples:

```text
feature/inventory-storage
feature/receipt-ocr
feature/recipe-selection
feature/date-tracking
feature/shopping-list
feature/panpan-ui
```

Make your changes and inspect them:

```cmd
git status
git diff
```

Then stage and commit:

```cmd
git add .
git commit -m "Add expiry date storage"
```

Push the branch:

```cmd
git push -u origin feature/date-tracking
```

The branch can then be reviewed and merged through a GitHub pull request.

---

## Commit Messages

Prefer short messages that describe the change clearly.

Good examples:

```text
Add inventory persistence
Implement expiry date validation
Add OCR result confirmation screen
Fix duplicate shopping list items
Add tests for expired ingredients
```

Avoid messages such as:

```text
stuff
changes
update
fix
final version 2
```

The Git history may form useful implementation evidence later in the project, so keeping it understandable is worthwhile.

---

# 🧪 Testing

Testing is part of the implementation rather than something left exclusively until the end of the project.

Where appropriate, new functionality should include tests covering:

- expected behaviour;
- invalid input;
- boundary conditions;
- error handling; and
- interactions with other PanPan components.

The team should especially test recognition-based features where OCR or computer vision results may be uncertain.

---

# 📚 Coursework Documentation

Development should be supported by evidence throughout the project.

Keep useful records of:

- requirements and acceptance criteria;
- architecture/design decisions;
- implementation progress;
- testing and results;
- significant defects and resolutions;
- individual contributions;
- meeting discussions;
- AI-assisted development; and
- limitations or features deliberately removed from scope.

Do not wait until the final week to reconstruct this information from memory.

---

## ⚠️ AI and Diagramming

AI tools may be used where permitted by the module guidance, including appropriate assistance with software development.

However, the coursework guidance states that **AI tools must not be used to generate the assessed UML/design diagrams**, including:

- use-case diagrams;
- architecture diagrams;
- class diagrams; and
- sequence diagrams.

The required diagrams must therefore be created using the methods permitted by the module guidance.

If AI functionality itself is incorporated into PanPan, its use and scope should be discussed with the module leader and appropriately documented.

---

# 🔒 Security

Never commit:

- SSH private keys;
- passwords;
- API keys;
- access tokens;
- credentials; or
- local secrets/configuration containing credentials.

Before committing, always check:

```cmd
git status
```

Secrets required by the application should be kept outside source control and excluded using `.gitignore` where appropriate.

---

# 📌 Project Status

🚧 **PanPan is currently under development.**

The initial development priority is:

1. Inventory
2. OCR and inventory input
3. Recipe selection
4. Local storage
5. Date tracking
6. Shopping lists
7. PanPan interaction
8. Further stretch features where feasible

Core functionality and reliability take priority over AR, smartwatch, Meta Quest and other stretch functionality.

---

## 🎓 Module

**CS6005 Software Design and Development**
Semester 1, 2026–27

Final coursework deadline: **25 January 2027, 17:00**

PanPan is an educational software engineering project developed as part of the module.
