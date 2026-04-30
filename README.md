1. Bagian Head dan Styling (CSS)
    Bagian ini mengatur kerangka dokumen dan tampilan visual.
 <!DOCTYPE html> & <html lang="id">: 
   Mendefinisikan dokumen sebagai HTML5 dengan bahasa pengantar Indonesia.

 <style>:
    body: Mengatur font utama (Arial), margin, dan warna latar belakang abu-abu muda.
    form: Memberikan kotak putih, padding, sudut melengkung (border-radius), dan efek bayangan agar terlihat melayang di atas latar belakang.
    input, textarea, select: Mengatur agar elemen input memenuhi lebar form (100%) dengan jarak (margin) yang konsisten.
    .submit, .reset, .btn-edit, .btn-delete: Mengatur pewarnaan tombol (Hijau untuk simpan, Kuning untuk reset, Biru untuk edit, dan Merah untuk hapus).
    table: Mengatur tabel agar memenuhi lebar layar dengan border-collapse agar garis tabel tidak terlihat ganda.

2. Struktur Body (HTML)
   Struktur input dan output data.
   <h2>Form Data Mahasiswa</h2>: Judul formulir.
   <form id="formMahasiswa">: Wadah input data. Memiliki ID untuk ditangkap oleh JavaScript.
   Input NIM & Nama: Menggunakan atribut required agar tidak boleh kosong.
   Input Alamat: Menggunakan tag <input> (biasanya alamat menggunakan <textarea>, namun di sini memakai input teks biasa).
   Jenis Kelamin: Menggunakan radio button. Atribut name="jk" yang sama memastikan hanya satu pilihan yang bisa dipilih.
   Tanggal Lahir: Terdiri dari tiga <select> (tanggal, bulan, tahun). Data tanggal dan tahun akan diisi secara otomatis lewat JavaScript.

Bagian Pencarian:
  Input id="searchInput" dengan event onkeyup="searchTable()". Ini artinya fungsi pencarian akan berjalan setiap kali pengguna melepas tombol keyboard.
  Tabel Data:
  Memiliki <thead> untuk judul kolom.
  <tbody id="tableBody">: Bagian ini kosong, karena akan diisi secara dinamis oleh JavaScript berdasarkan data di LocalStorage.

3. Logika JavaScript
   Inilah "otak" dari aplikasi ini.

A. Inisialisasi dan Dropdown
   JavaScript
   for (let i = 1; i <= 31; i++) { ... }
   for (let i = 1990; i <= 2026; i++) { ... }
   Dua loop ini berfungsi mengisi opsi (dropdown) angka 1-31 untuk tanggal dan tahun 1990-2026 ke dalam elemen HTML secara otomatis saat halaman dimuat.

B. Event Listener Submit
   JavaScript
   form.addEventListener("submit", function(e) {
     e.preventDefault(); // Mencegah halaman refresh saat tombol diklik
     // Mengambil semua nilai dari input ke dalam satu objek 'dataMahasiswa'
     const dataMahasiswa = { ... };
     saveToLocalStorage(dataMahasiswa); // Simpan ke storage
     form.reset(); // Bersihkan form
     displayData(); // Update tampilan tabel
  }); e.preventDefault() sangat krusial agar data tidak hilang karena page reload bawaan form HTML.

C. Fungsi Simpan (Create/Update)
   JavaScript
   function saveToLocalStorage(obj) {
     let list = JSON.parse(localStorage.getItem("mhsList")) || [];
     const index = list.findIndex(item => item.nim === obj.nim);
     if(index !== -1) {
        list[index] = obj; // Jika NIM sudah ada, timpa data lama (Update)
       } else {
         list.push(obj); // Jika NIM baru, tambahkan ke array (Create)
       }
        localStorage.setItem("mhsList", JSON.stringify(list));
    }
   Data di LocalStorage disimpan dalam bentuk string, sehingga perlu JSON.parse saat mengambil dan JSON.stringify saat menyimpan.

D. Fungsi Tampil Data (Read)
   JavaScript
    function displayData() {
    tableBody.innerHTML = ""; // Kosongkan tabel dulu
    let list = JSON.parse(localStorage.getItem("mhsList")) || [];
    list.forEach((mhs) => {
        // Buat baris (tr) baru dan masukkan data mahasiswa ke kolom (td)
        // Menambahkan tombol edit (✎) dan hapus (🗑) di kolom aksi
      });
  }
  Fungsi ini melakukan looping pada array mhsList dan merender ulang seluruh isi tabel setiap ada perubahan data.

E. Fungsi Hapus (Delete)
   JavaScript
    function deleteData(nim) {
    if (confirm("...")) { // Konfirmasi keamanan
        let list = list.filter(item => item.nim !== nim); // Buang data yang NIM-nya dipilih
        localStorage.setItem("mhsList", JSON.stringify(list));
        displayData();
     }
  }
F. Fungsi Edit
   JavaScript
   function editData(nim) {
    // Cari data di array berdasarkan NIM
    // Jika ketemu, pindahkan nilai-nilai tersebut kembali ke kotak input form
    window.scrollTo(0,0); // Geser layar ke atas agar user langsung lihat formnya
  }
G. Fungsi Pencarian (Search)
   JavaScript
   function searchTable() {
      let filter = input.value.toLowerCase();
      // Loop seluruh baris tabel
      // Jika teks di kolom NIM atau Nama mengandung kata kunci (filter), tampilkan.
      // Jika tidak ada, sembunyikan baris tersebut (display: none).
 }
