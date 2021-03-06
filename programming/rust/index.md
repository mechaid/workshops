---
title: Bahasa Pemrograman Rust
layout: workshop-index
description: Bahasa pemrograman Rust
course-parent: Programming
course-parent-url: ../
tags: rust
---

https://doc.rust-lang.org/rust-by-example/

# Fitur Bahasa

## Module
- https://doc.rust-lang.org/reference/items/modules.html
- https://doc.rust-lang.org/rust-by-example/mod.html

Module adalah wadah untuk kumpulan Item (Struct, Function, Trait, Impl, Module lainnya).

```rust
mod perusahaan {

    pub struct Karyawan {
        pub nama: String,
        pub jabatan: String,
        gaji: i32,
    }
    
    pub fn lihat_detail_perusahaan() {
        println!("Lihat detail perusahaan");
    }
    
    fn lihat_rahasia_perusahaan() {
        println!("Lihat rahasia perusahaan");
    }
    
    mod divisi_marketing {
        pub fn lihat_iklan_perusahaan() {
            println!("Lihat iklan perusahaan");
        }
        
        fn menyiapkan_strategi_marketing() {
            println!("Menyiapkan strategi marketing");
        }
    }
}
```

### Cara Mengakses Module

- https://doc.rust-lang.org/reference/items/modules.html#module-source-filenames

Ada beberapa cara untuk mengakses Module. 

| Alamat Module yang ditulis di script | Alamat di Filesystem | Isi File |
| --- | --- | --- |
| crate | src/lib.rs | mod jualan_baso; |
| crate::jualan_baso | src/jualan_baso.rs atau src/jualan_baso/mod.rs pilih salah satu | mod persiapan; |
| crate::jualan_baso::persiapan | src/jualan_baso/persiapan.rs | |


## Pointer

## Generic
- Fungsi utama dari generic adalah membuat type yang digunakan di dalam function, struct, enum, method menjadi dinamis
- Variabel untuk generic itu bebas gak harus E dan T
- Ada type parameter ada value parameter
- Salah satu kegunaannya adalah agar tipe dari parameter input output **Function**, maupun atribut dari **Struct** menjadi dinamis, tidak terikat type tertentu
- Generic menggunakan angle bracket \<\>
- Dalam implementasi penggunaan generic, untuk tahu bagaimana type yang didefinisikan digunakan, perlu melihat dokumentasi item nya terlebih dahulu untuk menelusuri bagaimana type tersebut digunakan

```rust
struct Koordinat<TipeX> {
    x: TipeX,
    y: TipeX,
}
```

- https://doc.rust-lang.org/book/ch10-01-syntax.html

https://stackoverflow.com/questions/58027416/what-are-the-brackets-before-a-function-in-rust

## Struct

- https://doc.rust-lang.org/stable/rust-by-example/custom_types/structs.html

Struct adalah tipe data khusus untuk mengelompokkan data yang saling terkait. Ada tiga bentuk penggunaan Struct yaitu sebagai :
- Tuple
- Struct tradisional seperti pada bahasa C. Terdiri atas Field dengan Key dan Value tipe data tertentu.
- Unit, struct tanpa atribut data

```rust
// Pendefinisian Struct (Struct definition)

// Struct tradisional
struct Penduduk {
    nama: String,
    jenis_kelamin: i32,
    umur: i32,
}

// Struct unit
struct Bahasa;

// Struct tuple
struct LongLat(f32, f32);

// Penggunaan Struct (Struct instantiation)
let penduduk1 = Penduduk {
    nama: String::from("Lamsijan"),
    jenis_kelamin: 1,
    umur: 24,
}
```

### Impl
Mendefinisikan method untuk Struct dan Enum

## Trait
- Trait adalah kumpulan method yang dapat dikaitkan pada Struct
- Trait dapat menjadi parameter function
```rust
pub fn bersuara(a: &impl Benda) {
    println!("Bersuara seperti ini {}", a.suara());
}
```

## Attributes

## Types

Type pada setiap item di Rust menunjukan operasi-operasi yang dapat dilakukan item tersebut, dan bagaimana interpretasi dari memory-nya.

Referensi:
- https://doc.rust-lang.org/reference/types.html

### Deklarasi Type

### Type Alias

Dapat digunakan untuk mempersingkat dan menyederhanakan type. Contoh :
```rust
type DBCon = Connection<PgConnectionManager<NoTls>>;
```

### Option

### Result

## Ownership

## Macros

## Future

# Contoh Script dan Cara Memahaminya

## Contoh 1

```rust
impl<F> FilterBase for BoxingFilter<F>
where
    F: Filter,
    F::Future: Send + 'static,
{
    type Extract = F::Extract;
    type Error = F::Error;
    type Future = Pin<Box<dyn Future<Output = Result<Self::Extract, Self::Error>> + Send>>;

    fn filter(&self, _: Internal) -> Self::Future {
        Box::pin(self.filter.filter(Internal).into_future())
    }
}
```

- Mengimplementasikan Trait FilterBase ke Struct BoxingFilter, dengan batasan :
  - F adalah Struct / Enum yang mengimplementasikan Trait Filter
  - F::Future adalah Struct / Enum yang mengimplementasikan Trait Send dan 'static
  
- Mendefinisikan Type Alias :
  - F::Extract sebagai Type Extract
  - F::Error sebagai Type Error
  - Pin<Box<dyn Future<Output = Result<Self::Extract, Self::Error>> + Send>> sebagai Type Future
