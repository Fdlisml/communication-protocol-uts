# Analisis Encoding dan HTTP Traffic - Product API

## 1. Analisis HTTP Method dan Status Code
*   **GET**: Digunakan untuk mengambil resource data dari server. 
    *   `GET /api/products` mengembalikan **200 OK**, artinya permintaan berhasil dan server mengembalikan *array* berisi list produk.
    *   `GET /api/products/1` mengembalikan **200 OK**, mengambil detail satu produk spesifik.
*   **POST**: Digunakan untuk membuat resource baru.
    *   `POST /api/products` mengembalikan **201 Created**, menandakan data produk baru berhasil disimpan di server. Header `Location: /api/products/4` diberikan oleh server sebagai referensi lokasi resource yang baru saja dibuat.
*   **PATCH**: Digunakan untuk melakukan *partial update* (update sebagian data, dalam hal ini `stock`).
    *   `PATCH /api/products/1` mengembalikan **200 OK**, menandakan modifikasi jumlah stok berhasil dilakukan.

## 2. Analisis HTTP Headers
*   **Content-Type: application/json; charset=utf-8**: Menandakan bahwa *payload* (isi pesan) baik dari *request body* maupun *response body* di-encode dalam format JSON dengan karakter UTF-8.
*   **Content-Length**: Menunjukkan ukuran body response dalam satuan *byte*. Digunakan oleh client (seperti browser atau curl) untuk memastikan seluruh data telah diterima.
*   **Access-Control-Allow-Origin: ***: Ini adalah header CORS (Cross-Origin Resource Sharing) yang bernilai wildcard `*`, artinya endpoint API ini bisa dipanggil dari web *frontend* dengan domain apapun.

## 3. Analisis Format Data (JSON Encoding)
Data ditransfer menggunakan encoding format **JSON (JavaScript Object Notation)**, yang merupakan standar industri untuk REST API karena sifatnya yang ringan (*lightweight*) dan mudah dibaca oleh manusia (*human-readable*).

Contoh struktur *response body* untuk operasi GET detail produk:
```json
{
  "id": 1,
  "name": "Laptop Pro 14",
  "category": "computer",
  "price": 14500000,
  "stock": 10,
  "updatedAt": "2026-06-07T22:39:22+0700"
}
```

**Pembahasan Struktur Data:**
*   **Key-Value Pair**: JSON tersusun atas pasangan kunci dan nilai. Field `"name"` menyimpan *string*, sedangkan `"price"` menyimpan *number*.
*   **Tipe Data Native**: JSON dapat membedakan nilai angka numerik (`14500000`) dengan teks *string* (`"computer"`). Teks harus diapit oleh tanda kutip ganda.
*   **Waktu (Timestamp)**: Waktu direpresentasikan sebagai *string* dengan format terstandarisasi ISO-8601 (contoh: `2026-06-07T22:39:22+0700`), sehingga mudah diparsing oleh berbagai macam bahasa pemrograman.
*   **Validasi**: Karena `Content-Type` adalah `application/json`, maka format payload harus benar. Saat mengirim data, harus mematuhi aturan JSON *syntax* (contoh: koma di akhir element tidak diperbolehkan). Server berhasil mem-parsing objek JSON tersebut dan mengupdate state di *backend*.
