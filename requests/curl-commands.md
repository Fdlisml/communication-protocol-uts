# Curl Commands - Product API

Berikut adalah command curl yang dijalankan pada demo app (berjalan di localhost:8088).

### 1. GET Daftar Produk
```bash
curl -i -X GET http://localhost:8088/api/products
```

### 2. GET Detail Produk
```bash
curl -i -X GET http://localhost:8088/api/products/1
```

### 3. POST Tambah Produk
```bash
curl -i -X POST http://localhost:8088/api/products \
-H "Content-Type: application/json" \
-d '{"name":"Smartwatch AI","category":"wearable","price":2000000,"stock":15}'
```

### 4. PATCH Update Stok Produk (Sesuai dengan implementasi server untuk update sebagian data)
```bash
curl -i -X PATCH http://localhost:8088/api/products/1 \
-H "Content-Type: application/json" \
-d '{"stock":10}'
```
