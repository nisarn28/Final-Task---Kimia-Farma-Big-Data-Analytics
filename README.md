### Big Data Analytics Kimia Farma x Rakamin Academy Batch March 2024

#### Program Introduction

Project Based Internship (PBI) adalah sebuah program magang virtual dari Rakamin Academy yang berkolaborasi dengan beberapa perusahaan yang bertujuan menggali potensi dan menambah pengalaman bagi peserta PBI. Dalam program ini, saya berperan sebagai Big Data Analytics di Kimia Farma yang menganalisis dan melaporkan data mengenai Performance Analytics Kimia Farma di Tahun 2020 - 2023.



#### Challenges

- Membuat tabel analisa
- Membuat visualisasi berupa dashboard Performance Analytics Kimia Farma di Tahun 2020 - 2023

#### Dataset
- Final transaction
- Inventory
- Kantor Cabang
- Product
### Tabel Analisa

```sh
-- Membuat tabel analisa

CREATE TABLE dataset_kimia_farma AS
SELECT 
    ft.transaction_id,
    ft.date, 
    ft.branch_id, 
    kc.branch_name,
    kc.kota,
    kc.provinsi,
    kc.rating,
    ft.customer_name,
    p.product_id,
    p.product_name,
    ft.price,
    ft.discount_percentage,
CASE
  WHEN ft.price <= 50000 THEN 0.10
  WHEN ft.price > 50000 - 100000 THEN 0.15
  WHEN ft.price > 100000 - 300000 THEN 0.20
  WHEN ft.price > 300000 - 500000 THEN 0.25
  WHEN ft.price > 500000 THEN 0.30
ELSE 0.30
END AS presentase_gross_laba, 
(ft.price - (ft.price * ft.discount_percentage)) AS nett_sales,
(ft.price * (1 - ft.discount_percentage) * CASE
                                              WHEN ft.price <= 50000 THEN 0.10
                                              WHEN ft.price > 50000 - 100000 THEN 0.15
                                              WHEN ft.price > 100000 - 300000 THEN 0.20
                                              WHEN ft.price > 300000 - 500000 THEN 0.25
                                              WHEN ft.price > 500000 THEN 0.30
                                            ELSE 0.30
                                              END) AS nett_profit,
ft.rating AS rating_transaksi
FROM 
    dataset_kimia_farma.kf_final_transaction AS ft 
LEFT JOIN 
    dataset_kimia_farma.kf_kantor_cabang AS kc ON ft.branch_id = kc.branch_id
LEFT JOIN 
    dataset_kimia_farma.kf_product AS p ON ft.product_id = p.product_id;
```

#### Visualisasi Data
<img width="448" alt="daahboard" src="https://github.com/nisarn28/Final-Task---Kimia-Farma-Big-Data-Analytics/assets/165548135/bf7d5a01-bc84-4ad3-a713-11c0172771fe">
