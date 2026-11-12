# Dokumentasi Latihan JavaScript: Product Detail Page

## 1. Gambaran Umum

Proyek ini merupakan latihan bertahap untuk membangun halaman detail
produk headphone **MW75 for TUMI**. Fokus utamanya bukan sekadar membuat
tampilan, tetapi memahami bagaimana HTML, CSS, JavaScript, DOM, event,
state, dan pengambilan data bekerja bersama.

Pengembangan dibagi menjadi tiga tahap:

1.  **Halaman 1: HTML statis (hard-coded)** --- struktur dan konten
    produk ditulis langsung di HTML.
2.  **Halaman 2: DOM dan Event** --- JavaScript mulai mengubah tampilan
    berdasarkan interaksi pengguna.
3.  **Halaman 3: Fetch API** --- data produk diambil dari API eksternal,
    lalu ditampilkan ke halaman melalui DOM.

Pendekatan ini sengaja bertahap. Setiap halaman menambah satu konsep
utama agar perubahan dari tampilan statis menuju halaman yang dinamis
dapat dipelajari dan diuji secara terpisah.

------------------------------------------------------------------------

## 2. Teknologi dan Pendekatan

  -----------------------------------------------------------------------
  Teknologi                           Peran
  ----------------------------------- -----------------------------------
  HTML5                               Menyusun struktur halaman dan
                                      elemen produk

  Tailwind CSS 4                      Mengatur layout, spacing,
                                      typography, warna, dan responsive
                                      design

  JavaScript                          Mengatur data, logika, interaksi,
                                      dan manipulasi DOM

  DOM API                             Mengakses serta memperbarui elemen
                                      HTML

  Event Listener                      Menjalankan fungsi ketika pengguna
                                      melakukan tindakan

  Fetch API                           Mengambil data dari endpoint
                                      eksternal

  DummyJSON                           Sumber data produk untuk latihan
                                      fetch
  -----------------------------------------------------------------------

### Pendekatan desain: mobile-first

Layout dimulai dari layar kecil, kemudian diperluas untuk layar yang
lebih besar menggunakan breakpoint Tailwind.

Contoh pola yang digunakan:

-   `grid-cols-1`: satu kolom pada ukuran layar dasar.
-   `md:grid-cols-2` atau `lg:grid-cols-2`: dua kolom pada breakpoint
    yang ditentukan.
-   `px-4 sm:px-6 lg:px-8`: padding horizontal bertambah sesuai ukuran
    layar.
-   `overflow-x-auto`: memungkinkan konten tertentu digeser secara
    horizontal pada layar kecil.

Prinsipnya, tampilan mobile menjadi dasar. Tampilan tablet dan desktop
merupakan pengembangan dari layout tersebut, bukan sebaliknya.

------------------------------------------------------------------------

## 3. Halaman 1: HTML Statis (Hard-coded)

### Tujuan

Membangun struktur halaman detail produk tanpa bergantung pada
JavaScript untuk mengisi informasi produk.

Pada tahap ini, konten seperti nama produk, harga, gambar, fitur, dan
pilihan warna sudah ditulis langsung di HTML.

### Bagian halaman

1.  **Header dan navigasi**
    -   Brand Master & Dynamic.
    -   Tombol menu, pencarian, akun, dan keranjang.
2.  **Galeri produk**
    -   Gambar utama headphone.
    -   Thumbnail gambar.
    -   Tombol previous dan next sebagai elemen antarmuka.
3.  **Informasi produk**
    -   Nama: MW75 FOR TUMI.
    -   Deskripsi: Active Noise-Cancelling Wireless Headphones.
    -   Harga: Rp9.500.000.
4.  **Pilihan warna**
    -   Black.
    -   Silver.
5.  **Tombol tambah ke keranjang**
6.  **Fitur produk**
    -   Adaptive ANC.
    -   Lambskin Leather.
    -   40mm Beryllium Drivers.
    -   32 Hours Battery Life.
    -   Bluetooth 5.1.
    -   4 Beamforming Mics.
7.  **Informasi tambahan**
    -   Pengiriman, pengembalian, perlindungan produk, artikel, dan
        spesifikasi.

