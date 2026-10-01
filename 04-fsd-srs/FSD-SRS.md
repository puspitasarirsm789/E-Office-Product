# Functional Specification Document / Software Requirements Specification: E-Office

## Konvensi status

`Draft` → `Pending Approval` → `Approved` atau `Rejected`; approver dapat mengubah `Pending Approval` menjadi `Need Revision`, lalu Staff memperbaiki dan submit ulang. Semua waktu ditampilkan dalam zona waktu organisasi yang dikonfigurasi.

## FR-001 Authentication dan Authorization

**Functional Requirement.** Sistem harus mengautentikasi pengguna terdaftar dan menentukan akses halaman maupun tindakan berdasarkan perannya.

**Actor:** Staff, Manager/Approver, HR/Admin, Management.

**Main Flow:** (1) Pengguna membuka Login. (2) Pengguna mengisi email dan kata sandi. (3) Sistem memvalidasi kredensial dan status akun. (4) Sistem membuat sesi aktif dan mengarahkan pengguna ke Dashboard sesuai peran.

**Alternative Flow:** Pengguna mencoba halaman yang tidak berwenang; sistem menampilkan akses ditolak dan tidak menampilkan data halaman tersebut.

**Exception Flow:** Kredensial salah atau akun nonaktif; sistem tidak membuat sesi dan menampilkan pesan umum tanpa menyatakan akun mana yang valid.

**Validation:** email wajib dan berformat valid; kata sandi wajib; tombol Login aktif hanya saat field terisi; sesi yang kedaluwarsa harus meminta login kembali.

**Business Rules:** BRULE-001, BRULE-002. Setiap request sensitif harus memeriksa role di server/API.

**Acceptance Criteria:**

- Given akun aktif dan kredensial valid, When pengguna menekan Login, Then sistem menampilkan Dashboard sesuai role.
- Given kredensial tidak valid, When pengguna menekan Login, Then sistem menolak login tanpa membuat sesi.
- Given Staff membuka URL Employee Management, When sistem mengevaluasi hak akses, Then halaman dan data ditolak.

## FR-002 Employee Management

**Functional Requirement.** HR/Admin harus dapat melihat daftar, menambah, mengubah, dan menonaktifkan pegawai; pengguna lain hanya memperoleh akses yang diizinkan oleh role.

**Actor:** HR/Admin; Staff sebagai pembaca profil sendiri bila diaktifkan.

**Main Flow:** (1) HR/Admin membuka Employee Management. (2) Sistem menampilkan daftar dengan pencarian dan filter status/departemen. (3) HR/Admin memilih Add Employee. (4) HR/Admin mengisi data. (5) Sistem memvalidasi dan menyimpan rekaman aktif serta audit log.

**Alternative Flow:** HR/Admin mengubah data pegawai; sistem menampilkan nilai saat ini, menyimpan perubahan valid, dan membuat audit log.

**Exception Flow:** Email atau Employee ID sudah digunakan; sistem menolak penyimpanan dan menandai field terkait. Pegawai yang menjadi approver aktif tidak dapat dinonaktifkan sebelum penggantinya ditetapkan.

**Validation:** Employee ID, nama, email, departemen, jabatan, status, dan role wajib; Employee ID serta email unik; email valid; departemen harus aktif.

**Business Rules:** BRULE-001, BRULE-002, BRULE-007. Nonaktifkan bersifat soft delete untuk menjaga riwayat.

**Acceptance Criteria:**

- Given seluruh field wajib valid, When HR/Admin menyimpan pegawai baru, Then rekaman aktif muncul pada daftar dan audit log tercatat.
- Given email sudah terdaftar, When HR/Admin menyimpan, Then sistem tidak membuat rekaman dan menampilkan validasi email unik.
- Given pegawai aktif adalah approver departemen, When HR/Admin menonaktifkannya tanpa pengganti, Then sistem menolak tindakan dan menjelaskan alasan.

## FR-003 Letter Management

**Functional Requirement.** Staff harus dapat membuat surat, menyimpan draft, menambahkan lampiran, mengirimkan surat untuk approval, serta melihat status dan riwayat surat yang berhak diaksesnya.

**Actor:** Staff; HR/Admin sesuai hak akses administrasi.

**Main Flow:** (1) Staff membuka Letter Management dan memilih New Letter. (2) Staff mengisi subject, type, recipient, content, dan lampiran opsional. (3) Staff memilih Save Draft atau Submit. (4) Saat Submit, sistem menentukan approver aktif departemen pengirim, membuat approval Pending, mengubah surat menjadi Pending Approval, dan membuat notifikasi.

**Alternative Flow:** Staff menyimpan Draft lalu melanjutkan pengeditan. Untuk Need Revision, Staff membuka surat, memperbaiki field yang diperlukan, lalu Submit ulang.

**Exception Flow:** Approver tidak tersedia; sistem tidak mengizinkan Submit dan meminta HR/Admin menetapkan approver. Gagal unggah lampiran; sistem tidak menyimpan lampiran gagal dan menjaga field lain tetap ada.

**Validation:** subject 5–150 karakter; type dan recipient wajib; content wajib; maksimal 5 lampiran; ukuran dan format lampiran mengikuti konfigurasi keamanan yang harus dikonfirmasi; hanya pemilik membuat/mengubah Draft atau Need Revision.

