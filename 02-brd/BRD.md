# Business Requirements Document: E-Office

## Tujuan bisnis

Meningkatkan efisiensi tata usaha dengan satu proses yang dapat ditelusuri untuk data pegawai dan surat internal, tanpa menjadikan asumsi case study sebagai kebijakan perusahaan.

## Stakeholder

| Stakeholder | Peran dan kepentingan |
|---|---|
| Sponsor bisnis / Management | Menetapkan sasaran pilot, menerima ringkasan operasional. |
| HR/Admin | Pemilik operasional data pegawai dan konfigurasi administratif. |
| Staff | Pengguna yang membuat surat serta mengakses informasi yang diizinkan. |
| Manager/Approver | Pengambil keputusan atas surat dari unitnya. |
| IT/Security | Menetapkan akses, keamanan, backup, dan kesiapan operasional. |

## Business Requirements

Prioritas menggunakan MoSCoW. Seluruh requirement berikut ditetapkan sebagai Must Have karena dibutuhkan untuk menghasilkan workflow MVP yang lengkap dan terkendali; urutan implementasi tetap mengikuti dependency teknis yang disepakati tim.

| ID | Requirement | Business Impact | Priority |
|---|---|---|---|
| BR-001 | Organisasi harus memiliki sumber data pegawai terpusat untuk mengurangi duplikasi dan ketidaksesuaian informasi antar-unit. | Tinggi. Menjadi dasar identitas pengguna, kepemilikan surat, dan kualitas administrasi lintas unit. | Must Have |
| BR-002 | Staff harus dapat membuat dan mengajukan surat internal secara digital agar statusnya dapat dipantau tanpa konfirmasi manual. | Tinggi. Memindahkan proses inti dari media tersebar ke alur yang terukur dan dapat dilacak. | Must Have |
| BR-003 | Surat yang memerlukan persetujuan harus dapat ditinjau oleh Manager/Approver yang berwenang sebelum didistribusikan. | Tinggi. Menjaga kontrol manajerial dan akuntabilitas keputusan atas surat. | Must Have |
| BR-004 | Pihak yang berwenang harus dapat mengetahui surat yang menunggu tindakan, disetujui, ditolak, atau perlu direvisi. | Tinggi. Mengurangi follow-up manual dan risiko surat tertunda tanpa pemilik tindakan yang jelas. | Must Have |
| BR-005 | HR/Admin harus dapat mengelola data pegawai, departemen, dan akses pengguna sesuai perannya. | Tinggi. Memastikan sumber data dan struktur organisasi tetap akurat serta dapat dikelola. | Must Have |
| BR-006 | Sistem harus membatasi akses terhadap data dan tindakan berdasarkan peran serta departemen bila relevan. | Tinggi. Mengurangi risiko akses tidak berwenang terhadap data pegawai dan dokumen internal. | Must Have |
| BR-007 | Sistem harus menyimpan jejak aktivitas penting agar perubahan dan keputusan dapat ditelusuri. | Tinggi. Mendukung audit, investigasi insiden, dan akuntabilitas proses. | Must Have |
| BR-008 | Management harus memperoleh ringkasan indikator surat dan data pegawai untuk pemantauan operasional. | Tinggi. Memberikan visibilitas proses untuk pengambilan keputusan dan evaluasi hasil pilot. | Must Have |

## Business Rules

| ID | Aturan |
|---|---|
| BRULE-001 | Satu pengguna hanya boleh memakai satu akun aktif dan satu identitas pegawai aktif pada satu waktu. |
| BRULE-002 | Hanya HR/Admin yang dapat membuat, mengubah, menonaktifkan data pegawai dan menetapkan peran. |
| BRULE-003 | Surat berstatus Draft tidak dapat ditinjau atau didistribusikan; surat harus disubmit terlebih dahulu. |
| BRULE-004 | Surat Submitted wajib memiliki approver yang aktif dan ditetapkan berdasarkan departemen pengirim. |
| BRULE-005 | Keputusan approval harus menyimpan waktu, pelaku, dan catatan; catatan wajib untuk Reject atau Request Revision. |
| BRULE-006 | Surat Approved bersifat read-only bagi Staff, kecuali proses revisi resmi ditetapkan pada fase lanjutan. |
| BRULE-007 | Semua perubahan penting pada pegawai dan surat dicatat dalam audit log yang tidak dapat diedit pengguna bisnis. |

## Assumption

1. MVP digunakan untuk pegawai internal yang telah terdaftar.
2. Satu approver aktif per departemen cukup untuk workflow MVP.
3. Notifikasi dalam aplikasi adalah kanal minimum; email belum diasumsikan tersedia.
4. HR/Admin bertanggung jawab atas kualitas data awal dan kebijakan nomor surat.

## Constraint

1. Informasi proses saat ini, volume pengguna, dan sistem eksisting tidak tersedia.
2. MVP tidak memasukkan payroll, absensi, maupun integrasi eksternal.
3. Kebijakan retensi dan klasifikasi dokumen belum diberikan sehingga harus dikonfirmasi sebelum produksi.

## Risk

Risiko detail dan mitigasi terdapat di Supporting Documents. Risiko utama: kualitas migrasi data, rendahnya adopsi, approval yang terlambat, akses berlebih, serta perubahan kebutuhan approval setelah pembangunan dimulai.
