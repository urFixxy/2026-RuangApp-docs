# Dokumentasi Repository RuangApp

## 1. Studi Kasus

Aplikasi ini dibuat untuk mempermudah pengelolaan peminjaman ruangan, termasuk pencatatan, persetujuan, dan monitoring peminjaman.

**Tujuan:**
* Mengotomatisasi proses peminjaman ruangan
* Memudahkan admin dan pengguna memantau status peminjaman
* Menyediakan fitur filter dan pencarian

**Scope Fitur:**
* User dapat mengajukan peminjaman ruangan
* Admin dapat melihat, menyetujui, menolak, dan menghapus peminjaman
* Filter dan pencarian berdasarkan status, tanggal, dan ruangan

---

## 2. Arsitektur

Aplikasi menggunakan arsitektur **Client-Server** dengan **frontend React** dan **backend ASP.NET Core Web API**.

**Komponen utama:**
* **Frontend:** React + TypeScript, Tailwind CSS
* **Backend:** ASP.NET Core Web API, PostgreSQL
* **Database:** PostgreSQL untuk penyimpanan data ruangan, peminjaman, dan user

**Diagram Arsitektur:**

```
[Frontend React] <---> [Backend ASP.NET Core API] <---> [Database PostgreSQL]
```

**Alur Data:**
1. User mengirim request (misal tambah peminjaman) melalui UI
2. Frontend memanggil endpoint API terkait
3. Backend memproses request, menyimpan / mengambil data dari database
4. Backend mengembalikan response ke frontend

---

## 3. API Specification

### **Endpoint Utama**

| Method | Endpoint               | Deskripsi                     |
| ------ | ---------------------- | ----------------------------- |
| GET    | `/api/borrowings`      | Ambil daftar semua peminjaman |
| POST   | `/api/borrowings`      | Menambahkan peminjaman baru   |
| PUT    | `/api/borrowings/{id}` | Update status peminjaman      |
| DELETE | `/api/borrowings/{id}` | Hapus peminjaman              |
| GET    | `/api/rooms`           | Ambil daftar ruangan          |

### **Contoh Request & Response**

**GET /api/borrowings**

```json
[
  {
    "id": 1,
    "borrowerName": "Fit",
    "roomId": 2,
    "room": {"id": 2, "roomName": "Ruang Rapat 1"},
    "borrowingDate": "2026-02-17",
    "startTime": "10:00",
    "endTime": "12:00",
    "purpose": "Meeting",
    "status": "Pending"
  }
]
```

---

## 4. Refleksi

**Tantangan:**
* Menangani sinkronisasi data realtime antara user dan admin
* Validasi form dan status peminjaman agar tidak bentrok

**Solusi / Keputusan Teknis:**
* Menggunakan fetch + useEffect di React untuk update list peminjaman
* Status hanya bisa diedit oleh admin
* Hanya admin yang bisa hapus peminjaman

**Pelajaran yang Didapat:**
* Pentingnya arsitektur API yang jelas
* Manajemen state di frontend sangat krusial untuk UX
* Penanganan loading & error harus konsisten
