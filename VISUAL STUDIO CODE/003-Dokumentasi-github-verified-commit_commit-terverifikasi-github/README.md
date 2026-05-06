# 🛡️ Setup SSH Commit Signing untuk GitHub

### ✨ _Panduan Lengkap Mendapatkan Badge "Verified" di Setiap Commit_

> 🎯 **Tujuan:** Mengatur agar setiap commit yang dilakukan dari terminal lokal (VS Code, Git Bash, PowerShell) mendapatkan badge hijau **"Verified"** di GitHub — sama seperti commit yang dibuat langsung di web.

---

### 📑 Daftar Isi

| No | Bagian | Deskripsi |
|----|--------|-----------|
| 📖 | [Latar Belakang](#latar-belakang) | Mengapa commit saya tidak "Verified"? |
| 🔑 | [Authentication vs Signing Key](#konsep-key) | Memahami dua peran satu kunci SSH |
| ⚖️ | [Mengapa SSH, Bukan GPG?](#mengapa-ssh) | Perbandingan dua metode signing |
| 🌐 | [Tahap 1 — Setup di Web GitHub](#tahap-1) | Mendaftarkan Signing Key |
| ⚠️ | [Troubleshooting](#troubleshooting) | Mengatasi error "Key is already in use" |
| 💻 | [Tahap 2 — Konfigurasi Terminal](#tahap-2) | 3 perintah ajaib yang wajib dijalankan |
| ✅ | [Verifikasi](#verifikasi) | Memastikan semuanya berhasil |

---

<a name="latar-belakang"></a>
## 📖 Latar Belakang — Mengapa Commit Saya Tidak "Verified"?

> _"Kenapa commit yang saya buat langsung di web GitHub ada tanda ✅ Verified, tapi commit dari terminal di laptop saya tidak ada?"_

Pertanyaan inilah yang memulai sesi eksplorasi ini. Ternyata jawabannya cukup sederhana:

### 🌐 Commit dari Web GitHub → **Otomatis Verified** ✅

Ketika kamu mengedit file langsung di browser GitHub, GitHub bertindak sebagai **"notaris digital"** — mereka secara otomatis menandatangani commit itu dengan kunci internal mereka sendiri.

### 💻 Commit dari Terminal Lokal → **Tidak Verified** ❌

Aplikasi Git di laptopmu hanya mencatat `user.name` dan `user.email`, tapi **tidak menyertakan bukti kriptografi** bahwa commit itu benar-benar berasal dari pemilik akun GitHub yang sah.

> [!TIP]
> 💡 **Analogi Mudah Dipahami**
>
> | | Commit dari Web | Commit dari Terminal |
> |---|---|---|
> | 📝 | Surat resmi **berstempel kantor pos** | Surat biasa yang **hanya ditulis nama pengirim** |
> | 🔒 | Siapa pun tahu ini asli | Siapa pun bisa meniru |
> | ✅ | Verified | ❌ Tidak Verified |

### 💡 Jadi, Apa Solusinya?

Kita perlu mengaktifkan fitur **Commit Signing** — fitur yang membuat Git di laptop secara otomatis "menandatangani" setiap commit menggunakan kunci kriptografi pribadimu. Setelah setup selesai, **semua commit** (baik dari web maupun terminal) akan memiliki badge "Verified"! 🎉

---

<a name="konsep-key"></a>
## 🔑 Konsep — Authentication Key vs Signing Key

> [!NOTE]
> 📌 **Konsep Kunci:** Satu SSH Key yang sama bisa digunakan untuk **dua peran berbeda** di GitHub, namun harus **didaftarkan secara terpisah**.

### 1️⃣ Authentication Key — _"Kartu Akses Masuk Gedung"_ 🏢

```
🎯 Fungsi    → Memberi izin laptop untuk push, pull, clone via SSH
📌 Status    → ✅ Sudah terdaftar (kamu sudah bisa git push)
🔐 Analogi   → Kartu akses yang membuktikan kamu BERHAK MASUK
               tapi tidak membuktikan dokumen di dalamnya milikmu
```

### 2️⃣ Signing Key — _"Stempel Notaris"_ 📜

```
🎯 Fungsi    → Menandatangani setiap commit sebagai bukti kepemilikan
📌 Status    → ❌ Belum terdaftar (inilah penyebab tidak Verified!)
🔐 Analogi   → Stempel yang membuktikan dokumen itu
               BENAR-BENAR dibuat dan disetujui olehmu
```

> [!IMPORTANT]
> 🔔 **Kamu TIDAK perlu membuat kunci baru!** Kunci SSH yang sudah ada (untuk `push`) bisa langsung didaftarkan ulang dengan peran tambahan sebagai *Signing Key*. GitHub mengizinkan satu kunci terdaftar dua kali **asalkan tipenya berbeda**.

---

<a name="mengapa-ssh"></a>
## ⚖️ Mengapa SSH Key dan Bukan GPG Key?

Dulu, GPG adalah satu-satunya cara. Sekarang? **SSH jauh lebih baik** untuk kebutuhan kita:

| Aspek | GPG Key 🔴 | SSH Key 🟢 |
|-------|:----------:|:----------:|
| Perlu install software tambahan? | ✅ Ya _(Gpg4win)_ | ❌ Tidak perlu |
| Sudah punya kuncinya? | ❌ Harus buat baru | ✅ Sudah ada! |
| Tingkat kesulitan setup | 🔴 Tinggi | 🟢 Rendah |
| Sering error saat konfigurasi? | 🔴 Ya | 🟢 Jarang |
| Hasil akhir (badge Verified) | ✅ Sama | ✅ Sama |

> [!TIP]
> 🏆 **Kesimpulan:** GitHub menambahkan dukungan SSH Signing pada akhir 2022 karena banyak developer mengeluh GPG terlalu ribet. Karena kita sudah punya SSH Key, gunakan yang sudah ada — **hasilnya identik!**

---

<a name="tahap-1"></a>
## 🌐 Tahap 1 — Daftarkan Signing Key di Web GitHub

> **⏱️ Estimasi waktu:** 2 menit | **📋 Prasyarat:** Sudah bisa `git push` dari terminal

**Langkah-langkah:**

**1.** 📋 **Salin kunci publik SSH milikmu.**

Buka terminal dan jalankan:
```bash
cat ~/.ssh/id_ed25519_azier001.pub
```
Salin **seluruh baris** output yang muncul.

---

**2.** 🌐 **Buka halaman pengaturan SSH di GitHub.**

👉 Navigasi ke: [**Settings → SSH and GPG keys**](https://github.com/settings/keys)

---

**3.** ➕ **Klik tombol hijau `New SSH key`.**

---

**4.** ✏️ **Isi kolom `Title`** dengan nama deskriptif.

> Contoh: `Laptop Windows - Signing` atau `Kunci Tanda Tangan`

---

**5.** 🚨 **LANGKAH PALING KRUSIAL!**

> [!CAUTION]
> 🔴 **WAJIB DIUBAH!** Di bawah kolom Title, ada dropdown **Key type** yang secara bawaan menampilkan `"Authentication Key"`. Klik dropdown tersebut dan **UBAH menjadi `"Signing Key"`**.
>
> Jika langkah ini terlewat, kamu akan mendapat **error**! _(Lihat bagian Troubleshooting di bawah.)_

---

**6.** 📋 **Paste** kunci publik yang sudah disalin ke kotak **Key**.

---

**7.** ✅ **Klik tombol hijau `Add SSH key`.**

---

🎊 **Selesai!** Kunci SSH-mu sekarang terdaftar dengan dua peran:

```
✅ Authentication Key  →  untuk push/pull (sudah ada sebelumnya)
✅ Signing Key         →  untuk badge Verified (baru ditambahkan!)
```

---

<a name="troubleshooting"></a>
## ⚠️ Troubleshooting — Error "Key is already in use"

> [!WARNING]
> 🐛 **Error ini benar-benar terjadi** saat proses setup pertama kali! Berikut kronologinya:

```
❌  Error Message:  "Key is already in use"
```

### 🔍 Penyebab

Lupa mengubah dropdown **Key type** dari `"Authentication Key"` → `"Signing Key"`. Karena kunci yang sama sudah terdaftar sebagai Authentication Key, GitHub menolak pendaftaran duplikat dengan tipe yang sama.

### ✅ Solusi

Ulangi dari Langkah 3 dan **pastikan langkah 5 tidak terlewat** — ubah Key type menjadi **"Signing Key"** sebelum menekan "Add SSH key".

> 📌 GitHub mengizinkan **satu kunci = dua pendaftaran**, asalkan tipe-nya berbeda!

---

<a name="tahap-2"></a>
## 💻 Tahap 2 — Konfigurasi Git di Terminal (Lokal)

> **⏱️ Estimasi waktu:** 1 menit | **📋 Prasyarat:** Tahap 1 sudah selesai

Ada **3 perintah ajaib** yang perlu dijalankan. Cukup **satu kali saja** — berlaku selamanya untuk semua repository.

---

### 🔧 Perintah 1 — Mengubah Format Tanda Tangan

```bash
git config --global gpg.format ssh
```

> 📖 **Penjelasan kata per kata:**
>
> | Bagian | Arti |
> |--------|------|
> | `git config` | Perintah untuk mengubah pengaturan Git |
> | `--global` | Berlaku untuk **semua** repository di laptop, bukan cuma satu |
> | `gpg.format` | Nama pengaturan yang mengontrol format tanda tangan |
> | `ssh` | Nilai baru — memberitahu Git untuk pakai SSH (bukan GPG) |

> [!NOTE]
> 💡 **Kenapa penting?** Tanpa perintah ini, Git secara default akan mencari kunci GPG yang tidak kita miliki, dan proses commit bisa gagal dengan error yang membingungkan.

---

### 🔧 Perintah 2 — Menentukan Lokasi Kunci

```bash
git config --global user.signingkey "C:\Users\azier\.ssh\id_ed25519_azier001.pub"
```

> 📖 **Penjelasan kata per kata:**
>
> | Bagian | Arti |
> |--------|------|
> | `user.signingkey` | Pengaturan lokasi file kunci untuk signing |
> | `"C:\Users\...pub"` | Path lengkap ke file kunci publik SSH milikmu |

> [!NOTE]
> 💡 **Kenapa perlu path eksplisit?** Di satu laptop bisa ada banyak SSH Key (untuk akun berbeda, platform berbeda). Dengan menentukan path, Git tahu **persis** kunci mana yang dipakai.
>
> ⚠️ **Sesuaikan path di atas** dengan lokasi SSH Key di laptopmu sendiri!

---

### 🔧 Perintah 3 — Mengaktifkan Auto-Signing

```bash
git config --global commit.gpgsign true
```

> 📖 **Penjelasan kata per kata:**
>
> | Bagian | Arti |
> |--------|------|
> | `commit.gpgsign` | Pengaturan apakah commit otomatis ditandatangani |
> | `true` | Aktifkan! Setiap `git commit` akan auto-signed |

> [!TIP]
> 💡 **Perbedaan sebelum & sesudah:**
> ```bash
> # ❌ SEBELUM (tanpa auto-sign) — harus ketik -S setiap saat
> git commit -S -m "pesan commit"
>
> # ✅ SESUDAH (dengan auto-sign) — otomatis ditandatangani!
> git commit -m "pesan commit"
> ```

---

### 📋 Ringkasan — Salin & Jalankan Sekaligus

```bash
git config --global gpg.format ssh
git config --global user.signingkey "C:\Users\azier\.ssh\id_ed25519_azier001.pub"
git config --global commit.gpgsign true
```

> ☝️ Ketiga perintah ini **cukup dijalankan sekali seumur hidup** (kecuali kamu ganti laptop atau ganti kunci SSH).

---

<a name="verifikasi"></a>
## ✅ Verifikasi — Cara Memastikan Setup Berhasil

### 1️⃣ Cek Konfigurasi Git

```bash
git config --global --list
```

Pastikan **3 baris ini** muncul di output:
```
gpg.format=ssh                                          ← ✅
user.signingkey=C:\Users\azier\.ssh\id_ed25519_azier001.pub  ← ✅
commit.gpgsign=true                                     ← ✅
```

### 2️⃣ Buat Commit Baru

```bash
git add .
git commit -m "test: verify signed commit"
git push origin main
```

### 3️⃣ Periksa di GitHub

Buka halaman **Commits** di repositorimu → commit terbaru seharusnya memiliki badge:

```
┌──────────┐
│ Verified │  ← 🎉 Muncul!
└──────────┘
```

---

> 📝 **Catatan Akhir:**
> Dokumentasi ini dibuat pada **6 Mei 2026** berdasarkan pengalaman setup langsung di **Windows 11** dengan Git dan GitHub. Langkah-langkah mungkin sedikit berbeda di macOS/Linux, namun konsep dasarnya tetap sama.
