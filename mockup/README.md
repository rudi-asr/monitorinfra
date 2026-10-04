# MonitorInfra — mockup

Mockup HTML statis. Belum ada backend, belum terhubung ke sistem nyata. Semua angka dan insiden adalah data contoh.

## Mulai dari sini: Tahap 1 — Jaringan

`network.html` adalah ruang lingkup tahap awal: **hanya perangkat jaringan**
(router, switch, firewall, access point, server jaringan). Tiga layar saja:

1. **Perangkat** — satu baris ringkasan ("2 perangkat perlu diperiksa"), lalu dua tabel:
   *perlu perhatian* di atas, *normal* di bawah. Klik baris → detail perangkat langsung di tempat
   (identitas dari SNMP, latensi 24 jam, interface, kejadian terakhir).
2. **Penemuan** — cara semua perangkat masuk ke daftar: isi rentang CIDR, pilih metode, tekan
   "Mulai penemuan". Log berjalan bertahap, lalu muncul daftar perangkat yang belum teridentifikasi
   lengkap dengan alasan dan tingkat keyakinan.
3. **Peta Koneksi** — dari LLDP/CDP dan tabel MAC switch. Klik simpul untuk melihat tautannya.

Bagaimana perangkat terdeteksi (dan batasnya) dijelaskan di dalam layar Penemuan, bagian
"Bagaimana perangkat ditemukan".

## Konsep penuh (belum jadi ruang lingkup tahap 1)

| Berkas | Isi |
|---|---|
| `index.html` | Halaman positioning: 7 engine, mode kerja, agent team, intelligence layer |
| `console.html` | Console konsep penuh: 9 tampilan, 7 mode, playbook, remediasi, audit, design system |

## Cara membuka

    cd /Users/rudi/Documents/monitorinfra/mockup
    python3 -m http.server 8123 --bind 127.0.0.1
    # lalu buka http://127.0.0.1:8123/network.html

Halaman juga bisa dibuka langsung sebagai berkas (`file://.../network.html`) — tidak perlu build step.

## Cara mencoba

Tahap 1 (`network.html`):
- Klik baris perangkat mana pun — detail muncul langsung, tanpa tombol "Muat" dan tanpa pindah halaman.
- Cari/filter: ketik `bandung`, atau pilih tipe `Switch`.
- **Penemuan** → "Mulai penemuan" → tekan *Tambahkan* pada salah satu hasil: perangkat itu benar-benar
  masuk ke daftar Perangkat dan ikut terhitung.
- **Peta Koneksi** → klik `rt-branch-bdg` (simpul yang diam) untuk melihat tautan yang putus.
- Bisa dioperasikan dengan keyboard: Tab ke simpul peta, lalu Enter.

Console konsep (`console.html`) menyimpan semua yang belum masuk tahap 1: korelasi, playbook,
remediasi, audit.

## Aturan desain yang dipegang

- **Dark default selalu** (`data-theme="dark"` pada `<html>`); tema terang hanya lewat pilihan manual + `localStorage`, tidak mengikuti preferensi sistem.
- Satu aksen (teal) untuk aksi; warna status hanya untuk menyatakan keadaan.
- Tanpa gradien, tanpa glassmorphism, tanpa ungu.
- Tipografi IBM Plex Sans (teks) + IBM Plex Mono (angka, id, keluaran perintah).
- Aksi tidak pernah berpindah halaman; memilih item langsung memuat isinya.
- Setiap angka bisa dibuka alasannya; setiap dugaan menyebut sumbernya.

## Status verifikasi

- Uji fungsional di DOM sungguhan (jsdom, node) untuk `network.html` dan `console.html`:
  semua tampilan dirender, filter, pemilihan perangkat, alur penemuan sampai selesai, tambah/abaikan
  hasil penemuan, peta + blast radius, aksi remediasi, tombol tema, operasi keyboard — **tanpa error JS**.
- Render visual diperiksa langsung (headless Chromium) untuk setiap tampilan, termasuk tema terang.
- Belum diuji: perangkat mobile nyata; graf peta belum digeser/di-zoom.

## Belum ada (sengaja)

- Backend dan koneksi nyata ke SNMP/ICMP/syslog; semua nilai masih contoh.
- Login, multi-pengguna, notifikasi (email/WA/Telegram), ekspor laporan.
- Posisi simpul di peta masih tetap (belum dihitung otomatis dari LLDP), dan peta belum bisa digeser/di-zoom.

