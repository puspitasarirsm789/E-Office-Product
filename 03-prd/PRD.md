# Product Requirements Document: E-Office

## Product Overview

E-Office adalah aplikasi web internal untuk mengelola direktori pegawai dan siklus hidup surat internal: Draft, Pending Approval, Need Revision, Approved, atau Rejected. Produk menerjemahkan BR-001 sampai BR-008 ke dalam fitur operasional yang dapat digunakan oleh Staff, Manager/Approver, HR/Admin, dan Management.

## User Persona

| Persona | Tujuan | Kendala saat ini | Kebutuhan produk |
|---|---|---|---|
| Staff | Mengajukan surat dengan benar dan cepat | Tidak tahu status atau revisi terakhir | Form jelas, draft, status, riwayat, notifikasi. |
| Manager/Approver | Menyelesaikan antrean keputusan | Dokumen dan konteks tersebar | Antrean prioritas, preview, keputusan, catatan. |
| HR/Admin | Menjaga data pegawai dan administrasi | Data ganda serta akses tidak terkendali | CRUD pegawai, departemen, peran, audit. |
| Management | Memantau kesehatan proses | Harus meminta rekap secara manual | Dashboard ringkas, hanya baca. |

## Feature List

| Feature | Deskripsi | Referensi BR | Referensi FSD |
|---|---|---|---|
| F-01 Authentication & authorization | Login aman dan akses berbasis peran. | BR-006 | FR-001 |
| F-02 Employee Management | Kelola data pegawai, departemen, status, dan peran. | BR-001, BR-005 | FR-002 |
| F-03 Letter Management | Buat, simpan draft, lampirkan berkas, submit, cari, dan lihat riwayat surat. | BR-002, BR-004 | FR-003 |
| F-04 Approval Workflow | Tinjau, approve, reject, atau request revision pada surat yang ditugaskan. | BR-003, BR-004 | FR-004 |
| F-05 Dashboard & notification | Ringkasan berbasis peran, antrean tindakan, dan notifikasi dalam aplikasi. | BR-004, BR-008 | FR-005 |
| F-06 Audit trail | Catat aktivitas bisnis yang penting. | BR-007 | FR-006 |

## User Flow

```text
Login → Dashboard sesuai peran
  ├─ HR/Admin → Employee Management → Tambah/Ubah/Nonaktifkan → Audit Log
  ├─ Staff → Letter Management → Draft → Submit → Pending Approval
  │                                  ↑                 ↓
  │                             Need Revision ← Request Revision
  ├─ Manager → Approval Queue → Review → Approve / Reject / Request Revision
  └─ Management → Dashboard → Lihat ringkasan dan status (read-only)
```

## MVP dan Prioritization

| Prioritas | Feature | Alasan |
|---|---|---|
| Must Have | F-01 sampai F-05 dasar: login, role, pegawai, surat, approval satu tingkat, dashboard dan notifikasi in-app | Membentuk alur bisnis inti dan kontrol akses minimal. |
| Must Have | F-06 audit trail untuk tindakan utama | Diperlukan untuk keterlacakan yang menjadi tujuan bisnis. |
| Should Have | Template surat, ekspor daftar, filter lanjutan, notifikasi email | Meningkatkan produktivitas, tetapi alur inti tetap berjalan tanpa fitur ini. |
| Could Have | Approval multi-level/parallel yang dapat dikonfigurasi, SSO, integrasi HRIS | Nilainya tinggi bila kebutuhan tervalidasi, namun membutuhkan discovery dan dependensi tambahan. |
| Won't Have | Payroll, absensi, aplikasi mobile native, tanda tangan tersertifikasi pada MVP | Berbeda dari masalah inti atau memiliki kompleksitas serta kepatuhan tambahan. |

## Non-functional requirements tingkat produk

1. Antarmuka desktop-first dan responsif untuk penggunaan internal umum.
2. Hak akses diterapkan pada setiap halaman dan tindakan, bukan hanya menu.
3. Waktu dan status memakai zona waktu organisasi yang harus dikonfirmasi saat implementasi.
4. Data sensitif tidak ditampilkan pada persona yang tidak berwenang.