### Karakteristik tahap ini

-   HTML menjadi sumber utama konten.
-   Nilai produk belum berasal dari API atau database.
-   Elemen tombol sudah tersedia, tetapi keberadaan tombol tidak
    otomatis membuat fungsinya berjalan.
-   Perubahan konten masih dilakukan dengan mengedit HTML secara
    langsung.

**Hasil yang ingin dicapai:** memahami struktur HTML, hubungan
antar-elemen, semantic HTML, dan penyusunan layout responsif sebelum
menambahkan perilaku JavaScript.

------------------------------------------------------------------------

## 4. Halaman 2: DOM dan Event

### Tujuan

Mengubah halaman statis menjadi halaman interaktif. JavaScript digunakan
untuk membaca elemen HTML, menyimpan kondisi tampilan yang sedang aktif,
mendengarkan tindakan pengguna, lalu memperbarui DOM.

Tahap ini menggunakan produk dan harga yang masih ditentukan di dalam
kode.

### 4.1 Pemilihan warna: Black dan Silver

Pengguna dapat memilih dua varian warna:

-   Black.
-   Silver.

Setiap varian memiliki kumpulan gambar sendiri. Ketika warna dipilih,
JavaScript menjalankan beberapa proses:

1.  Mengganti kumpulan gambar aktif.
2.  Mengembalikan indeks gambar ke posisi awal.
3.  Mengganti gambar utama.
4.  Mengganti sumber gambar pada thumbnail.
5.  Memperbarui penanda visual warna yang sedang dipilih.

Objek `productImages` menyimpan daftar gambar berdasarkan varian.
Variabel `activeImage` menyimpan daftar gambar yang sedang digunakan.

### 4.2 Galeri gambar

Galeri memiliki tiga jenis interaksi:

-   **Thumbnail:** pengguna memilih gambar tertentu.
-   **Previous:** berpindah ke gambar sebelumnya.
-   **Next:** berpindah ke gambar berikutnya.

Variabel `currentIndex` menyimpan posisi gambar yang sedang ditampilkan.

Navigasi dibuat melingkar. Jika pengguna menekan previous ketika berada
di gambar pertama, galeri berpindah ke gambar terakhir. Jika pengguna
menekan next ketika berada di gambar terakhir, galeri kembali ke gambar
pertama.

### 4.3 Dropdown / accordion spesifikasi

Bagian spesifikasi menggunakan pola accordion:

-   Pengguna menekan judul bagian.
-   Konten bagian yang dipilih dibuka.
-   Bagian lain ditutup.
-   Atribut `aria-expanded` diperbarui untuk membantu menyampaikan
    status komponen kepada teknologi bantu.
-   Ikon panah ikut berubah arah.

Secara implementasi, elemen yang memiliki class `.accordion-item`
diiterasi, kemudian setiap `.accordion-trigger` diberi event listener.

**Catatan istilah:** komponen pada implementasi ini adalah accordion,
bukan dropdown form. Accordion membuka dan menutup panel konten;
dropdown form biasanya menyediakan daftar opsi untuk dipilih.

### 4.4 Jumlah barang

Pengguna dapat mengatur kuantitas melalui:

-   Tombol tambah (`+`).
-   Tombol kurang (`-`).
-   Input angka secara langsung.

Aturan validasi yang diterapkan:

-   Kuantitas minimal adalah 1.
-   Nilai harus berupa bilangan bulat.
-   Jika nilai tidak valid atau kurang dari 1, nilai dikembalikan
    menjadi 1.

### 4.5 Perhitungan subtotal

Harga produk disimpan dalam variabel `productPrice`.

Rumus:

`Subtotal = Kuantitas × Harga Produk`

Ketika kuantitas berubah, fungsi `updateProductTotal()` menghitung ulang
subtotal dan memperbarui tampilan jumlah barang serta harga.

### 4.6 Keranjang dan total belanja

Ketika tombol tambah ke keranjang ditekan:

