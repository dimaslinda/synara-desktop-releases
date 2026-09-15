# Synara Desktop Releases

[![Latest Release](https://img.shields.io/github/v/release/dimaslinda/synara-desktop-releases?style=flat-square&color=2563eb&label=Latest%20Release)](https://github.com/dimaslinda/synara-desktop-releases/releases/latest)
[![Platform](https://img.shields.io/badge/Platform-Windows%2010%20%7C%2011%20(x64)-0078d4?style=flat-square&logo=windows)](https://github.com/dimaslinda/synara-desktop-releases/releases/latest)
[![Ecosystem](https://img.shields.io/badge/Ecosystem-Digital%20Gradient%20HRIS-10b981?style=flat-square)](https://github.com/dimaslinda/synara-desktop-releases)
[![Type](https://img.shields.io/badge/Installer-NSIS%20Setup-orange?style=flat-square)](https://github.com/dimaslinda/synara-desktop-releases/releases/latest)

Repositori resmi distribusi berkas rilis dan *feed* pembaruan otomatis (**Auto-Update Feed**) untuk **Synara Desktop** — aplikasi pendamping pelacak waktu (*time tracker*) dan manajemen beban kerja karyawan yang terintegrasi langsung dengan ekosistem **Digital Gradient HRIS**.

---

## 📥 Unduh Cepat (Quick Download)

Untuk mendapatkan versi terbaru yang siap digunakan di komputer Windows:

| Berkas | Keterangan | Tautan Unduh |
| :--- | :--- | :--- |
| **Installer Versi Terbaru** | Installer resmi Windows (x64) tanpa perlu memilih versi manual | [⬇️ Unduh Synara-Desktop-Setup.exe](https://github.com/dimaslinda/synara-desktop-releases/releases/latest/download/Synara-Desktop-Setup.exe) |
| **Daftar Semua Rilis & Changelog** | Catatan perbaikan fitur, perubahan antarmuka, dan arsip rilis sebelumnya | [📋 Lihat Halaman Rilis GitHub](https://github.com/dimaslinda/synara-desktop-releases/releases) |

> **Catatan:** Jika organisasi Anda menyediakan portal web HRIS mandiri, Anda juga dapat mengunduh installer melalui menu portal di rute `https://<domain-hris-anda>/download/desktop`.

---

## ✨ Fitur Utama Synara Desktop

- **Floating Time Tracker & Edge Docking:** Widget mini melayang yang ringan dan responsif. Dapat ditempel mepet ke tepi atau sudut layar tanpa mengganggu jendela aplikasi kerja lainnya.
- **Sinkronisasi Real-Time dengan HRIS:** Jam kerja, durasi tugas, dan status pengerjaan tercatat langsung ke sistem Digital Gradient HRIS.
- **Proteksi Timer Otomatis:** Fitur pencegahan alarm malam dan jeda otomatis saat jam kerja berakhir sesuai kebijakan jadwal kerja server.
- **Dashboard & Kanban Task Execution:** Pantau daftar pekerjaan harian, geser status tugas (*Kanban*), dan kelola beban kerja (*workload*) secara mandiri.
- **Integrasi ESS (Employee Self-Service):** Akses cepat pengajuan cuti, izin, lembur, dan tukar jadwal shift langsung dari perangkat desktop.
- **Silent Background Auto-Update:** Aplikasi otomatis mendeteksi ketersediaan versi baru di latar belakang tanpa mengganggu alur kerja pengguna.

---

## 💻 Panduan Instalasi (Windows 10 / 11)

Ikuti langkah-langkah berikut untuk memasang aplikasi di komputer Anda:

1. **Unduh Installer:**  
   Klik tautan [Synara-Desktop-Setup.exe](https://github.com/dimaslinda/synara-desktop-releases/releases/latest/download/Synara-Desktop-Setup.exe) dan simpan berkas di komputer Anda.
2. **Jalankan Berkas Setup:**  
   Buka berkas `Synara-Desktop-Setup.exe` yang telah diunduh.
3. **Peringatan Windows SmartScreen (Jika Muncul):**  
   Karena berkas installer dirilis untuk lingkungan internal:
   - Klik **More info** (*Informasi selengkapnya*).
   - Klik tombol **Run anyway** (*Tetap jalankan*).
4. **Pilih Lokasi Pemasangan:**  
   Tentukan direktori instalasi yang diinginkan dan ikuti wizard hingga selesai (ikon pintasan *Desktop* dan *Start Menu* akan dibuat secara otomatis).
5. **Masuk ke Akun HRIS:**  
   Buka aplikasi **Synara Desktop**, periksa alamat URL server HRIS pada menu pengaturan jika diperlukan, lalu masuk menggunakan kredensial akun Digital Gradient HRIS Anda.

---

## 🔄 Mekanisme Pembaruan Aplikasi (Auto-Update)

Synara Desktop dilengkapi modul pembaruan otomatis menggunakan teknologi `electron-updater`:

- **Pembaruan Otomatis (Background):**  
  Setiap kali aplikasi berjalan, sistem akan memeriksa rilis baru secara anonim ke repositori ini. Jika versi baru ditemukan, paket pembaruan diunduh di latar belakang dan akan otomatis terpasang saat aplikasi ditutup atau dimulai ulang (*restart*).
- **Pemeriksaan Manual:**  
  Anda dapat memeriksa ketersediaan versi secara mandiri melalui menu:  
  **Pengaturan** → **Pembaruan Aplikasi** → **Cek Pembaruan**.

---

## 🛠️ Informasi Teknis untuk Administrator & Pengembang (DevOps)

Repositori ini bertindak sebagai **Public Distribution Gateway** yang terpisah dari repositori kode sumber utama (`digitalgradient-desktop`):

```mermaid
flowchart LR
    subgraph Private["Repositori Privat"]
        DevCode["Source Code (Electron + React)"] --> Build["npm run release"]
    end

    subgraph Public["Repo Publik: synara-desktop-releases"]
        Build --> Draft["Buat Rilis GitHub"]
        Draft --> Files["Assets:\n- latest.yml\n- Synara-Desktop-Setup-<ver>.exe\n- Synara-Desktop-Setup.exe (Alias)\n- *.blockmap"]
    end

    subgraph Clients["Klien Pengguna"]
        Files --> Direct["Portal HRIS: /download/desktop"]
        Files --> Updater["Runtime App: electron-updater"]
    end
