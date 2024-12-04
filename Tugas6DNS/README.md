# Domain Name System (DNS)

## Arsitektur dan Konsep DNS

### Definisi Teknis
DNS merupakan sistem hierarkis dan terdistribusi yang menerjemahkan nama domain (domain names) menjadi alamat IP yang dapat diproses oleh perangkat jaringan. Sistem ini beroperasi menggunakan protokol UDP/TCP port 53.

### Struktur Hierarki DNS
```
.                   (Root Domain)
|
+-- .com            (Top-Level Domain)
|   |
|   +-- example.com (Second-Level Domain)
|       |
|       +-- www     (Subdomain)
```

### Komponen Infrastruktur
1. **Root Nameserver**
   - 13 server root yang dikelola secara global
   - Menyediakan referensi TLD (Top-Level Domain)
   - Dioperasikan oleh 12 organisasi independen

2. **TLD Nameserver**
   - Mengelola domain tingkat atas (.com, .org, .net)
   - Menyimpan informasi nameserver untuk domain kedua

3. **Authoritative Nameserver**
   - Server resmi yang menyimpan record DNS aktual
   - Memberikan jawaban definitif untuk query

4. **Recursive Resolver**
   - Melakukan pencarian DNS kompleks
   - Menelusuri hierarki untuk mendapatkan alamat IP

### Tipe Record DNS Terperinci

| Tipe Record | Fungsi | Contoh |
|-------------|--------|--------|
| A Record | Pemetaan IPv4 | `example.com IN A 192.168.1.1` |
| AAAA Record | Pemetaan IPv6 | `example.com IN AAAA 2001:0db8:85a3:0000:0000:8a2e:0370:7334` |
| CNAME | Alias domain | `www IN CNAME example.com.` |
| MX Record | Routing email | `example.com IN MX 10 mail.example.com.` |
| TXT Record | Verifikasi domain | SPF, DKIM, DMARC |
| NS Record | Nameserver otoritatif | `example.com IN NS ns1.example.com.` |
| PTR Record | Reverse DNS | IP ke nama domain |
| SOA Record | Parameter zona | Informasi administrasi DNS |

## Mekanisme Resolusi DNS

### Proses Resolusi Lengkap
1. Klien mengirim query ke resolver lokal
2. Resolver memeriksa cache lokal
3. Jika tidak ada, query diteruskan ke root nameserver
4. Root nameserver merujuk ke TLD nameserver
5. TLD nameserver merujuk ke authoritative nameserver
6. Authoritative nameserver memberikan jawaban definitif
7. Jawaban di-cache di berbagai tingkatan

### Strategi Caching
- Browser: Singkat (menit)
- Sistem Operasi: Menengah (jam)
- DNS Resolver: Panjang (hari)

## Konfigurasi DNS di Nginx

### Konfigurasi Resolusi
```nginx
# Pengaturan global resolver
resolver 8.8.8.8 8.8.4.4 valid=300s;
resolver_timeout 5s;

# Konfigurasi server
server {
    listen 80;
    server_name example.com;

    # Proxy dengan resolusi dinamis
    location / {
        proxy_pass http://backend_server;
        proxy_set_header Host $host;
        proxy_resolver_address 1.1.1.1;
    }
}
```

### Konfigurasi Keamanan DNS
```nginx
# Mencegah DNS rebinding
server {
    listen 80;
    server_name example.com;
    
    # Pembatasan resolusi
    resolver 9.9.9.9 valid=60s;
    resolver_timeout 3s;
}
```

## Praktik Keamanan DNS

### Teknik Perlindungan
- DNSSEC (Domain Name System Security Extensions)
- DNS over TLS (DoT)
- DNS over HTTPS (DoH)
- Implementasi DANE (DNS-based Authentication of Named Entities)

### Mitigasi Serangan
- Cache poisoning
- DNS amplification
- DNS tunneling
- Implementasi QNAME minimization

## Troubleshooting Lanjutan

### Alat Diagnostik
- `dig`: Analisis query DNS
- `nslookup`: Informasi resolver
- `traceroute`: Pelacakan rute
- Wireshark: Analisis paket DNS

### Log dan Monitoring
- `/var/log/named/`
- `/var/log/syslog`
- Monitoring real-time dengan `rndc status`

## Referensi Teknis
- RFC 1035 (DNS Implementasi)
- RFC 4034 (DNSSEC)
- IANA DNS Parameters