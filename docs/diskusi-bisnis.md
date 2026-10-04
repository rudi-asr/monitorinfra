# Diskusi Bisnis — MonitorInfra (tahap 1: pemantauan perangkat jaringan)

Ditulis 28 Sep 2026. Semua angka harga diambil dari halaman resmi vendor pada tanggal tersebut.

---

## 1. Yang TIDAK berbeda (harus diakui lebih dulu)

Kalau pembedanya adalah "auto-discovery + peta koneksi + alerting", itu **sudah jadi inti bisnis pemain lain**:

| Pemain | Yang sudah mereka punya |
|---|---|
| Auvik (Kanada) | Discovery & mapping otomatis sebagai jualan utama, ditambah rekomendasi troubleshooting berbantuan AI ("Auvik Aurora"), backup konfigurasi, NetFlow/traffic analysis, terminal in-app |
| Domotz | Discovery otomatis tanpa batas + peta real-time, remote access, VPN on demand, harga per-device yang dipublikasikan |
| LibreNMS / Observium | Discovery + peta + polling, gratis, komunitas besar |
| Zabbix | Polling jaringan + server, gratis, dipakai luas di Indonesia |
| PRTG (Paessler) | Discovery + peta + 250+ jenis sensor, ada edisi gratis 100 sensor |
| SolarWinds / ManageEngine OpManager / WhatsUp Gold | Versi enterprise, harga lewat penawaran |

Jadi: **"AI", "agentic", "dashboard cantik", "observe→verify" bukan pembeda.** Pembeli tidak membeli kata-kata itu. Pembeli membeli satu dari tiga hal:
1. gangguan lebih cepat ketahuan,
2. lebih cepat selesai (atau tidak perlu mereka tangani sendiri),
3. lebih murah/sederhana daripada yang sudah mereka pakai.

Kalau produk ini hanya "LibreNMS dengan tampilan lebih enak", pembedanya tipis dan harus menang di harga — pertarungan yang sulit.

---

## 2. Yang realistis jadi pembeda (urutan dari yang paling kuat)

1. **Perangkat yang dipakai pasar Indonesia, didukung benar.**
   MikroTik, Ruijie, TP-Link Omada, Huawei, ZTE, Tenda, BDCOM, Fiberhome. Tool luar biasanya hanya menangani ini sebagai "generic SNMP" — tanpa profil khusus, tanpa pemetaan OID yang benar, tanpa tahu arti suhu/optik/PPPoE-nya. Menyediakan profil perangkat yang tepat untuk merek-merek ini adalah kerja nyata yang pemain luar enggan lakukan.

2. **Harga per-situs, bukan per-sensor atau per-perangkat.**
   Model per-sensor (PRTG) menghukum jaringan yang punya banyak port. Model per-device (Auvik/Domotz) menghukum saat jaringan tumbuh. Model "per lokasi, perangkat inti saja" jauh lebih mudah dijual dan diprediksi: satu kantor cabang = satu harga.

3. **On-prem, offline, satu berkas tanpa Docker.**
   Banyak instansi (pemerintah daerah, BUMN kecil, rumah sakit, koperasi, sekolah, pabrik) tidak boleh/tidak mampu pakai cloud asing, dan stafnya tidak akan memelihara Docker/Kubernetes. Satu binary yang dijalankan sebagai service di satu PC/mini PC adalah keunggulan nyata di segmen ini.

4. **Bahasa Indonesia + kanal notifikasi lokal.**
   Antarmuka, alert, dan penjelasan dalam Bahasa Indonesia; notifikasi WhatsApp/Telegram, bukan hanya email (email sering tidak dibaca staf IT kantor cabang).

5. **Penjelasan yang bisa ditindaklanjuti, bukan grafik.**
   Ini tempat AI benar-benar berguna: "latensi naik sejak 19:58, CRC error di uplink, kemungkinan kabel/SFP — periksa ini". Nilainya bukan "AI", tapi "staf IT satu orang tidak perlu jadi ahli jaringan untuk tahu langkah berikutnya". Harus dijual sebagai hasil, bukan sebagai teknologi.

6. **Jalur pengadaan lokal.**
   Untuk instansi pemerintah: e-Katalog LKPP dan syarat TKDN membuka pintu yang pemain asing sulit masuk. Syarat detailnya perlu Anda verifikasi sendiri ke LKPP/konsultan TKDN — tapi sebagai vendor lokal ini keunggulan struktural, bukan soal teknis.

7. **Jasa sebagai pendamping produk.**
   Segmen ini sering tidak mampu membeli alat tanpa orang yang mengoperasikan. Paket "alat + pendampingan bulanan" bisa lebih laku daripada lisensi murni.

---

## 3. Patokan harga pesaing (data, bukan taksiran)

