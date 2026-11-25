# Microsoft Graph Integration Plan - DCEMS

Dokumen ini merinci rencana integrasi dengan Microsoft Graph API untuk pengiriman notifikasi email otomatis.

## 1. Tujuan Integrasi
Mengirimkan notifikasi email otomatis ke admin/user ketika sensor mendeteksi suhu atau kelembapan yang melewati ambang batas (threshold) yang telah ditentukan.

## 2. Arsitektur Alur Kerja
1. **Event Detection**: Backend Worker mendeteksi nilai sensor > Threshold.
2. **Message Construction**: Backend menyusun pesan email (Subject & Body) menggunakan data real-time.
3. **Graph Request**: Backend mengirim request `POST` ke endpoint Microsoft Graph untuk mengirim email via SMTP/Graph API.
4. **Delivery**: Microsoft mengirimkan email ke alamat tujuan yang terdaftar.

## 3. Spesifikasi Teknis API
- **Endpoint Utama**: `https://graph.microsoft.com/v1.0/users/{user_id}/sendMail`
- **Metode**: `POST`
- **Payload Contoh**:
  ```json
  {
    "message": {
      "subject": "⚠️ ALERT: Suhu Tinggi Terdeteksi",
      "body": {
        "contentType": "HTML",
        "content": "Suhu saat ini adalah 35°C (Melebihi batas 30°C). Mohon segera diperiksa."
      },
      "toRecipients": [
        {
          "emailAddress": {
            "address": "admin@company.com"
          }
        }
      ]
    }
  }
  ```

## 4. Autentikasi & Izin (OAuth 2.0)
- **App Registration**: Aplikasi harus didaftarkan di Azure Portal.
- **Permissions**: Memerlukan `Mail.Send` (Application atau Delegated).
- **Credentials**: Client ID, Tenant ID, dan Client Secret akan disimpan di environment variables backend.

## 5. Penanganan Kegagalan
- Jika API tidak dapat dijangkau, sistem akan mencatat log kegagalan di `KNOWN_ISSUES.md`.
- Sistem akan mencoba mengirim ulang (retry mechanism) sebanyak 3 kali dengan interval 1 menit.
