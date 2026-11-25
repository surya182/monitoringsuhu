# Arsitektur Sistem - DCEMS

Dokumen ini menjelaskan struktur arsitektur teknis aplikasi Data Center Environmental Monitoring System (DCEMS).

## Gambaran Umum Arsitektur
DCEMS menggunakan arsitektur **Decoupled Layered Architecture** yang memisahkan tanggung jawab antara pengambilan data (Hardware Interaction), pengolahan data (Backend), dan tampilan (Frontend).

## Diagram Komponen Utama

### 1. Layer Perangkat Keras (Data Source)
- **Sensor Serial:** Perangkat fisik yang mengirimkan data suhu dan kelembapan melalui komunikasi serial (USB-to-TTL).
- **Serial Port (COMx):** Jalur komunikasi fisik yang akan dideteksi secara dinamis oleh sistem.

### 2. Layer Backend (Core System)
Backend dibagi menjadi dua bagian utama agar tidak saling mengganggu (Asynchronous Processing):

#### **A. .NET Worker Service (The Ingestor)**
- **Tanggung Jawab:** Berjalan terus-menerus di latar belakang (Background Process).
- **Fungsi Utama:**
  - Mendengarkan koneksi serial port.
  - Melakukan parsing string `*A18.50#*B59.90#` menjadi objek data.
  - Melakukan *sampling* data setiap 10 detik (sesuai konfigurasi).
  - Melakukan validasi ambang batas (Thresholding).
  - Menyimpan data ke PostgreSQL melalui Entity Framework Core.
  - Mengirim notifikasi ke Microsoft Graph API jika terjadi *alert*.
  - Mendorong data ke **SignalR Hub** untuk pembaruan *realtime*.

#### **B. ASP.NET Core Web API (The Gateway)**
- **Tanggung Jawab:** Menyediakan RESTful API untuk frontend dan manajemen sistem.
- **Fungsi Utama:**
  - Autentikasi dan Otorisasi (JWT).
  - Penyediaan data konfigurasi sensor.
  - Penyajian data historis dari PostgreSQL.
  - Manajemen log peringatan.

### 3. Layer Komunikasi Realtime
- **SignalR Hub:** Berfungsi sebagai *message broker* internal untuk mendorong data dari Worker Service langsung ke klien Frontend yang sedang aktif.

### 4. Layer Frontend (The Dashboard)
- **React + TypeScript:** Aplikasi web single-page (SPA).
- **SignalR Client:** Mendengarkan perubahan data secara *realtime* untuk memperbarui grafik tanpa *refresh*.
- **Recharts:** Merender data historis ke dalam grafik garis/bar.

## Alur Data (Data Flow)

1. **Data Ingestion:**
   `Sensor` -> `Worker Service (Serial Read)` -> `Parser` -> `PostgreSQL` & `SignalR Hub`.
2. **Alerting:**
   `Worker Service` -> `Threshold Check` -> `Microsoft Graph API` -> `Email User`.
3. **User Interaction:**
   `User (Browser)` -> `Web API` -> `PostgreSQL` (Data History).
   `User (Browser)` <-> `SignalR Hub` <-> `Worker Service` (Realtime Update).

## Teknologi Pendukung
- **ORM:** Entity Framework Core (untuk abstraksi database).
- **Caching:** (Opsional) In-memory cache untuk konfigurasi sensor yang sering diakses.
- **Logging:** Serilog untuk mencatat log sistem dan error serial.

## Pertimbangan Keamanan
- **Isolation:** Worker Service berjalan sebagai layanan sistem, Web API berjalan sebagai web server.
- **Network:** Aplikasi hanya dapat diakses melalui LAN/Intranet.
- **Secrets:** Kredensial Microsoft Graph dan Database akan disimpan di `appsettings.json` atau Environment Variables (tidak di-commit ke Git).