1.  JavaScript membaca kuantitas yang dipilih.
2.  Kuantitas ditambahkan ke total barang dalam keranjang.
3.  Nilai pembelian ditambahkan ke total harga keranjang.
4.  DOM diperbarui untuk menampilkan jumlah barang dan total belanja.

Variabel yang digunakan:

-   `totalCartItem`: total unit barang yang sudah ditambahkan.
-   `totalCartPrice`: akumulasi nilai belanja.
-   `cartItem`: elemen DOM untuk menampilkan jumlah barang.
-   `cartTotal`: elemen DOM untuk menampilkan total belanja.

Format Rupiah menggunakan `Intl.NumberFormat()` dengan locale `id-ID`
dan currency `IDR`.

### 4.7 Konsep JavaScript yang dipelajari

  Konsep                  Penggunaan dalam halaman
  ----------------------- ----------------------------------------------------------
  `querySelector()`       Mengambil elemen DOM
  `querySelectorAll()`    Mengambil beberapa elemen sekaligus
  `addEventListener()`    Mendengarkan klik atau input pengguna
  `textContent`           Mengubah teks pada elemen
  `src`                   Mengubah sumber gambar
  `classList`             Menambah dan menghapus class CSS
  `closest()`             Menemukan elemen terdekat yang cocok dari target event
  `forEach()`             Memproses sekumpulan elemen
  `let`                   Menyimpan nilai yang dapat berubah
  Function                Memisahkan logika ke fungsi yang dapat digunakan kembali
  Conditional             Mengatur keputusan berdasarkan kondisi
  `Number()`              Mengubah input menjadi angka
  `Intl.NumberFormat()`   Memformat angka menjadi mata uang Rupiah

### Pemahaman penting: state

Dalam latihan ini, state berarti nilai yang disimpan JavaScript untuk
merepresentasikan kondisi halaman saat ini.

Contoh:

-   `currentIndex`: gambar yang sedang aktif.
-   `activeImage`: kumpulan gambar untuk varian aktif.
-   `totalCartItem`: jumlah barang dalam keranjang.
-   `totalCartPrice`: total nilai keranjang.

State bukan elemen HTML. DOM adalah tampilan yang diperbarui berdasarkan
nilai state tersebut.

**Hasil yang ingin dicapai:** memahami alur interaksi dari tindakan
pengguna, perubahan nilai JavaScript, hingga pembaruan DOM.

------------------------------------------------------------------------

## 5. Halaman 3: Fetch API dan Data Eksternal

### Tujuan

Mempelajari cara mengambil data produk dari API eksternal, mengubah
respons menjadi data JavaScript, menyimpan daftar produk, dan
menampilkan produk berdasarkan indeks yang aktif.

Endpoint latihan:

`https://dummyjson.com/products`

### 5.1 Alur pengambilan data

Urutan proses pada fungsi `getData()`:

1.  Menentukan URL endpoint.
2.  Memanggil `fetch(url)` untuk mengirim HTTP request.
3.  Menunggu respons menggunakan `await`.
4.  Memeriksa apakah respons berhasil.
5.  Mengubah respons menjadi JSON dengan `response.json()`.
6.  Mengambil array produk dari `data.products`.
7.  Menyimpan array tersebut ke `productList`.
8.  Memanggil `tampilkanProduk()` untuk memperbarui halaman.

### 5.2 Struktur data yang digunakan

Respons DummyJSON memiliki objek utama yang berisi daftar produk pada
properti `products`.

Secara konseptual, bentuk data yang dipakai adalah:

``` javascript
{
  products: [
    {
      id: 1,
      title: "Product title",
      price: 100,
      rating: 4.5,
      thumbnail: "https://..."
    }
  ]
}
```

Contoh di atas hanya ilustrasi struktur properti yang digunakan, bukan
salinan respons lengkap API.

Properti yang dibaca pada latihan:

  Properti      Kegunaan
  ------------- -------------------------
  `title`       Nama produk
  `price`       Harga produk
  `rating`      Nilai rating
  `thumbnail`   Gambar thumbnail produk

### 5.3 Menyimpan data dan indeks aktif

Dua variabel utama:

-   `productList`: menampung array produk dari API.
-   `currentIndex`: menentukan produk yang sedang ditampilkan.