| Produk | Model harga | Angka resmi |
|---|---|---|
| PRTG Network Monitor | per sensor (rata-rata 5–10 sensor per perangkat) | PRTG 500 = 500 sensor (≈50 perangkat) **$200/bulan**; PRTG 1000 ≈100 perangkat **$358/bulan**; PRTG 2500 ≈250 perangkat **$742/bulan** — dibayar tahunan, di luar pajak |
| PRTG (edisi gratis) | — | gratis sampai **100 sensor** |
| PRTG Hosted | langganan tahunan | HOSTED 500 **$2.399/tahun**, HOSTED 1000 **$4.299/tahun** |
| Domotz | per collector / per perangkat (dipublikasikan) | **$35/collector/bulan** atau **$1,50/perangkat terkelola/bulan**; discovery tanpa batas gratis |
| Auvik | per perangkat, kategori inti saja | harga tidak dipublikasikan — **hanya lewat penawaran**. Perangkat inti (firewall, router, switch, WLC, hypervisor, server) dihitung; access point, printer, UPS, kamera, IoT gratis |
| LibreNMS / Observium / Zabbix | gratis (open source) | biaya = tenaga + waktu staf Anda sendiri |

Sumber: halaman pricing Paessler (paessler.com/pricing), halaman support Auvik (support.auvik.com), halaman perbandingan resmi Domotz (domotz.com/compare/domotz-vs-auvik).

**Terjemahan untuk pasar Indonesia** (kurs kasar $1 = Rp16.000, hanya untuk merasa besarnya angka):
- 50 perangkat jaringan di PRTG = sekitar **Rp3,2 juta/bulan** (dibayar tahunan).
- 250 perangkat = sekitar **Rp11,9 juta/bulan**.
- Domotz untuk 50 perangkat = sekitar **Rp1,2 juta/bulan** (peta otomatis sudah termasuk). Yang tidak tersedia untuk pasar kita: dukungan perangkat merek lokal, Bahasa Indonesia, dan pendampingan di tempat.

Catatan penting: dua pemain ini berlomba ke arah yang sama seperti rencana Anda (discovery otomatis + penjelasan + perbaikan), dan kini menempelkan AI ke fitur troubleshooting. Artinya pembedaan tidak boleh diletakkan pada fitur AI itu sendiri.

---

## 4. Celah yang belum dilayani dengan baik

- **LibreNMS/Zabbix**: gratis, tapi butuh orang yang paham Linux, setup rumit, tanpa dukungan resmi. Tidak ada yang bisa ditelepon saat rusak.
- **PRTG/SolarWinds/OpManager**: mahal untuk kantor 20–150 perangkat, harga per-sensor/per-node, vendor asing, dokumentasi dan dukungan berbahasa Inggris.
- **Auvik/Domotz**: unggul untuk MSP di Amerika/Eropa/Australia; dukungan perangkat merek lokal Indonesia lemah, harga dalam dolar, cloud (data keluar).

**Irisan paling masuk akal:** perusahaan/organisasi Indonesia dengan 20–300 perangkat jaringan, punya 1–3 staf IT yang bukan spesialis jaringan, tersebar di 1–10 lokasi, dan tidak punya NOC. Mereka terlalu besar untuk monitoring manual, terlalu kecil untuk membeli SolarWinds — dan tidak punya orang untuk mengoperasikan LibreNMS dengan baik.

Model harga yang saya sarankan: **lisensi per lokasi + batas jumlah perangkat inti** (firewall, router, switch, WLC), dan perangkat pinggiran (access point, printer, kamera, IoT) dihitung gratis tetapi tetap terdeteksi. Alasannya: model Auvik terbukti menjual (prediktabel, jaringan tetap terlihat seluruhnya), dan model gratis-discovery Domotz menurunkan hambatan mencoba.

---

## 5. Bahasa: Go vs Rust (dengan data ekosistem)

Data unduhan per 28 Sep 2026:

| Kebutuhan | Rust (crates.io) | Go | Python |
|---|---|---|---|
| Klien SNMP | `snmp` **94.715** unduhan total (~10.931 dalam 90 hari); `snmp-parser` 1.598.374 (hanya parser) | `gosnmp` **v1.45.0**, rilis 19 Sep 2026 — de-facto standar, dipakai `snmp_exporter` Prometheus | `pysnmp` **7.1.30** — sudah jadi standar bertahun-tahun |
| NetFlow/IPFIX | `netflow_parser` 649.649 | `goflow2` v1.3.7 (tag terakhir Des 2023) | `netflow` 0.12.2 |
| sFlow | `sflow-parser` 488.897 | (bagian goflow2) | — |
| Ambil paket mentah | `pcap` 8.077.808 — sehat | `gopacket` — sehat | `scapy` — sehat |
| Instrumentasi metrik | `prometheus` 148,5 juta — sangat sehat | asal-usul Prometheus sendiri | — |
| Otomasi perangkat (backup config, dsb.) | hampir tidak ada padanan matang | ada (komunitas Prometheus/Nornir-Go) | `netmiko` 4.8.0, `napalm` 5.2.0 — paling matang |

