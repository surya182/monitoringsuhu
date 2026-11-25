# UI/UX Wireframes - DCEMS

Dokumen ini berisi deskripsi detail tata letak dan alur kerja antarmuka pengguna (UI) untuk sistem DCEMS.

## 1. Dashboard Utama (Overview)
Dashboard adalah layar utama yang memberikan ringkasan kondisi suhu dan kelembapan secara real-time.

- **Header**: 
  - Judul Aplikasi (DCEMS).
  - Status Koneksi Serial (Indikator Hijau/Merah).
  - Jam Sistem.
- **Widget Ringkasan (Top Cards)**:
  - Suhu Terkini (Celsius) - Besar & Jelas.
  - Kelembapan Terkini (%) - Besar & Jelas.
  - Status Alert Terakhir (Misal: "Normal" atau "Warning").
- **Grafik Realtime**:
  - Grafik garis (Line Chart) menggunakan Recharts untuk menampilkan tren Suhu dan Kelembapan dalam 30 menit terakhir.
  - Sumbu X: Waktu (Real-time).
  - Sumbu Y: Nilai (Celsius/%).
- **Log Aktivitas Terkini**:
  - Tabel sederhana yang menampilkan 5-10 pembacaan terakhir beserta timestamp-nya.

## 2. Layar Konfigurasi Alert (Alert Configuration)
Layar untuk mengatur ambang batas (threshold) peringatan.

- **Form Input Ambang Batas**:
  - Input Suhu Maksimum (Numeric).
  - Input Suhu Minimum (Numeric).
  - Input Kelembapan Maksimum (Numeric).
  - Input Kelembapan Minimum (Numeric).
- **Tombol Aksi**:
  - Simpan Konfigurasi.
  - Reset ke Default.
- **Visual Feedback**:
  - Notifikasi sukses/gagal setelah menyimpan konfigurasi.

## 3. Layar Manajemen Sensor & Port (Sensor Management)
Layar untuk konfigurasi koneksi hardware.

- **Pemilihan Port Serial**:
  - Dropdown untuk memilih Port COM yang tersedia (misal: COM1, COM2, dst).
  - Input untuk Baud Rate (Default: 9600).
  - Input untuk Data Bits (Default: 8).
  - Input untuk Parity (Dropdown: None, Even, Odd).
  - Input untuk Stop Bits (Dropdown: 1, 2).
- **Tombol Koneksi**:
  - Hubungkan (Connect).
  - Putuskan (Disconnect).
  - Test Koneksi.

## 4. Alur Kerja Notifikasi (Notification Flow)
1. **Trigger**: Sensor mengirim data > Backend memproses > Nilai melebihi Threshold.
2. **Action**: Sistem mengirim permintaan ke Microsoft Graph API.
3. **Output**: User menerima email notifikasi berisi detail (Sensor ID, Nilai saat ini, Waktu kejadian).
