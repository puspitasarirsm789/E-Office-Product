# Product Proposal: E-Office

## Ringkasan dan asumsi

E-Office adalah sistem internal terpusat untuk administrasi kepegawaian, surat-menyurat elektronik, dan tata usaha. Dokumen ini disusun dari case study yang terbatas. Istilah “perusahaan” digunakan sebagai organisasi pengguna tanpa mengasumsikan industri, ukuran organisasi, struktur legal, ataupun aplikasi yang telah tersedia.

**Assumption utama:** organisasi memiliki beberapa departemen, data pegawai dikelola oleh HR/Admin, dan surat keluar perlu ditinjau oleh atasan sebelum didistribusikan. Kebijakan retensi dokumen, klasifikasi kerahasiaan, serta integrasi sistem yang telah ada merupakan Open Question yang harus dikonfirmasi saat discovery.

## Problem Statement

Proses administrasi yang tersebar di email, spreadsheet, atau dokumen fisik berpotensi menyebabkan data pegawai tidak konsisten, status surat sulit ditelusuri, persetujuan terlambat, dan bukti aktivitas tidak mudah diaudit. Staff harus melakukan konfirmasi manual untuk mengetahui tahapan pengajuan, sedangkan Manager dan Management tidak memiliki ringkasan operasional yang sama.

## Product Objective

Menyediakan satu sistem internal yang menjadi sumber informasi operasional untuk data pegawai dan surat, mendukung workflow persetujuan, serta menampilkan status dan riwayat tindakan secara jelas kepada pihak yang berwenang.

## Target User

| Pengguna | Kebutuhan utama |
|---|---|
| Staff | Mengakses profil kerja, membuat surat, melacak status, dan menindaklanjuti revisi. |
| Manager/Approver | Meninjau, menyetujui, atau mengembalikan surat beserta catatan. |
| HR/Admin | Memelihara data pegawai, departemen, nomor surat, dan akses pengguna. |
| Management | Memantau indikator operasional dan surat yang memerlukan perhatian. |

## Product Scope

**In scope untuk MVP:** Authentication dan role-based authorization; pengelolaan data pegawai dan departemen; pembuatan serta pengiriman surat internal; lampiran; workflow persetujuan satu tingkat; notifikasi dalam aplikasi; dashboard berbasis peran; pencarian, filter, dan audit trail.

**Out of scope untuk MVP:** payroll, absensi, tanda tangan elektronik tersertifikasi, integrasi layanan eksternal, OCR, workflow persetujuan paralel atau multi-level yang dapat dikonfigurasi, dan aplikasi mobile native. Item tersebut dapat dievaluasi setelah penggunaan MVP tervalidasi.

## Success Metrics

Baseline perlu diukur sebelum pilot. Target berikut berlaku tiga bulan setelah go-live untuk unit pilot.

| Metrik | Definisi | Target |
|---|---|---|
| Adopsi pengguna aktif | Pengguna aktif mingguan dibagi pengguna yang ditugaskan | ≥ 80% |
| Digitalisasi surat | Surat internal yang dibuat dan diproses di E-Office | ≥ 75% |
| Waktu persetujuan median | Dari Submit sampai keputusan akhir | turun ≥ 30% dari baseline |
| Keterlacakan surat | Surat submit yang memiliki status dan riwayat lengkap | ≥ 98% |
| Kualitas data pegawai | Rekor pegawai aktif dengan field wajib lengkap | ≥ 95% |
| Kepuasan pengguna | Skor survei pasca-pilot skala 1–5 | ≥ 4,0 |

## High-level Timeline

Timeline berikut adalah estimasi untuk pilot MVP selama 12 minggu. Estimasi mengasumsikan keputusan bisnis dapat diberikan tepat waktu, tidak ada integrasi eksternal pada MVP, dan data pegawai awal tersedia dari HR/Admin.

| Fase | Minggu | Fokus | Output / keputusan utama |
|---|---:|---|---|
| Discovery & alignment | 1–2 | Validasi proses saat ini, role, kebijakan data, Open Questions, dan baseline metrik | Ruang lingkup pilot, workflow satu tingkat, serta owner kebijakan disetujui. |
| Design & backlog refinement | 3–4 | Detail requirement, prototype, data model, desain UI, dan rencana UAT | Backlog MVP, acceptance criteria, serta desain siap dibangun. |
| MVP development | 5–8 | Authentication, employee management, letter management, approval, dashboard, notifikasi, dan audit trail | Increment produk yang dapat diuji pada environment UAT. |
| System test & UAT | 9–10 | Pengujian fungsional, perbaikan isu kritis, persiapan data pilot, dan UAT | Skenario UAT kritis lulus dan pengguna pilot siap menggunakan sistem. |
| Pilot go-live & measurement | 11–12 | Rilis ke unit pilot, hypercare, pengukuran adopsi dan baseline pembanding | Laporan hasil pilot dan keputusan iterasi fase berikutnya. |

## High-level Budget / Resource Assumption

Anggaran di bawah adalah **rough order of magnitude (ROM)** untuk MVP pilot selama 12 minggu dalam konteks pengadaan jasa pengembangan di Indonesia. Ini bukan quotation, belum termasuk PPN, biaya internal organisasi, lisensi enterprise, SSO, e-signature, maupun integrasi pihak ketiga. Nilai perlu divalidasi melalui discovery dan strategi pengadaan.

| Komponen | Assumption | Estimasi biaya |
|---|---|---:|
| Product & delivery | Product Owner/BA 0,5 FTE dan Project Manager/Scrum Master 0,25 FTE selama 12 minggu | Rp55–85 juta |
| Design & engineering | UI/UX Designer 0,5 FTE pada fase awal; 2 Full-stack Engineer 1 FTE selama build | Rp180–280 juta |
| Quality & platform | QA Engineer 0,5 FTE; DevOps/Cloud Engineer 0,2 FTE; setup environment dan monitoring dasar | Rp55–90 juta |
| Infrastruktur pilot | Hosting, database, object storage, backup, dan domain internal selama pilot | Rp15–30 juta |
| Contingency | Cadangan 15% untuk klarifikasi requirement, perbaikan UAT, dan risiko delivery | Rp45–70 juta |
| **Total ROM** | **Sekitar 11–13 person-month, tidak termasuk resource internal organisasi** | **Rp350–555 juta** |

**Assumption resource:** satu Product Owner dari organisasi tetap tersedia untuk keputusan prioritas minimal dua kali per minggu; HR/Admin menyediakan pemilik data untuk cleansing dan UAT; satu Manager/Approver dari unit pilot tersedia untuk validasi workflow. Jika salah satu asumsi ini tidak terpenuhi, timeline dan biaya dapat meningkat.

## Open Questions

1. Apakah surat mencakup surat masuk, surat keluar, atau keduanya pada tahap pertama?
2. Siapa pemilik kebijakan nomor surat, retensi, klasifikasi, dan template?
3. Apakah approval wajib satu tingkat untuk semua departemen, atau terdapat pengecualian?
4. Apakah organisasi memerlukan SSO, tanda tangan elektronik, atau integrasi HRIS pada fase berikutnya?
