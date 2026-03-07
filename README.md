# 🚀 Billions Network: Verified Agent Identity Tutorial

Panduan ini akan membimbing kamu langkah demi langkah untuk melakukan verifikasi **Agent Identity** pada Billions Network menggunakan fitur **GitHub Actions**.

---

## 📋 Persiapan

Sebelum memulai, pastikan kamu memiliki:

- Akun **GitHub** yang aktif
- Akun **Billions Network** yang sudah terdaftar
- Browser (Chrome / Kiwi / Mises)

---

## 🛠 Langkah-Langkah Eksekusi

### 1️⃣ Fork Repository

1. Buka repository berikut: https://github.com/BillionsNetwork/verified-agent-identity
2. Klik tombol **Fork** di pojok kanan atas untuk menyalin repository ke akun GitHub kamu.

---

### 2️⃣ Membuat File Identitas (.json)

Di dalam repository hasil fork kamu:

**Add file → Create new file**

Gunakan format nama file:

```

nama-anda.json

```

Contoh:

```

bang-pateng.json

````

Isi file:

```json
{
  "identity": "Nama_Agen_Kamu",
  "agent": "Billions"
}
````

Contoh:

```json
{
  "identity": "Bang Pateng",
  "agent": "Billions"
}
```

Klik **Commit changes** untuk menyimpan.

---

### 3️⃣ Setup GitHub Actions

1. Masuk ke tab **Actions** di repository kamu
2. Klik **Set up a workflow yourself**.

Hapus semua kode yang ada lalu ganti dengan kode berikut:

File lokasi:

```
.github/workflows/main.yml
```

Isi file:

```yaml
name: Verify Human Identity

on:
  workflow_dispatch:
    inputs:
      agent_name:
        description: 'Nama Agen'
        required: true
        default: 'Nama_Agen_Kamu'
      agent_description:
        description: 'Deskripsi Agen'
        required: true
        default: 'AI Agent'

jobs:
  verify:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repo
        uses: actions/checkout@v3

      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '20'

      - name: Step 1 - Install ClawHub skill
        run: npx clawhub@latest install verified-agent-identity

      - name: Install script dependencies
        run: |
          cd scripts
          npm install

      - name: Step 2 - Create new Ethereum Identity
        run: node scripts/createNewEthereumIdentity.js

      - name: Step 3 - Link Human to Agent
        run: |
          node scripts/manualLinkHumanToAgent.js --challenge '{"name": "Nama_Agen_Kamu", "description": "AI Agent"}'
```

⚠️ **PENTING**

Ganti bagian berikut:

```
Nama_Agen_Kamu
```

Dengan nama yang **sama persis dengan file `.json` yang kamu buat**.

Contoh:

```
Bang Pateng
```

Klik **Commit changes**.

---

### 4️⃣ Menjalankan Workflow Verifikasi

Masuk ke tab **Actions**.

Pilih workflow:

```
Verify Human Identity
```

Klik tombol:

```
Run workflow
```

Klik lagi **Run workflow** untuk menjalankan.

Tunggu sekitar **1–2 menit** sampai muncul tanda:

```
✅ Success
```

---

### 5️⃣ Finalisasi: Binding ke Profil Billions

Klik workflow yang berhasil (centang hijau).

Klik job:

```
verify
```

Buka bagian:

```
Step 3 - Link Human to Agent
```

Di dalam log akan muncul **URL Verifikasi**.

Salin link tersebut lalu buka di browser.

---

### 6️⃣ Konfirmasi di Dashboard Billions

Login ke dashboard **Billions Network**.

Klik tombol:

```
Bind Agent
```

Setelah selesai, agent kamu akan muncul di profil.

---

## ⚠️ Catatan Tambahan

### Sinkronisasi Nama

Nama di file `.json` dan nama di `main.yml` harus **identik**.

Jika berbeda → verifikasi akan gagal.

---

### Link Expired

Link verifikasi memiliki batas waktu.

Jika link tidak bisa dibuka, jalankan kembali:

```
Run workflow
```

Untuk mendapatkan link baru.

---

### Keamanan

Jangan membagikan:

* Private key
* Token
* Informasi sensitif dari log workflow

kepada siapapun.

---

## 🎉 Selesai

Agent kamu sekarang sudah berhasil diverifikasi di **Billions Network**.

Semoga berhasil 🚀

```

Kalau kamu mau, saya juga bisa buatkan **versi README yang lebih profesional (dengan badge, gambar, dan step visual)** supaya repo GitHub kamu terlihat **lebih legit dan mudah diikuti**.
```
