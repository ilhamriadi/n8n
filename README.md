# n8n-server

n8n workflow automation server yang berjalan dengan Docker dan Docker Compose.

## Tentang n8n

n8n adalah platform otomatisasi workflow open-source yang memungkinkan Anda menghubungkan berbagai aplikasi dan layanan tanpa perlu menulis kode.

## Prasyarat

- Docker
- Docker Compose
- Network `npm-network` (untuk koneksi dengan Nginx Proxy Manager atau reverse proxy lainnya)

## Instalasi

1. Clone repository ini:
```bash
git clone <repository-url>
cd n8n-server
```

2. Buat network Docker jika belum ada:
```bash
docker network create npm-network
```

3. Konfigurasi environment variables di file `.env`:
```bash
cp .env.example .env
# Edit .env sesuai kebutuhan
```

## Konfigurasi

Edit file `.env` untuk mengatur parameter berikut:

| Variable | Deskripsi | Default |
|----------|-----------|---------|
| `N8N_BASIC_AUTH_ACTIVE` | Aktifkan basic authentication | `true` |
| `N8N_BASIC_AUTH_USER` | Username untuk basic auth | `ilham` |
| `N8N_BASIC_AUTH_PASSWORD` | Password untuk basic auth | - |
| `N8N_HOST` | Host/IP address server | - |
| `N8N_PORT` | Port yang digunakan | `5678` |
| `N8N_PROTOCOL` | Protokol (http/https) | `http` |
| `N8N_SECURE_COOKIE` | Gunakan secure cookie | `false` |
| `NODE_ENV` | Environment mode | `production` |

## Penggunaan

### Menjalankan Server

```bash
docker-compose up -d
```

### Menghentikan Server

```bash
docker-compose down
```

### Melihat Logs

```bash
docker-compose logs -f n8n
```

## Data Persistence

Data n8n disimpan di direktori `./n8n-data` yang di-mount ke container pada path `/home/node/.n8n`. Pastikan untuk backup direktori ini secara berkala.

## Akses

Setelah server berjalan, Anda dapat mengakses n8n melalui:
- Direct: `http://<N8N_HOST>:5678`
- Melalui reverse proxy (Nginx Proxy Manager)

Gunakan kredensial basic auth yang dikonfigurasi di file `.env` untuk login.

## Troubleshooting

### Container tidak mau start
```bash
docker-compose logs n8n
```

### Tidak dapat mengakses melalui reverse proxy
Pastikan:
1. Network `npm-network` sudah dibuat
2. Container berada di network yang sama
3. Port 5678 sudah di-expose dengan benar

### Reset data
Hapus direktori `n8n-data` dan restart container:
```bash
rm -rf n8n-data
docker-compose up -d
```

## Backup

Untuk backup data n8n:
```bash
tar -czf n8n-backup-$(date +%Y%m%d).tar.gz n8n-data/
```

## License

**n8n** dilisensikan under [Fair-Code License](https://faircode.io/license).

**Konfigurasi Docker dan file konfigurasi** dalam repository ini dilisensikan under [MIT License](https://opensource.org/licenses/MIT).

---

**Repository**: [https://github.com/ilhamriadi/n8n](https://github.com/ilhamriadi/n8n)

---

*Dibuat dengan ❤️ oleh [ilhamriadi](https://github.com/ilhamriadi)*
