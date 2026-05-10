1. Bagian Head dan Styling (CSS)
Bagian ini berfungsi mengatur tampilan halaman agar lebih rapi dan nyaman digunakan.
<style>
body{
   font-family: Arial, sans-serif;
   margin:20px;
   background:#f5f5f5;
}

form{
   background:#fff;
   padding:20px;
   border-radius:10px;
   box-shadow:0 2px 5px rgba(0,0,0,0.1);
}
</style>
Perubahan:
•	Tampilan form lebih modern.
•	Ada bayangan (box-shadow).
•	Sudut form melengkung (border-radius).
•	Warna background lebih nyaman dilihat.
Bug:
Tidak ada bug pada bagian ini, hanya peningkatan desain.

2. Struktur Form HTML
<form id="formMahasiswa">

<input type="text" id="nim" required>
<input type="text" id="nama" required>

<textarea id="alamat"></textarea>

<input type="radio" name="jk" value="Pria">
<input type="radio" name="jk" value="Wanita">

<select id="tanggal"></select>
<select id="bulan"></select>
<select id="tahun"></select>

<input type="password" id="password">

</form>
Perubahan:
•	Input lebih lengkap dan tersusun rapi.
•	Password menggunakan tipe password.
•	Alamat memakai textarea.
Bug:
Pada kode lama, jika required tidak dipakai maka NIM dan Nama bisa kosong.

3. Dropdown Tahun
for(let i = 1990; i <= 2026; i++){

document.getElementById("tahun").innerHTML += `
<option value="${i}">${i}</option>
`;

}
Perubahan:
•	Tahun diisi otomatis.
•	Lebih cepat dibanding menulis manual satu per satu.
Bug:
Tidak ada bug, hanya efisiensi penulisan.

4. Fungsi updateTanggal()
function updateTanggal(){

const bulan = document.getElementById("bulan").value;
const tahun = document.getElementById("tahun").value;

const jumlahHari = new Date(tahun, bulan, 0).getDate();

}
Perubahan:
•	Dropdown tanggal sekarang menyesuaikan bulan dan tahun.
•	Tahun kabisat juga otomatis dihitung.
Bug Sebelumnya:
•	Februari tetap 31 hari.
•	April bisa pilih tanggal 31.
•	Data tanggal tidak valid.

5. Event Submit Form
form.addEventListener("submit", function(e){

e.preventDefault();

saveToLocalStorage(dataMahasiswa);

displayData();

});
Perubahan:
•	Setelah submit data langsung tampil otomatis.
•	Form langsung reset.
Bug Sebelumnya:
Jika e.preventDefault() tidak digunakan:
•	Halaman refresh otomatis.
•	Input terhapus.
•	Data bisa hilang.

6. Fungsi saveToLocalStorage()
function saveToLocalStorage(obj){

let list = JSON.parse(localStorage.getItem("mhsList")) || [];

list.push(obj);

localStorage.setItem("mhsList", JSON.stringify(list));

}
Perubahan:
•	Data sekarang tersimpan permanen di browser.
•	Saat refresh data tetap ada.
Bug Sebelumnya:
•	Data hanya tampil di tabel.
•	Setelah refresh semua hilang.

7. Fungsi displayData()
function displayData(){

tableBody.innerHTML = "";

list.forEach((mhs)=>{

row.innerHTML = `
<td>${mhs.nim}</td>
<td>${mhs.nama}</td>
<td>${"*".repeat(mhs.password.length)}</td>
`;

});

}
Perubahan:
•	Tabel otomatis membaca data dari LocalStorage.
•	Password disamarkan menjadi bintang.
Bug Sebelumnya:
•	Password tampil asli.
•	Tabel tidak otomatis load data lama.

8. Fungsi deleteData()
function deleteData(nim){

list = list.filter(item => item.nim !== nim);

}
Perubahan:
•	Hapus data permanen dari LocalStorage.
•	Ada konfirmasi sebelum hapus.
Bug Sebelumnya:
Kode lama hanya:
row.remove();
Akibatnya:
•	Hanya hilang dari tabel.
•	Saat refresh bisa muncul lagi.

9. Fungsi editData()
function editData(nim){

document.getElementById("nim").value = mhs.nim;
document.getElementById("nama").value = mhs.nama;

}
Perubahan:
•	Semua data dikembalikan ke form.
•	User bisa edit tanpa input ulang.
Bug Sebelumnya:
•	Jenis kelamin tidak ikut kembali.
•	Tanggal lahir tidak masuk.
•	Password kosong saat edit.

10. Fungsi clearForm()
function clearForm(){

form.reset();
updateTanggal();

}
Perubahan:
•	Setelah reset, dropdown tanggal ikut normal kembali.
Bug Sebelumnya:
•	Form kosong, tetapi tanggal tidak ter-reset dengan benar.

11. Fungsi searchTable()
function searchTable(){

let filter = input.value.toLowerCase();

}
Perubahan:
•	Bisa mencari data berdasarkan NIM atau Nama.
•	Mempermudah mencari data banyak.
Bug:
Tidak ada bug sebelumnya karena fitur ini memang belum ada.

12. Kesimpulan
Bug Lama:
•	Data hilang saat refresh
•	Password terlihat
•	Edit tidak lengkap
•	Tanggal tidak valid
•	Reset tidak sempurna
Perubahan Baru:
•	Tambah LocalStorage
•	Tambah Search
•	Tampilan lebih bagus
•	Tombol modern
•	Password jadi bintang
•	Dropdown tanggal otomatis




Example


# Perbandingan Tampilan

## Sebelum Perbaikan

![Before](https://raw.githubusercontent.com/xolveyndaa-blip/Form-Mahasiswa_Pemograman-Web/main/images/before.png)

## Setelah Perbaikan

![After](https://raw.githubusercontent.com/xolveyndaa-blip/Form-Mahasiswa_Pemograman-Web/main/images/Screenshot%202026-05-10%20115945.png)
