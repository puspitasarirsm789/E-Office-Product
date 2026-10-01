# Product Backlog: E-Office

Prioritas menggunakan MoSCoW dari PRD. Story point memakai skala Fibonacci dan merupakan estimasi relatif, bukan durasi.

| ID | Epic | User Story | Priority | SP | Referensi | Acceptance Criteria ringkas |
|---|---|---|---|---:|---|---|
| US-001 | Authentication | As a Staff, I want to log in with my active account, so that I can access my work area securely. | Must | 5 | FR-001 | Kredensial valid membuka dashboard sesuai role; kredensial salah tidak membuat sesi. |
| US-002 | Authorization | As an HR/Admin, I want system access restricted by role, so that sensitive actions are protected. | Must | 8 | FR-001 | Akses halaman dan API yang tidak berwenang ditolak. |
| US-003 | Employee | As an HR/Admin, I want to add an employee, so that the employee can be managed in a central directory. | Must | 5 | FR-002 | Field wajib valid disimpan; ID dan email unik; audit tercatat. |
| US-004 | Employee | As an HR/Admin, I want to edit employee information, so that directory data remains accurate. | Must | 5 | FR-002 | Perubahan valid tersimpan dan tercatat; email duplikat ditolak. |
| US-005 | Employee | As an HR/Admin, I want to deactivate an employee safely, so that former employees lose access without losing history. | Must | 5 | FR-002 | Soft delete; approver aktif tanpa pengganti tidak dapat dinonaktifkan. |
| US-006 | Employee | As an HR/Admin, I want to search and filter employees, so that I can find records efficiently. | Should | 3 | FR-002 | Pencarian nama/ID dan filter departemen/status memperbarui daftar. |
| US-007 | Letter | As a Staff, I want to create a letter draft, so that I can complete it before asking for approval. | Must | 5 | FR-003 | Field draft tersimpan tanpa approval; hanya pemilik dapat mengedit. |
| US-008 | Letter | As a Staff, I want to attach supporting files to a letter, so that the approver has necessary context. | Must | 5 | FR-003 | Lampiran valid terunggah; lampiran gagal tidak disimpan. |
| US-009 | Letter | As a Staff, I want to submit a completed letter, so that it enters the approval workflow. | Must | 8 | FR-003 | Approver aktif ditetapkan; status Pending Approval dan notifikasi dibuat. |
| US-010 | Letter | As a Staff, I want to view my letters and their histories, so that I know their latest status. | Must | 5 | FR-003 | Daftar hanya menampilkan surat yang berhak diakses; riwayat status terlihat. |
| US-011 | Approval | As a Manager/Approver, I want to view my pending approval queue, so that I can prioritize decisions. | Must | 5 | FR-004 | Hanya surat Pending yang ditugaskan tampil; filter tidak mengubah data. |
| US-012 | Approval | As a Manager/Approver, I want to approve a letter, so that approved work can proceed. | Must | 5 | FR-004 | Status Approved, keputusan dan notifikasi pembuat tercatat. |
| US-013 | Approval | As a Manager/Approver, I want to reject or request revision with a note, so that the requester knows what to do. | Must | 5 | FR-004 | Catatan wajib; status dan riwayat diperbarui sesuai aksi. |
| US-014 | Dashboard | As a Staff, I want to see my pending actions on a dashboard, so that I can act without checking every letter. | Must | 3 | FR-005 | Kartu dan tautan mencerminkan surat Need Revision atau Pending milik pengguna. |
| US-015 | Dashboard | As a Manager/Approver, I want to see my pending approval count, so that I do not miss requests. | Must | 3 | FR-005 | Jumlah sesuai queue dan tautan ke daftar approval. |
| US-016 | Dashboard | As Management, I want to see read-only operational summaries, so that I can monitor process health. | Must | 5 | FR-005 | Data agregat tampil; tidak ada aksi edit atau approval. |
| US-017 | Notification | As a user, I want in-app notifications for important status changes, so that I can respond promptly. | Must | 5 | FR-005 | Submit, keputusan, dan revisi membuat notifikasi yang dapat dibuka. |
| US-018 | Audit | As an HR/Admin, I want to review audit logs, so that I can trace important changes and decisions. | Must | 8 | FR-006 | Create/update/deactivate/approval tercatat; log tidak dapat diedit. |
| US-019 | Letter | As an HR/Admin, I want to manage letter templates, so that recurring letters are consistent. | Should | 8 | PRD F-03 | Template dapat dipilih dan mengisi konten awal; tidak mengubah surat yang sudah submit. |
| US-020 | Integration | As a user, I want to sign in through SSO, so that I do not manage a separate password. | Could | 13 | PRD F-01 | SSO hanya diaktifkan setelah penyedia identitas dan aturan akses disetujui. |
