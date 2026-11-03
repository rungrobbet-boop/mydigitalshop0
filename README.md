# MyDigitalShop - Modern Retail & POS System

Sistem Manajemen Retail Terintegrasi (Point of Sale, Akuntansi Double-Entry, Inventori FIFO, dan Landing Page Katalog) yang dirancang untuk **semua jenis bisnis retail modern** (Toko Bangunan, Supermarket, Minimarket, F&B, Fashion, Elektronik, dll). 

Dibangun dengan arsitektur modern, sangat cepat, hemat biaya server (Serverless), dan siap di-deploy untuk kebutuhan *White-Label* (Multi-Tenant).

## 🚀 Teknologi yang Digunakan
- **Frontend:** React + Vite (Landing Page & Dashboard) + Alpine.js (Kasir & Akuntansi)
- **Styling:** Tailwind CSS
- **Database Hybrid:** 
  - Google Cloud Firestore (Master Data Katalog: `products`, `customers`, `suppliers`)
  - Firebase Realtime Database (Transaksi POS, Shift Kasir, Stok, Jurnal Akuntansi)
- **Hosting & Backend:** Cloudflare Pages & Serverless Functions

## ✨ Fitur Utama (Universal Retail)
1. **Kasir (POS):** Multi-scan barcode, Harga Bertingkat (Ecer/Partai/Agen), Qty Lock, Anti-overselling.
2. **Akuntansi Otomatis:** Double-entry, 3-digit COA, FIFO HPP, Auto Jurnal POS/Void, Laporan Laba Rugi, Neraca, dan Arus Kas.
3. **Manajemen Inventori:** Stok real-time, Import CSV massal, Penerimaan Barang, dan Stock Opname.
4. **Landing Page Dinamis:** Katalog produk interaktif, Top Brand, dan integrasi Checkout.
5. **Keamanan:** PIN Supervisor untuk aksi destruktif, proteksi Password Admin.
6. **Multi-Tenant (White-Label):** Konfigurasi nama toko, logo, tema warna, dan kategori produk diatur secara dinamis via `site_config` di Firebase tanpa perlu mengubah kode.

## 🛠️ Persiapan Instalasi (White-Label / Multi-Tenant)

Sesuai standar keamanan, **JANGAN PERNAH** menaruh API Key di dalam kode (hardcode). Semua konfigurasi Firebase dibaca dari Environment Variables.

1. **Clone Repo & Install Dependensi:**
   ```bash
   git clone https://github.com/username/mydigitalshop0.git
   cd mydigitalshop0
   npm install
Setup Firebase Config (Wajib):
Buat file .env di root folder proyek, lalu isi dengan kredensial Firebase project Anda (setiap kloningan WAJIB menggunakan Firebase Project yang berbeda):

env
VITE_FIREBASE_API_KEY="AIzaSy..."
VITE_FIREBASE_AUTH_DOMAIN="project-anda.firebaseapp.com"
VITE_FIREBASE_DATABASE_URL="https://project-anda-default-rtdb.asia-southeast1.firebasedatabase.app"
VITE_FIREBASE_PROJECT_ID="project-anda"
VITE_FIREBASE_STORAGE_BUCKET="project-anda.appspot.com"
VITE_FIREBASE_MESSAGING_SENDER_ID="1234567890"
VITE_FIREBASE_APP_ID="1:1234:web:abcd"
Jalankan Secara Lokal:


Untuk mempermudah konversi penjualan UMKM, pelanggan tidak boleh dipaksa mengisi formulir login password yang panjang saat hendak memesan barang.
bash
npm run dev
☁️ Deployment ke Cloudflare Pages
Hubungkan repository GitHub ini ke Cloudflare Pages.

Gunakan pengaturan build berikut:

Framework preset: Vite

Build command: npm run build

Build output directory: dist

Masukkan variabel .env (VITE_FIREBASE_...) di menu Settings > Environment Variables di Cloudflare.

Pastikan fungsi Serverless (folder functions/) terdeteksi otomatis untuk menangani proses backend (Payment, Ongkir, Jurnal, dll).

🔒 Aturan Arsitektur (Penting untuk Developer/AI)
Dilarang mengubah struktur folder inti.

Dilarang meng-hardcode API Key atau URL Firebase (Gunakan .env).

Dilarang mengubah logika Double-Entry, Void, Reversal, dan Shift tanpa persetujuan Owner.

Skala data besar (3.000+ produk) wajib menggunakan Cursor-Based Pagination, bukan onSnapshot untuk katalog utama.

Semua nama toko, logo, warna, dan teks wajib dibaca dari site_config (Firebase), dilarang hardcode di HTML.
