# Panduan Mendalam Simple Mail Transfer Protocol (SMTP)

## Arsitektur dan Konsep SMTP

### Definisi Teknis
SMTP adalah protokol komunikasi standar untuk transmisi email antar server menggunakan model client-server, beroperasi pada port 25 (non-SSL), 465 (SMTPS), dan 587 (STARTTLS).

### Komponen Infrastruktur Email
1. **Mail User Agent (MUA)**
   - Email client (Outlook, Thunderbird)
   - Antarmuka pengguna

2. **Mail Transfer Agent (MTA)**
   - Server pengolah transmisi email
   - Routing dan pengiriman pesan

3. **Mail Delivery Agent (MDA)**
   - Mengantarkan email ke mailbox
   - Filtering dan penyimpanan

### Alur Transmisi Email
```
Pengirim (MUA) → Outgoing SMTP Server (MTA) 
→ Internet Routing → Incoming SMTP Server 
→ Mail Delivery Agent (MDA) 
→ Penerima (MUA)
```

## Protokol dan Mekanisme SMTP

### Perintah Dasar SMTP
- `HELO`: Memulai sesi
- `MAIL FROM`: Mendefinisikan pengirim
- `RCPT TO`: Mendefinisikan penerima
- `DATA`: Memulai transfer konten
- `QUIT`: Mengakhiri sesi

### Kode Respon Standar
| Kode | Kategori | Makna |
|------|----------|-------|
| 2xx  | Sukses   | Perintah diterima |
| 3xx  | Transisi | Diperlukan tindakan tambahan |
| 4xx  | Temporer | Kesalahan sementara |
| 5xx  | Permanen | Kesalahan fatal |

## Konfigurasi SMTP di Nginx

### Konfigurasi Proxy SMTP
```nginx
mail {
    server_name mail.example.com;
    
    smtp_server {
        listen 25 ssl;
        protocol smtp;
        
        # Batasan koneksi
        max_connections 500;
        max_connections_per_ip 50;
        
        # Autentikasi
        auth_methods plain login;
        
        # SSL/TLS
        ssl_certificate /etc/ssl/smtp.crt;
        ssl_certificate_key /etc/ssl/smtp.key;
        
        # Rate limiting
        limit_req zone=smtp_zone burst=100;
    }
}
```

### Konfigurasi Keamanan Lanjutan
```nginx
# Filter dan proteksi
mail {
    smtp_server {
        # Whitelist IP
        allow 192.168.1.0/24;
        deny all;
        
        # Ukuran pesan
        max_message_size 20m;
        
        # Anti-spam
        rbl_zone spamhaus_zone resolve=127.0.0.2-255;
    }
}
```

## Keamanan dan Autentikasi

### Protokol Keamanan
- STARTTLS
- SSL/TLS
- SMTP Authentication
- SPF (Sender Policy Framework)
- DKIM (DomainKeys Identified Mail)
- DMARC (Domain-based Message Authentication)

### Mitigasi Serangan
- Open Relay Prevention
- Reverse DNS Checking
- Greylisting
- Spam Score Filtering
- Rate Limiting

## Troubleshooting SMTP

### Diagnostik Email
- Analisis log: `/var/log/mail.log`
- Pengujian koneksi: `telnet`, `swaks`
- Validasi konfigurasi: `postconf -n`

### Monitoring
- Jumlah email terkirim/diterima
- Latensi transmisi
- Error rate
- Kapasitas queue

## Praktik Terbaik
- Implementasi autentikasi
- Enkripsi full-channel
- Validasi pengirim
- Batasan koneksi
- Manajemen queue
- Monitoring berkala

## Referensi Teknis
- RFC 5321 (SMTP)
- RFC 3207 (STARTTLS)
- RFC 4954 (SMTP Authentication)