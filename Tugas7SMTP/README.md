# Komprehensif SMTP (Simple Mail Transfer Protocol)

## Konsep Dasar SMTP

### Definisi
SMTP adalah protokol standar untuk mengirim email antar server, mentransfer pesan elektronik melalui internet.

### Proses Dasar
1. Koneksi server pengirim dan penerima
2. Autentikasi (opsional)
3. Transfer data email
4. Konfirmasi pengiriman

## Konfigurasi SMTP di Nginx

### Contoh Konfigurasi Dasar
```nginx
# Konfigurasi proxy SMTP melalui Nginx
mail {
    server_name mail.example.com;
    
    smtp_server {
        listen 25;
        protocol smtp;
        
        max_connections 100;
        timeout 60s;
        
        auth_methods plain login;
        
        ssl_certificate /path/to/smtp.crt;
        ssl_certificate_key /path/to/smtp.key;
    }
}
```

### Konfigurasi Keamanan SMTP
```nginx
# Pencegahan spam dan keamanan SMTP
mail {
    smtp_server {
        # Batasan rate
        limit_req zone=smtp_limit burst=50;
        
        # Pembatasan ukuran email
        max_message_size 10m;
        
        # Whitelist IP
        allow 192.168.1.0/24;
        deny all;
    }
}
```

## Praktik Terbaik
- Aktifkan TLS/SSL
- Gunakan autentikasi
- Terapkan SPF, DKIM, dan DMARC
- Batasi koneksi dan ukuran pesan

## Troubleshooting
- Periksa log email: `/var/log/mail.log`
- Gunakan `telnet` untuk tes koneksi
- Verifikasi sertifikat SSL

## Referensi
- RFC 5321 (SMTP)
- Dokumentasi Resmi Nginx

[Dokumentasi Konfigurasi Nginx](./assets/konfigurasi_smtp_nginx.png)
[Attech for smtp konfigutasi](./assets/host_smtp.png)