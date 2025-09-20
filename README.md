# Starter
- pipenv shell
- pipenv install django==4.2
- django-admin startproject DicoEvent .
- buat database bernama dico_event menggunakan PostgreSQL
    ```
    psql -U postgres
    CREATE DATABASE dico_event;
    GRANT ALL PRIVILEGES ON DATABASE "dico_event" TO developer;
    ALTER DATABASE "dico_event" OWNER TO developer;
    ```
- 

# Ketentuan Project
## Pengantar

Setiap kriteria dapat bernilai **0 sampai 4 points (pts)**.  
Untuk lulus dari submission ini, setidaknya Anda harus mendapatkan **2 points dari setiap kriteria**.  
Submission akan ditolak jika masih terdapat kriteria dengan nilai **0 points**.

---

## Kriteria 1: Menggunakan Database untuk Menyimpan Data

RESTful API yang Anda bangun haruslah menyimpan data di **database PostgreSQL**.

### Reject (0 pts)
- Data tidak disimpan di database apa pun, menunjukkan tidak ada implementasi database.
- Tidak ada konfigurasi database dalam proyek, atau konfigurasi yang ada tidak lengkap dan tidak berfungsi dengan baik.
- Menggunakan database selain PostgreSQL.
- Terdapat error dalam pengujian mandatory Postman.

### Basic (2 pts)
- Data berhasil disimpan di PostgreSQL.
- Menggunakan Django ORM pada tingkat dasar, terbatas pada operasi CRUD sederhana tanpa memanfaatkan fitur ORM lanjutan seperti limit, ordering, dan filter.
- Pengujian mandatory Postman tidak ada yang error.

### Skilled (3 pts)
- Memenuhi ketentuan nilai sebelumnya.
- Normalisasi database telah dilakukan dengan baik dengan setidaknya terdapat beberapa relasi antar tabel.
- Merancang ERD (Entity Relationship Diagram) dan melampirkannya dalam proyek dalam bentuk image jpg/png dengan format nama berkas: **ERD-DicoEvent-versi-1**.
- Menambahkan satu *unique constraint* di salah satu atribut di sebuah tabel. Misalnya, untuk atribut **email** di tabel **users**.

### Advanced (4 pts)
- Memenuhi ketentuan nilai sebelumnya.
- Kredensial database disimpan di **environment variables** untuk memastikan keamanan data.
- Environment variables harus menggunakan nama berikut:
  - `DATABASE_NAME`
  - `DATABASE_USER`
  - `DATABASE_PASSWORD`
  - `DATABASE_HOST`
  - `DATABASE_PORT`
- Menggunakan Django ORM yang lebih lanjut, dengan implementasi beberapa query lanjutan seperti limit, ordering, dan filter.
- Menggunakan `uuid` sebagai id di tabel.
- Semua pengujian Postman, baik mandatory maupun opsional (jika ada), bebas dari error.

---

## Kriteria 2: Menerapkan Autentikasi dan Otorisasi pada RESTful API Django

### Reject (0 pts)
- Tidak ada implementasi autentikasi dan otorisasi dalam RESTful API.
- Menggunakan metode autentikasi yang tidak sesuai, seperti sessions atau cookies.
- Tidak ada implementasi RBAC (Role-based access control).
- Terdapat error dalam pengujian mandatory Postman.

### Basic (2 pts)
- Terdapat implementasi autentikasi menggunakan **JWT**.
- Terdapat implementasi RBAC dengan role dasar pengguna: **user**, **admin**, dan **superuser**.  
  Rancangan otorisasinya sebagai berikut:
  - **Superuser** → akses penuh ke semua fitur.
  - **Admin** → dapat mengelola:
    - Event (CRUD)
    - Ticket (CRUD)
    - Registration (CRUD)
    - Payment (CRUD)
  - **User** → dapat melakukan:
    - Mendaftar akun dan login.
    - Melihat daftar dan detail Event.
    - Melihat daftar dan detail Ticket.
    - Melakukan dan melihat detail Registrations.
    - Melakukan dan melihat detail Payment.
- Pengujian mandatory Postman tidak ada yang error.

### Skilled (3 pts)
- Memenuhi ketentuan nilai sebelumnya.
- Access Token yang dihasilkan JWT memiliki masa berlaku hingga **3 jam** setelah diterbitkan.
- Mengonfigurasi autentikasi JWT sebagai default di `settings.py`.

### Advanced (4 pts)
- Memenuhi ketentuan nilai sebelumnya.
- Membuat **custom model User**.
- Implementasi RBAC mencakup role tambahan seperti **organizer**.
  - **Organizer** dapat mengelola entitas Event miliknya (mengubah dan menghapus data).
- Terdapat implementasi **custom permission** di views.
- Semua pengujian Postman, baik mandatory maupun opsional (jika ada), bebas dari error.


# Pengujian
- Terletak pada folder postman