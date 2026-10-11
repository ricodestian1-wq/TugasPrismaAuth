# Prisma Auth

Modul registrasi dan login dengan Next.js App Router, Prisma, MySQL, dan
`bcryptjs`.

## Persiapan

1. Jalankan MySQL melalui XAMPP atau Laragon. Pengguna `root` tanpa kata sandi
   dapat menggunakan contoh koneksi di bawah.
2. Salin `.env.example` menjadi `.env`, lalu sesuaikan `DATABASE_URL` dengan
   kredensial dan nama database MySQL Anda:

   ```env
   DATABASE_URL="mysql://root:@localhost:3306/db_prisma_auth"
   ```

   Jika kata sandi berisi karakter khusus, URL-encode kata sandi tersebut.
   Jangan commit file `.env`.
3. Pasang dependensi dan siapkan database:

   ```powershell
   npm install
   npm run db:generate
   npm run db:migrate -- --name init_users
   ```

   Prisma akan membuat database `db_prisma_auth` bila pengguna MySQL memiliki
   izin untuk membuat database. Migrasi awal tersedia di
   `prisma/migrations/20261006000000_init_users`.
4. Jalankan aplikasi:

   ```powershell
   npm run dev
   ```

   Buka `http://localhost:3000/register` untuk membuat akun atau
   `http://localhost:3000/login` untuk masuk.

## Endpoint

- `POST /api/register` menerima `{ "name": "...", "email": "...", "password": "..." }`.
- `POST /api/login` menerima `{ "email": "...", "password": "..." }`.

Email dinormalisasi ke huruf kecil, password minimal 8 karakter dan dibatasi
hingga 72 byte untuk kompatibilitas bcrypt, dan password hanya disimpan setelah
di-hash. Login demo memvalidasi kredensial lalu mengembalikan ringkasan pengguna;
modul ini belum membuat sesi persisten atau melindungi halaman privat.

Untuk membuka Prisma Studio, jalankan `npm run db:studio`.
# TugasPrismaAuth
