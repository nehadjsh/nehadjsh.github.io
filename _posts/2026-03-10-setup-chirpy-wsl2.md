---
layout: post
title:  "The Ultimate Guide to Hosting a Chirpy Blog on GitHub Pages using WSL2"
date: 2026-03-10 01:00:05 +0300
categories: [Tutorials, GitHub]
tags: [GitHub-Pages, Chirpy, WSL2, Jekyll, Ruby, Guide]
comments: true
---



# The Ultimate Guide to Hosting a Chirpy Blog on GitHub Pages using WSL2

## 1. What is GitHub Pages & Why Use It?

**GitHub Pages** is a free static site hosting service. By using the **Chirpy** template, you get a professional, SEO-optimized, and high-performance technical blog without hosting costs.

---

## Prerequisites



Before we begin, ensure you have the following:

    Windows 10 or 11 (Updated to the latest version).

    GitHub Account (Ready to create a new repository).

    Basic Terminal Familiarity (Knowing how to copy/paste commands).

    Visual Studio Code installed on your Windows machine.

---

## 2. Initial Repository Setup

1. Navigate to the [Chirpy Starter Template](https://github.com/cotes2020/chirpy-starter).
2. Select **Use this template** > **Create a new repository**.

![](/assets/img/posts/2026-03-10-setup-chirpy-wsl2/01.png)

3. **Name your repo:** `your-username.github.io`.
4. **Visibility:** Must be **Public**.

![](/assets/img/posts/2026-03-10-setup-chirpy-wsl2/02.png)

5. **Critical Configuration:** Go to **Settings > Pages**. Under "Build and deployment", change the source to **GitHub Actions**.

> **💡 Note:** We choose **GitHub Actions** because older tutorials assume simple sites. Chirpy uses advanced Ruby plugins that require a custom build workflow provided by GitHub Actions to function correctly.

![](/assets/img/posts/2026-03-10-setup-chirpy-wsl2/03.png)

![](/assets/img/posts/2026-03-10-setup-chirpy-wsl2/04.png)

![](/assets/img/posts/2026-03-10-setup-chirpy-wsl2/05.png)

---

## 3. Environment Setup (WSL2 & Ubuntu)

### Phase A: Install WSL2 (Windows Side)

1. Open **Windows PowerShell** as Administrator.
2. Run the following command:
```powershell
wsl --install
```
3. **Ubuntu** will launch automatically after installation. Create your Linux username and password.

![](/assets/img/posts/2026-03-10-setup-chirpy-wsl2/08.png)

### Phase B: System Updates & Tools

Inside your **Ubuntu terminal**, run:

```bash
# Update the system
sudo apt update && sudo apt upgrade -y

# Install essential dependencies
sudo apt install -y build-essential git curl rbenv
```

![](/assets/img/posts/2026-03-10-setup-chirpy-wsl2/09.png)

![](/assets/img/posts/2026-03-10-setup-chirpy-wsl2/010.png)

![](/assets/img/posts/2026-03-10-setup-chirpy-wsl2/011.png)


## 3. Ruby Installation & Path Configuration

Following a practical workflow, we first download the necessary files and then "bridge" them to the system path.

### Phase C: Installing Ruby 3.1.2

Install the specific version required for the Chirpy environment:

```bash
# This downloads and compiles Ruby 3.1.2
rbenv install 3.1.2
```
![](/assets/img/posts/2026-03-10-setup-chirpy-wsl2/012.png)

### Phase D: The Critical Path Fix (rbenv Configuration)

After downloading Ruby, the system still defaults to the pre-installed version. We must update the environment paths so Ubuntu recognizes the new version.

1. **Run these commands to update your profile:**
```bash
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init - bash)"' >> ~/.bashrc
source ~/.bashrc
```

2. **Activate and Verify:**

```bash
# Verification checks
which ruby # Should point to .rbenv/shims/ruby
ruby -v    # Should show version 3.1.2
```

![](/assets/img/posts/2026-03-10-setup-chirpy-wsl2/015.png)

```bash
# Set the installed version as the global default
rbenv global 3.1.2
```

![](/assets/img/posts/2026-03-10-setup-chirpy-wsl2/013.png)

---

## 4. Local Development & VS Code Integration

### Step 1: Organize Your Workspace

```bash
mkdir -p ~/projects
cd ~/projects
```

![](/assets/img/posts/2026-03-10-setup-chirpy-wsl2/018AA.png)

### Step 2: Clone and Open with VS Code

```bash
# Clone your repo
git clone https://github.com/your-username/your-username.github.io.git
cd your-username.github.io
```

![](/assets/img/posts/2026-03-10-setup-chirpy-wsl2/017.png)

![](/assets/img/posts/2026-03-10-setup-chirpy-wsl2/018BB.png)


```bash
# Open in VS Code (This bridges Linux to Windows)
code .
```

![](/assets/img/posts/2026-03-10-setup-chirpy-wsl2/019.png)

![](/assets/img/posts/2026-03-10-setup-chirpy-wsl2/020.png)

### Step 3: Install Jekyll & Preview

```bash
gem install bundler jekyll
bundle install
bundle exec jekyll serve
```

![](/assets/img/posts/2026-03-10-setup-chirpy-wsl2/016.png)

![](/assets/img/posts/2026-03-10-setup-chirpy-wsl2/022.png)

Your blog is now live locally at `http://127.0.0.1:4000`.

![](/assets/img/posts/2026-03-10-setup-chirpy-wsl2/023.png)

---

## 5. Deployment

Ready to go live? Push your changes to GitHub:

```bash
git add .
git commit -m "My first Chirpy post via WSL2"
git push
```

Your site will be deployed automatically via **GitHub Actions** to `https://your-username.github.io`.

---

## References & Resources

* [Official Jekyll Documentation](https://jekyllrb.com/docs/)
* [Chirpy Theme Wiki & Customization](https://github.com/cotes2020/jekyll-theme-chirpy/wiki)
* [WSL2 Documentation](https://learn.microsoft.com/en-us/windows/wsl/)

 "Must-watch: An excellent lecture on this topic."
 {% include embed/youtube.html id='0aa6Tsd6ZDA' %}
---

## Summary Checklist

* [ ] Repository created as `username.github.io`.
* [ ] Deployment source set to **GitHub Actions**.
* [ ] Ruby 3.1.2 installed via `rbenv`.
* [ ] Path configuration added to `.bashrc`.
* [ ] Local preview working at port `4000`.
* [ ] VS Code "WSL Extension" installed for seamless editing.

---
