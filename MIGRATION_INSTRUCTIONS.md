# Instruksi Migration Database

## Perubahan dari "customer" ke "plate_number"

Aplikasi telah diupdate untuk menggunakan "Plat Nomor" sebagai pengganti "Nama Pelanggan". Untuk menerapkan perubahan ini ke database, ikuti langkah berikut:

### Opsi 1: Via Supabase Dashboard (Direkomendasikan)

1. Buka [Supabase Dashboard](https://supabase.com/dashboard)
2. Pilih project Anda
3. Klik "SQL Editor" di sidebar
4. Salin dan jalankan SQL berikut:

```sql
-- Rename column dari customer ke plate_number
ALTER TABLE transactions
RENAME COLUMN customer TO plate_number;

-- Update data sample yang sudah ada
UPDATE transactions SET plate_number = 'B 1234 ABC' WHERE plate_number = 'Budi Santoso';
UPDATE transactions SET plate_number = 'B 5678 DEF' WHERE plate_number = 'Rina Wati';
UPDATE transactions SET plate_number = 'B 9012 GHI' WHERE plate_number = 'Andi Pratama';
UPDATE transactions SET plate_number = 'B 3456 JKL' WHERE plate_number = 'Siti Nurhaliza';
```

5. Klik tombol "Run" untuk menjalankan SQL

### Opsi 2: Database Fresh Install

Jika Anda ingin memulai dari awal dengan database bersih:

1. Drop tabel `transactions` yang lama
2. Jalankan ulang migration file: `20251014155257_create_avto_carwash_tables.sql` dengan perubahan `customer` menjadi `plate_number`

### Verifikasi

Setelah migration berhasil, Anda bisa verify dengan query:

```sql
SELECT * FROM transactions LIMIT 5;
```

Pastikan kolom `plate_number` ada dan berisi data plat nomor kendaraan.

## Catatan

- Migration file sudah tersedia di `supabase/migrations/20251016164300_rename_customer_to_plate_number.sql`
- Kode aplikasi sudah diupdate untuk menggunakan `plate_number`
- Form input sekarang otomatis mengubah input ke uppercase untuk plat nomor
