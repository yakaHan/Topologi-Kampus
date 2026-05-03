# 🎓 Campus Network Topology Project (High Availability Design)

## 📌 Deskripsi
Project ini merupakan simulasi topologi jaringan kampus yang dirancang untuk mendukung operasional berbagai unit akademik dan non-akademik. Jaringan ini mencakup beberapa gedung dengan segmentasi user yang kompleks, serta mengimplementasikan konsep high availability menggunakan dual multilayer switch dan dua ISP berbeda.

Topologi ini dirancang untuk memastikan jaringan tetap berjalan meskipun terjadi gangguan pada salah satu jalur utama.

---

## 🏢 Struktur Jaringan Kampus
- Total 5 gedung
- 1 gedung terdiri dari 4 lantai
- Setiap lantai memiliki:
  - 1 Switch (akses layer)
  - 1 Wireless Access Point (WLAN)
- Core jaringan menggunakan 2 Multilayer Switch

---

## 👥 Segmentasi Pengguna
Jaringan dibagi berdasarkan kebutuhan masing-masing unit:
- Rektor
- Dekan
- Kaprodi
- Staff Pengajaran
- Staff Akademik
- Staff Customer Service (CS)
- Ruang Kelas
- PC Lab
- Staff Keuangan
- Ruang Dosen
- Staff IT

Setiap kategori pengguna dipisahkan dalam jaringan yang berbeda untuk meningkatkan keamanan dan manajemen traffic.

---

## ⚙️ Konfigurasi yang Digunakan

### VLAN (Virtual Local Area Network)
- Digunakan untuk segmentasi jaringan berdasarkan unit pengguna
- Mengurangi broadcast domain
- Meningkatkan keamanan dan performa jaringan

### WLAN (Wireless Local Area Network)
- Access Point tersedia di setiap lantai
- Mendukung mobilitas user di lingkungan kampus

### DHCP (Dynamic Host Configuration Protocol)
- IP address diberikan secara otomatis ke seluruh client
- Mempermudah pengelolaan jaringan dalam skala besar

### Multilayer Switch (Layer 3)
- Digunakan untuk inter-VLAN routing
- Menjadi core utama jaringan kampus
- Terdapat 2 multilayer switch untuk mendukung redundancy

### IP Route (Static Routing)
- Digunakan untuk mengatur jalur komunikasi antar network
- Menghubungkan jaringan internal dengan ISP

### Network Port Security
- Diterapkan pada switch akses
- Membatasi perangkat yang dapat terhubung
- Mencegah akses ilegal ke jaringan

---

## 🔄 High Availability & Redundancy

### Desain
- Multilayer Switch 1 → Terhubung ke ISP 1 (Primary)
- Multilayer Switch 2 → Terhubung ke ISP 2 (Backup)

### Mekanisme
- Saat Multilayer Switch 1 aktif → seluruh traffic menggunakan ISP 1
- Saat Multilayer Switch 1 mati (ISP 1 down) → seharusnya Multilayer Switch 2 mengambil alih

### ⚠️ Kendala yang Ditemukan
- Multilayer Switch 2 **tidak aktif secara otomatis** saat Multilayer Switch 1 mati
- Perlu dilakukan aktivasi/manual intervention

### 💡 Analisis
- Belum adanya mekanisme failover otomatis seperti:
  - Dynamic routing protocol
  - First Hop Redundancy Protocol (FHRP) seperti HSRP/VRRP
- Sistem masih bergantung pada konfigurasi manual

### ✅ Solusi yang Disarankan
- Mengimplementasikan:
  - HSRP (Hot Standby Router Protocol)
  - atau dynamic routing (OSPF/EIGRP)
- Mengatur priority dan preemption untuk failover otomatis

---

## 🎯 Tujuan Project
- Memahami desain jaringan kampus skala besar
- Menerapkan segmentasi menggunakan VLAN
- Menggunakan multilayer switch untuk routing
- Mengimplementasikan DHCP dan WLAN
- Meningkatkan keamanan dengan port security
- Mempelajari konsep high availability dan failover
