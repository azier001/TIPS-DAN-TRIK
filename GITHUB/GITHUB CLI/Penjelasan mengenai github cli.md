# 🚀 GitHub CLI - Panduan Lengkap untuk Pemula

<div align="center">

![GitHub CLI](https://img.shields.io/badge/GitHub%20CLI-2.0+-blue?style=for-the-badge&logo=github)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Active-success?style=for-the-badge)

**Kelola repository GitHub langsung dari terminal dengan mudah!**

</div>

---

## 📋 Daftar Isi

- [🔧 Instalasi](#-instalasi)
- [🔐 Login & Autentikasi](#-login--autentikasi)
- [📁 Mengelola Repository](#-mengelola-repository)
- [⬆️ Push Project ke GitHub](#️-push-project-ke-github)
- [🌿 Mengelola Branch](#-mengelola-branch)
- [🔀 Pull Request](#-pull-request)
- [💡 Tips & Trik](#-tips--trik)

---

## 🔧 Instalasi

### Windows
```powershell
# Menggunakan Chocolatey
choco install gh

# Menggunakan Scoop
scoop install gh
```

### macOS
```bash
# Menggunakan Homebrew
brew install gh
```

### Linux (Ubuntu/Debian)
```bash
# Install via apt
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null
sudo apt update
sudo apt install gh
```

**Verifikasi Instalasi:**
```bash
gh --version
```

---

## 🔐 Login & Autentikasi

### Login ke GitHub
```bash
# Login dengan browser (Recommended)
gh auth login

# Login dengan token
gh auth login --with-token < token.txt
```

### Pilihan Login:
1. **GitHub.com** (untuk akun publik)
2. **GitHub Enterprise Server** (untuk akun perusahaan)

### Verifikasi Login:
```bash
# Cek status login
gh auth status

# Lihat informasi user
gh api user
```

---

## 📁 Mengelola Repository

### Membuat Repository Baru
```bash
# Buat repo public
gh repo create nama-repo --public

# Buat repo private
gh repo create nama-repo --private

# Buat repo dengan deskripsi
gh repo create nama-repo --description "Deskripsi project saya"
```

### Clone Repository
```bash
# Clone repo sendiri
gh repo clone username/nama-repo

# Clone repo orang lain
gh repo clone owner/nama-repo
```

### Lihat Informasi Repository
```bash
# Lihat daftar repo
gh repo list

# Lihat detail repo
gh repo view username/nama-repo
```

---

## ⬆️ Push Project ke GitHub

### Skenario 1: Project Baru (Belum ada Git)

```bash
# 1. Inisialisasi Git
git init

# 2. Tambahkan file ke staging
git add .

# 3. Commit pertama
git commit -m "Initial commit"

# 4. Buat repository di GitHub
gh repo create nama-project --public --source=. --push

# 5. Set branch utama (opsional)
git branch -M main
```

### Skenario 2: Project Sudah Ada Git

```bash
# 1. Buat repository di GitHub
gh repo create nama-project --public

# 2. Tambahkan remote origin
git remote add origin https://github.com/username/nama-project.git

# 3. Push ke GitHub
git push -u origin main
```

### Skenario 3: Push Cepat

```bash
# Tambah, commit, dan push sekaligus
git add . && git commit -m "Update project" && git push
```

---

## 🌿 Mengelola Branch

### Operasi Branch
```bash
# Lihat semua branch
gh repo view --json defaultBranchRef

# Buat branch baru
git checkout -b feature/fitur-baru

# Push branch baru
git push -u origin feature/fitur-baru

# Hapus branch
gh api repos/:owner/:repo/git/refs/heads/branch-name -X DELETE
```

---

## 🔀 Pull Request

### Membuat Pull Request
```bash
# Buat PR dari branch saat ini
gh pr create --title "Judul PR" --body "Deskripsi perubahan"

# Buat PR dengan template
gh pr create --template

# Buat draft PR
gh pr create --draft
```

### Mengelola Pull Request
```bash
# Lihat daftar PR
gh pr list

# Lihat detail PR
gh pr view 123

# Merge PR
gh pr merge 123 --merge

# Close PR
gh pr close 123
```

---

## 💡 Tips & Trik

### ⚡ Shortcut Berguna

```bash
# Buka repo di browser
gh repo view --web

# Buka PR di browser
gh pr view --web

# Clone dan masuk ke direktori
gh repo clone owner/repo && cd repo

# Lihat issues
gh issue list
```

### 🔧 Konfigurasi

```bash
# Set editor default
gh config set editor "code"

# Set protokol default
gh config set git_protocol https

# Lihat semua konfigurasi
gh config list
```

### 📊 Informasi Cepat

| Perintah | Fungsi |
|----------|--------|
| `gh status` | Status repository |
| `gh repo list` | Daftar repository |
| `gh pr status` | Status PR |
| `gh issue list` | Daftar issues |

---

<div align="center">

## 🎉 Selamat! Anda Sudah Menguasai GitHub CLI

**Happy Coding! 🚀**

> 💡 **Pro Tip:** Gunakan `gh --help` untuk melihat bantuan lengkap setiap perintah

---

[![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com)
[![Documentation](https://img.shields.io/badge/Docs-GitHub%20CLI-blue?style=for-the-badge)](https://cli.github.com/manual/)

</div>