Fungsi `tampilkanProduk()` mengambil satu objek produk berdasarkan
`productList[currentIndex]`, kemudian memasukkan nilainya ke elemen HTML
menggunakan `textContent` dan properti `src`.

### 5.4 Navigasi previous dan next

Tombol previous dan next digunakan untuk berpindah antarproduk di dalam
array.

-   Previous mengurangi `currentIndex`.
-   Next menambah `currentIndex`.
-   Ketika mencapai batas array, indeks dikembalikan ke posisi ujung
    yang berlawanan.

Dengan demikian, satu halaman dapat menampilkan produk yang berbeda
tanpa menulis ulang HTML untuk setiap produk.

### 5.5 Konsep JavaScript yang dipelajari

  Konsep              Penggunaan
  ------------------- -------------------------------------
  `fetch()`           Mengirim HTTP request
  `async`             Mendeklarasikan fungsi asynchronous
  `await`             Menunggu hasil operasi asynchronous
  `try...catch`       Menangani error
  `response.json()`   Membaca body respons sebagai JSON
  Array               Menyimpan daftar produk
  Object              Menyimpan properti satu produk
  Array index         Memilih produk berdasarkan posisi
  DOM update          Menampilkan data API ke halaman

### Catatan teknis untuk kode fetch saat ini

Ada beberapa hal yang perlu diperbaiki agar implementasinya lebih tepat:

1.  **Pemeriksaan respons:** `if (!response)` bukan pemeriksaan status
    HTTP. `fetch()` umumnya tetap menghasilkan objek `Response` ketika
    server mengembalikan status seperti 404. Gunakan `if (!response.ok)`
    sebelum membaca JSON.
2.  **Pemanggilan fungsi next:** pada kode saat ini terdapat
    `tampilkanProduk;` yang hanya merujuk fungsi, bukan menjalankannya.
    Seharusnya fungsi dipanggil dengan tanda kurung:
    `tampilkanProduk()`.
3.  **Konsistensi pemanggilan:** `tampilkanProduk()` tidak menerima
    parameter, sehingga pemanggilan cukup menggunakan
    `tampilkanProduk()`.
4.  **Kondisi data kosong:** tombol navigasi sebaiknya tidak memproses
    indeks ketika `productList` masih kosong. Fungsi `tampilkanProduk()`
    sudah memiliki pemeriksaan awal untuk kondisi ini, tetapi event
    navigasi juga perlu dijaga.
5.  **Sumber gambar:** `thumbnail` dari DummyJSON adalah gambar produk
    dari API, bukan galeri foto headphone MW75 lokal. Jadi tahap fetch
    saat ini merupakan latihan menampilkan data produk, belum
    menghubungkan data API ke galeri varian Black dan Silver.

Contoh pemeriksaan respons yang benar:

``` javascript
const response = await fetch(url);

if (!response.ok) {
    throw new Error("Gagal mengambil data produk");
}

const data = await response.json();
```

**Hasil yang ingin dicapai:** memahami perjalanan data dari API sampai
tampil di browser, bukan hanya menghafal sintaks `fetch()`.

------------------------------------------------------------------------

## 6. Perbandingan Tiga Tahap

  -----------------------------------------------------------------------
  Aspek             Halaman 1         Halaman 2         Halaman 3
  ----------------- ----------------- ----------------- -----------------
  Sumber data       HTML              JavaScript lokal  API eksternal

  Konten produk     Ditulis langsung  Nilai ditentukan  Diambil dari API
                                      dalam kode        

  DOM manipulation  Belum menjadi     Ya                Ya
                    fokus                               

  Event listener    Belum menjadi     Ya                Ya
                    fokus                               

  State             Belum diperlukan  Ya                Ya
                    untuk interaksi                     

  Asynchronous      Tidak             Tidak menjadi     Ya
                                      fokus             

  Fetch API         Tidak             Tidak             Ya

  Tujuan utama      Struktur dan      Interaksi dan     Pengambilan dan
                    layout            logika            penyajian data
  -----------------------------------------------------------------------

