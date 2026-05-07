# 🔧 Kernel Builder - KernelSU Next for Poco F1 (Beryllium)

Build kernel dengan KernelSU Next otomatis via GitHub Actions.

---

## 📋 Persiapan

### Yang Kamu Butuhkan:
- Akun GitHub (gratis)
- File `boot.img` dari Qassa ROM (untuk diambil ramdisk-nya)
- Browser

---

## 🚀 Cara Pakai (Step by Step)

### Step 1 — Buat Repository GitHub

1. Buka **https://github.com/new**
2. Isi nama repo: `kernel-poco-f1-ksun`
3. Set **Private** (opsional)
4. Klik **"Create repository"**

---

### Step 2 — Upload File Ini ke GitHub

Setelah repo dibuat, upload semua file berikut:

```
kernel-poco-f1-ksun/
├── .github/
│   └── workflows/
│       └── build-kernel.yml   ← workflow utama
├── scripts/
│   └── boot.img               ← boot.img dari Qassa ROM KAMU
└── README.md
```

**Cara upload:**
1. Di halaman repo, klik **"uploading an existing file"**
2. Drag & drop semua file
3. Klik **"Commit changes"**

> ⚠️ **PENTING:** File `boot.img` harus kamu upload ke folder `scripts/`

---

### Step 3 — Jalankan Build

1. Klik tab **"Actions"** di repo kamu
2. Klik **"Build Kernel KSUN - Poco F1 (Beryllium)"**
3. Klik tombol **"Run workflow"** (kanan atas)
4. Isi parameter (atau biarkan default):

| Parameter | Default | Keterangan |
|-----------|---------|------------|
| KERNEL_SOURCE | `https://github.com/Tantangan45/android_kernel_xiaomi_beryllium` | Source kernel beryllium |
| KERNEL_BRANCH | `ten` | Branch Android 10 |
| KERNEL_DEFCONFIG | `beryllium_defconfig` | Config untuk Poco F1 |
| KSUN_BRANCH | `next` | Branch KernelSU Next |

5. Klik **"Run workflow"** (hijau)
6. Tunggu **45-90 menit**

---

### Step 4 — Download Hasil Build

1. Setelah build selesai (✅ hijau), klik job-nya
2. Scroll ke bawah ke bagian **"Artifacts"**
3. Download **`boot-KSUN-Beryllium-X`**
4. Extract ZIP → kamu akan dapat file `boot-KSUN-beryllium-YYYYMMDD.img`

---

### Step 5 — Flash ke Poco F1

#### Via Fastboot (Rekomendasi):
```
1. Aktifkan USB Debugging + OEM Unlock di HP
2. Reboot ke Fastboot: tahan Vol- + Power bersamaan
3. Sambungkan ke PC via USB
4. Buka Command Prompt di folder tempat boot.img
5. Jalankan:
   fastboot flash boot boot-KSUN-beryllium-*.img
   fastboot reboot
```

#### Via Recovery (TWRP):
```
1. Copy boot.img ke HP
2. Reboot ke TWRP
3. Install → pilih boot.img → swipe to flash
4. Reboot System
```

---

### Step 6 — Setup KernelSU Next

1. Download KernelSU Next APK:
   **https://github.com/rifsxd/KernelSU-Next/releases**
2. Install APK di HP
3. Buka app → harusnya sudah terdeteksi ✅
4. Kalau masih error, cek di tab **Troubleshooting** di bawah

---

## ❓ Troubleshooting

### Error: "KernelSU Next v2 signature not found"
→ Patch KSUN belum masuk. Pastikan step patch di workflow berhasil.
→ Cek log Actions, cari bagian "Patch KernelSU Next"

### Error: Build failed / compile error
→ Download `build-log-failed` dari Artifacts
→ Cari baris yang ada tulisan `error:` 
→ Kemungkinan source kernel tidak kompatibel, coba ganti KERNEL_SOURCE

### Boot loop setelah flash
→ Flash ulang boot.img original Qassa ROM
→ `fastboot flash boot boot_original.img`

### KernelSU app tidak terbuka / crash
→ Pastikan versi APK sesuai dengan versi KSUN yang di-patch

---

## 📱 Info Device

| Item | Detail |
|------|--------|
| Device | Poco F1 (Beryllium) |
| Chipset | Snapdragon 845 (SDM845) |
| Kernel Base | Linux 4.9.x |
| Android | 10 (Q) |
| ROM Target | Qassa ROM |

---

## 🔗 Link Penting

- KernelSU Next: https://github.com/rifsxd/KernelSU-Next
- Kernel Source: https://github.com/Tantangan45/android_kernel_xiaomi_beryllium
- ADB/Fastboot Tools: https://developer.android.com/tools/releases/platform-tools