**Business Rules:** BRULE-003, BRULE-004, BRULE-006, BRULE-007. Nomor surat dibuat saat status menjadi Approved, mengikuti pola yang dikelola HR/Admin.

**Acceptance Criteria:**

- Given Staff mengisi field wajib valid dan approver aktif tersedia, When Staff menekan Submit, Then surat tersimpan sebagai Pending Approval dan approver menerima notifikasi.
- Given surat masih Draft, When Staff menekan Save Draft, Then surat tersimpan tanpa membuat approval.
- Given surat Need Revision, When Staff memperbaiki dan submit ulang, Then sistem membuat riwayat submit baru dan status menjadi Pending Approval.

## FR-004 Approval Workflow

**Functional Requirement.** Manager/Approver harus dapat meninjau surat yang ditugaskan dan memberikan keputusan yang tercatat.

**Actor:** Manager/Approver.

**Main Flow:** (1) Approver membuka Approval Queue. (2) Sistem menampilkan surat Pending Approval yang ditugaskan kepadanya. (3) Approver membuka detail beserta lampiran dan riwayat. (4) Approver memilih Approve, Reject, atau Request Revision. (5) Sistem memvalidasi, menyimpan keputusan, memperbarui status surat, audit log, dan notifikasi pembuat.

**Alternative Flow:** Approver memfilter queue berdasarkan departemen, type, atau tanggal tanpa mengubah data.

**Exception Flow:** Approver mencoba memutuskan surat yang sudah diputuskan atau tidak ditugaskan kepadanya; sistem menolak dan memuat ulang status terbaru.

**Validation:** keputusan harus salah satu dari tiga aksi; catatan wajib untuk Reject dan Request Revision; hanya approval Pending milik approver aktif yang dapat diputuskan.

**Business Rules:** BRULE-005, BRULE-006, BRULE-007. Keputusan bersifat final pada MVP; perubahan keputusan harus melalui proses admin yang belum termasuk MVP.

**Acceptance Criteria:**

- Given approval Pending milik Manager, When Manager memilih Approve, Then surat menjadi Approved, keputusan tercatat, dan pembuat menerima notifikasi.
- Given Manager memilih Reject tanpa catatan, When Manager mengonfirmasi, Then sistem menolak penyimpanan dan meminta catatan.
- Given Staff mencoba membuka aksi keputusan pada suratnya, When halaman detail ditampilkan, Then aksi approval tidak tersedia.

## FR-005 Dashboard dan Notification

**Functional Requirement.** Sistem harus menampilkan ringkasan yang relevan berdasarkan role serta notifikasi in-app atas tindakan yang membutuhkan perhatian.

**Actor:** Seluruh role.

**Main Flow:** (1) Pengguna berhasil login. (2) Sistem menghitung dan menampilkan kartu ringkasan sesuai role. (3) Pengguna memilih kartu atau notifikasi. (4) Sistem membuka daftar/objek yang relevan dan menandai notifikasi sebagai dibaca.

**Alternative Flow:** Pengguna tetap dapat melihat notifikasi belum dibaca pada ikon notifikasi dan membukanya kemudian.

**Exception Flow:** Tidak ada data; sistem menampilkan empty state yang informatif, bukan nilai atau daftar kosong tanpa konteks.

**Validation:** kartu Management hanya menampilkan data agregat; tautan notifikasi harus melalui pemeriksaan hak akses target.

**Business Rules:** BRULE-006. Notifikasi dibuat minimal saat surat disubmit, disetujui, ditolak, atau membutuhkan revisi.

**Acceptance Criteria:**

- Given Staff memiliki surat Need Revision, When Staff membuka Dashboard, Then kartu dan notifikasi menampilkan jumlah tindakan yang diperlukan.
- Given Manager memiliki tiga approval Pending, When Manager membuka Dashboard, Then angka antrean menunjukkan tiga dan tautan mengarah ke Approval Queue.
- Given Management membuka Dashboard, When sistem memuat data, Then tidak ada aksi edit maupun keputusan yang tersedia.

## FR-006 Audit Trail

**Functional Requirement.** Sistem harus mencatat aktivitas bisnis penting untuk pegawai, surat, dan approval.

**Actor:** Sistem; HR/Admin sebagai pembaca audit yang berwenang.

**Main Flow:** Setelah aktivitas create, update, deactivate, submit, approve, reject, atau request revision berhasil, sistem membuat satu audit log dengan pelaku, waktu, entitas, ID entitas, aksi, dan ringkasan perubahan.

**Alternative Flow:** HR/Admin mencari atau memfilter log menurut rentang waktu, entitas, dan pelaku.

**Exception Flow:** Jika penulisan audit gagal, transaksi bisnis tidak boleh dinyatakan berhasil dan kegagalan harus dicatat sebagai insiden teknis.

**Validation:** field audit berasal dari sistem, tidak dapat diubah melalui UI; detail sensitif mengikuti hak akses.

**Business Rules:** BRULE-007. Audit log retensi dan ekspor adalah Open Question kepatuhan.

**Acceptance Criteria:**

- Given HR/Admin memperbarui departemen pegawai, When perubahan berhasil, Then audit log memuat pelaku, waktu, pegawai, dan ringkasan perubahan.
- Given Manager menyetujui surat, When keputusan tersimpan, Then audit log dan riwayat surat memuat keputusan tersebut.