------------------------------------------------------------------------

## 7. Batasan Implementasi Saat Ini

Penting untuk membedakan fitur yang sudah ada dari fitur yang baru
direncanakan.

### Halaman 1

-   Struktur halaman produk statis sudah dibuat.
-   Pilihan warna tampil, tetapi belum memiliki perilaku JavaScript pada
    versi ini.
-   Tombol galeri dan keranjang masih berupa elemen antarmuka.

### Halaman 2

-   Pilihan warna Black dan Silver mengganti galeri.
-   Thumbnail serta tombol previous/next berfungsi.
-   Accordion spesifikasi dapat dibuka dan ditutup.
-   Kuantitas dapat diubah.
-   Subtotal dan ringkasan keranjang diperbarui.
-   Harga produk masih ditentukan secara lokal dalam JavaScript.

### Halaman 3

-   Data produk diambil dari DummyJSON.
-   Nama, harga, rating, dan thumbnail ditampilkan ke DOM.
-   Navigasi produk menggunakan indeks array.
-   Tahap ini belum menggabungkan seluruh fitur halaman 2 dengan data
    API.

### Fitur yang belum menjadi bagian dari implementasi saat ini

-   Sinkronisasi varian Black/Silver dengan data produk dari API.
-   Keranjang yang menyimpan rincian setiap produk dan varian.
-   Penyimpanan keranjang setelah halaman di-refresh.
-   Validasi stok dan harga dari backend.
-   Proses checkout atau pembayaran.

------------------------------------------------------------------------

## 8. Rekomendasi Urutan Pengembangan Berikutnya

Agar ketiga tahap benar-benar terhubung, urutan pengembangan yang
disarankan:

1.  **Rapikan halaman 3:** perbaiki pemeriksaan `response.ok`,
    pemanggilan fungsi, dan kondisi data kosong.
2.  **Pahami struktur objek API:** periksa satu objek produk menggunakan
    `console.log(data.products[0])` sebelum mengambil propertinya.
3.  **Buat fungsi render yang konsisten:** pisahkan proses mengambil
    data dan proses menampilkan data.
4.  **Gabungkan data dan pilihan varian:** tentukan bagaimana data
    produk, warna, dan gambar disimpan agar tidak saling bertentangan.
5.  **Kembangkan keranjang berbasis array:** simpan item keranjang
    sebagai objek yang memiliki identitas produk, varian, harga, dan
    kuantitas.
6.  **Hitung total dari data keranjang:** hindari hanya mengandalkan
    penambahan angka total secara terpisah. Total sebaiknya dapat
    dihitung ulang dari isi keranjang.
7.  **Tambahkan penyimpanan lokal:** gunakan `localStorage` setelah
    struktur keranjang sudah benar.

Contoh konsep struktur item keranjang untuk tahap berikutnya:

``` javascript
{
  productId: 1,
  title: "MW75 FOR TUMI",
  color: "Black",
  price: 9500000,
  quantity: 2
}
```

Struktur tersebut merupakan rancangan pengembangan, bukan fitur yang
sudah diterapkan pada kode saat ini.

------------------------------------------------------------------------

## 9. Fokus Pembelajaran

Proyek ini melatih beberapa kemampuan inti frontend secara berurutan:

-   Menyusun HTML semantik dan layout responsif.
-   Memahami DOM sebagai representasi struktur HTML di JavaScript.
-   Mengambil elemen dan memperbarui atribut maupun kontennya.
-   Memahami event dan event listener.
-   Mengelola state sederhana.
-   Mengolah array dan object.
-   Membuat fungsi untuk memisahkan tanggung jawab logika.
-   Memahami asynchronous JavaScript melalui `async/await`.
-   Mengambil dan memproses data JSON dari API.
-   Menampilkan data eksternal ke antarmuka.

**Prinsip utama proyek:** jangan hanya mengejar halaman yang terlihat
berfungsi. Pastikan dapat menjelaskan dari mana data berasal, di mana
data disimpan, kapan nilainya berubah, event apa yang memicu perubahan,
dan bagaimana perubahan tersebut ditampilkan ke DOM.
