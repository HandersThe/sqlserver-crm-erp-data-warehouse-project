# **Kaidah Penamaan**

Dokumen ini menguraikan kaidah penamaan yang digunakan untuk schemas, tables, views, columns, and objek lain dalam data warehouse.

## **Table of Contents**

1. [General Principles](#general-principles)
2. [Table Naming Conventions](#table-naming-conventions)
   - [Bronze Rules](#bronze-rules)
   - [Silver Rules](#silver-rules)
   - [Gold Rules](#gold-rules)
3. [Column Naming Conventions](#column-naming-conventions)
   - [Surrogate Keys](#surrogate-keys)
   - [Technical Columns](#technical-columns)
4. [Stored Procedure](#stored-procedure-naming-conventions)
---

## **General Principles**

- **Kaidah Penamaan**: Menggunakan snake_case, dengan huruf kecil dan garis bawah (`_`) untuk memisahkan kata.
- **Bahasa**: Menggunakan Bahasa Inggris untuk semua nama.
- **Hindari kata-kata yang Dicadangkan**: Jangan gunakan kata-kata yang dicadangkan SQL sebagai nama objek.

## **Table Naming Conventions**

### **Bronze Rules**
- Semua nama harus dimulai dengan nama sistem sumber, dan nama tabel harus sesuai dengan nama aslinya tanpa mengganti nama.
- **`<sourcesystem>_<entity>`**  
  - `<sourcesystem>`: Nama dari sistem sumber (misal `crm`, `erp`).  
  - `<entity>`: Nama table dari sistem sumber.  
  - Contoh: `crm_customer_info` → Informasi pelanggan dari sistem CRM.

### **Silver Rules**
- Semua nama harus dimulai dengan nama sistem sumber, dan nama tabel harus sesuai dengan nama aslinya tanpa mengganti nama.
- **`<sourcesystem>_<entity>`**  
  - `<sourcesystem>`: Nama dari sistem sumber (misal `crm`, `erp`).  
  - `<entity>`: Nama table dari sistem sumber.  
  - Contoh: `crm_customer_info` → Informasi pelanggan dari sistem CRM.

### **Gold Rules**
- Semua nama harus menggunakan nama yang bermakna dan selaras dengan bisnis untuk table, dimulai dengan awalan kategori.
- **`<category>_<entity>`**  
  - `<category>`: Menjelaskan peran table, seperti `dim` (dimensi) atau `fact` (fakta).  
  - `<entity>`: Nama deskriptif table, selaras dengan domain bisnis (misalnya `customers`, `products`, `sales`).  
  - Contoh:
    - `dim_customers` → Table dimensi untuk data pelanggan.  
    - `fact_sales` → Table fakta yang berisi transaksi penjualan.  

#### **Glossary of Category Patterns**

| Pattern     | Meaning                           | Example(s)                              |
|-------------|-----------------------------------|-----------------------------------------|
| `dim_`      | Table dimensi                  | `dim_customer`, `dim_product`           |
| `fact_`     | Table fakta                       | `fact_sales`                            |
| `report_`   | Table laporan                     | `report_customers`, `report_sales_monthly`   |

## **Column Naming Conventions**

### **Surrogate Keys**  
- Semua kunci primer dalam table dimensi harus menggunakan akhiran `_key`.
- **`<table_name>_key`**  
  - `<table_name>`: Mengacu pada nama table atau entitas tempat kunci tersebut berada.  
  - `_key`: Akhiran yang menunjukkan bahwa kolom ini adalah surrogate key.  
  - Contoh: `customer_key` → Surrogate key dalam table `dim_customers`.
  
### **Technical Columns**
- Semua kolom teknis harus dimulai dengan awalan `dwh_`, diikuti dengan nama deskriptif yang menunjukkan tujuan kolom tersebut.
- **`dwh_<column_name>`**  
  - `dwh`: Awalan khusus untuk metadata yang dihasilkan sistem.  
  - `<column_name>`: Nama deskriptif yang menunjukkan tujuan kolom.  
  - Contoh: `dwh_load_date` → Kolom yang dihasilkan sistem digunakan untuk menyimpan tanggal ketika catatan dimuat.
 
## **Stored Procedure**

- Semua prosedur tersimpan yang digunakan untuk memuat data harus mengikuti pola penamaan:
- **`load_<layer>`**.
  
  - `<layer>`: Mewakili lapisan yang sedang dimuat, seperti `bronze`, `silver`, atau `gold`.
  - Contoh: 
    - `load_bronze` → Prosedur tersimpan untuk memuat data ke dalam lapisan Bronze.
    - `load_silver` → Prosedur tersimpan untuk memuat data ke dalam lapisan Silver.