Kesimpulan dari data itu:

- **Ekosistem jaringan paling matang ada di Python, kedua di Go, paling belakang di Rust.** SNMP v3 (auth+priv) dan pembacaan MIB adalah bagian yang paling menyakitkan untuk ditulis dari nol — dan di Rust Anda cenderung harus menulis lebih banyak sendiri, termasuk keamanan protokolnya.
- **Go unggul pada tiga hal sekaligus**: library jaringan yang sudah terbukti (gosnmp), kemampuan menghasilkan satu binary statis tanpa dependensi (sama seperti Rust), dan populasi developer di Indonesia yang jauh lebih besar daripada Rust. Untuk produk yang harus dipelihara dan diserahkan ke orang lain, faktor ketiga sering jadi pembeda antara bisa dijual dan tidak.
- **Rust unggul pada hal spesifik**: jejak memori paling kecil (bisa jalan di perangkat dengan RAM 64–128 MB), tanpa GC, latensi paling terprediksi pada frekuensi polling sangat tinggi, dan keamanan memori saat mem-parsing masukan dari luar (NetFlow, SNMP trap, syslog — ini permukaan serangan nyata). Untuk armadanya, keamanan memori juga argumen yang enak dipakai saat audit/keamanan dan saat mengurus paten/HAKI.
- **Python tetap relevan** sebagai tempat mengolah data, eksperimen model, dan menghubungkan LLM — bukan sebagai mesin polling.

---

## 6. Rekomendasi arsitektur bahasa

**Go untuk seluruh inti produk di tahap 1**, satu binary: collector (ICMP/SNMP/MAC/LLDP), penyimpanan deret waktu ringan, HTTP API, dan antarmuka web yang ditanam. Alasan: library jaringan yang terbukti, satu binary tanpa Docker, kecepatan membangun jauh lebih tinggi untuk tim kecil, dan Anda sudah memakai Go di pekerjaan lain (CI `go build/vet/test` sudah jadi kebiasaan).

**Rust sebagai komponen opsional nanti, bukan sekarang** — khusus untuk bagian yang benar-benar butuh, misalnya parser NetFlow/sFlow/trap berkecepatan tinggi atau agen yang ditempel di perangkat kecil. Kalau ditulis sebagai library terpisah (cgo/FFI atau proses tersendiri), ia tidak menular ke seluruh proyek.

**Python hanya untuk hal di luar jalur produksi**: analisis data, evaluasi model, skrip impor inventaris.

**Hindari tiga bahasa sekaligus di tahap 1.** Setiap bahasa tambahan berarti dua kali jalur build, dua kali penanganan bug, dua kali profil orang yang harus direkrut.

Yang **saya tidak sarankan**: memilih Rust sebagai bahasa utama sekarang, hanya karena "Rust lebih kencang". Pada 20–300 perangkat, kendala Anda bukan CPU atau memori — melainkan waktu Anda membangun, dukungan perangkat merek lokal, dan kepercayaan pembeli. Rust memindahkan risiko ke tempat yang salah pada tahap ini.

---

## 7. Risiko jujur

1. **Pembedaan fitur mudah disalin.** Auvik/Domotz sudah punya discovery + peta + AI troubleshooting. Yang sulit disalin: dukungan merek lokal, Bahasa, harga lokal, dan kehadiran fisik untuk pendampingan.
2. **Segmen SMB Indonesia sensitif harga dan lambat membeli.** Calon pembeli akan membandingkan dengan "LibreNMS kan gratis". Jawabannya harus jasa + kemudahan + dukungan, bukan fitur.
3. **Dukungan perangkat lokal adalah pekerjaan tanpa akhir** (firmware beda-beda, OID beda-beda). Ini pembeda sekaligus biaya operasional terbesar.
4. **AI di jalur diagnosis berisiko salah menjelaskan.** Untuk tindakan yang menyentuh jaringan produksi, wajib ada mode saran + persetujuan manusia (sudah jadi aturan di mockup).
5. **Kalau masuk pengadaan pemerintah**, siapkan dokumen legal, TKDN, dan dukungan formal — bukan hanya produk.

---

## 8. Keputusan yang perlu ditetapkan sebelum menulis kode

1. Segmen mana yang dikejar lebih dulu: SMB/kantor 20–300 perangkat, ISP/MSP multi-site, instansi pemerintah, atau enterprise.
2. Model bisnis: lisensi perpetual + maintenance tahunan, langganan bulanan per lokasi, atau jasa terkelola (alat + pendampingan).
3. Bahasanya: Go semua, atau Go inti + Rust untuk parser/agen.
4. Yang dijual lebih dulu: deteksi perangkat saja (tahap 1), atau langsung dengan peta + alerting.
