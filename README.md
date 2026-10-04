# MonitorInfra

Agentic infrastructure operations. **Tahap 1 = monitoring jaringan** (network
devices) — routers, switches, firewalls, AP, network servers. Servers/apps,
containers, cloud, security/vuln adalah tahap berikutnya.

## Isi

- `mockup/network.html` — **Tahap 1, yang in-scope**: 3 layar (Perangkat,
  Penemuan, Peta Koneksi)
- `mockup/console.html` — konsep full (9 view, 7 mode, playbooks, remediation) — arsip
- `mockup/index.html` — halaman konsep/positioning
- `docs/diskusi-bisnis.md` — catatan bisnis

## Deploy (server)

- Repo: `github.com/rudi-asr/monitorinfra` (public)
- LXC 207 `24-monitorinfra` @ 192.168.1.24 / ::124 (Debian 13, nginx)
- Frontend statis di nginx, satu LXC (frontend + backend masa depan sama)
- URL: https://monitorinfra.rudilab.my.id
- Routing: Cloudflare Tunnel -> rproxy 101 nginx -> 192.168.1.24:80
- Akses: davy@pve role LabVMOp di /vms/207

## Serve lokal

```bash
cd mockup && python3 -m http.server 8123 --bind 127.0.0.1
```

## House rules (lihat skill monitorinfra)

Dark default (`data-theme="dark"`), aksen teal #17b8a6, tidak ungu, "Batasi jujur"
sebagai fitur, tindakan tidak pernah navigasi keluar.