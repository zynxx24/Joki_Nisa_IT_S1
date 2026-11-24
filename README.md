# Sistem Absensi Karyawan

Aplikasi absensi berbasis web dengan Next.js dan MySQL. Karyawan absen dengan mengunggah foto dan memilih status Hadir atau Izin, lalu admin memantau, mengoreksi, dan mengekspor datanya. Dibuat sebagai proyek pesanan untuk tugas Sistem Informasi.

## Fitur

**Karyawan**
- Daftar akun dengan email, username, NIP, dan kode pendaftaran dari admin.
- Form absensi: foto (PNG atau JPG, maksimal 5 MB), keterangan, dan status Hadir atau Izin.
- Riwayat absensi sendiri.

**Admin**
- Ringkasan: total karyawan, total absensi, hadir hari ini.
- Tabel absensi dengan foto, filter status, dan edit absensi.
- Kelola data karyawan.
- Export semua absensi ke CSV.

Login memakai JWT yang berlaku 24 jam, dan password disimpan sebagai hash bcrypt.

## Menjalankan

Butuh Node.js 18 atau lebih baru dan MySQL (misalnya dari XAMPP).

1. Buat database dengan menjalankan `mysql.schema`. Skrip ini membuat database `attendance_db`, tabelnya, satu akun admin, dan satu kode pendaftaran.
   ```bash
   mysql -u root -p < mysql.schema
   ```
2. Sesuaikan `nisa/.env` dengan MySQL kamu: `DB_HOST`, `DB_USER`, `DB_PASSWORD`, `DB_NAME`, dan ganti `JWT_SECRET` dengan string acak yang panjang.
3. Jalankan aplikasinya:
   ```bash
   cd nisa
   npm install
   npm run dev
   ```
4. Buka http://localhost:3000.

### Akun bawaan

| | |
|---|---|
| Admin | `tes@gmail.com` / `123456` |
| Kode pendaftaran karyawan | `KODE2025` |

Keduanya hanya untuk mencoba di komputer sendiri. Ganti password admin dan kode pendaftaran sebelum aplikasi dipakai sungguhan (tabel `admins` dan `admin_codes`).

## Struktur

```
mysql.schema          tabel users, admins, attendance, admin_codes, dan view attendance_with_users
nisa/
  lib/auth.ts         JWT, bcrypt, cek kode pendaftaran
  lib/db.ts           koneksi MySQL (mysql2)
  pages/              halaman login, daftar, dashboard karyawan dan admin
  pages/api/user/     daftar, login, kirim absensi, riwayat
  pages/api/admin/    login, statistik, kelola absensi dan user, export CSV
```

Foto absensi disimpan di `nisa/public/uploads/`.

Dibuat oleh [zynxx24](https://github.com/zynxx24).
