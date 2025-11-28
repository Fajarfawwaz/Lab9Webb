---

# Praktikum 9: PHP Modular

---

**Mata Kuliah:** Pemrograman Web1

**Dosen Pengampu:** Agung Nugroho, S.Kom., M.Kom.

**Nama:** Fajar Fawwaz Atallah

**NIM:** 312410357

**Kelas:** TI.2A.A.4

---

# Lab9Web – Praktikum 9: Modularisasi PHP

---

##  Struktur Folder Project

```
Lab9Web/
│
├── index.php
├── config.php
│
├── templates/
│   ├── header.php
│   ├── footer.php
│   └── style.css
│
└── user/
    ├── list.php
    ├── add.php
    ├── edit.php
    └── delete.php
```

---

#  Kumpulan Codingan (Source Code)

## **index.php**

```php
<?php
require_once 'config.php';
require_once 'templates/header.php';

$page = isset($_GET['page']) ? $_GET['page'] : 'home';
$path = $page . '.php';

if (file_exists($path)) {
    include $path;
} else {
    echo '<h2>404 - Halaman Tidak Ditemukan</h2>';
}

require_once 'templates/footer.php';
?>
```

## **config.php**

```php
<?php
$host='localhost';
$user='root';
$pass='';
$db='latihan1';

$conn=mysqli_connect($host,$user,$pass,$db);
if(!$conn){ die('Koneksi gagal: '.mysqli_connect_error()); }
?>
```

## **templates/header.php**

```php
<!DOCTYPE html>
<html>
<head>
<meta charset='UTF-8'>
<title>Modular PHP</title>
<link rel='stylesheet' href='templates/style.css'>
</head>
<body>
<div class='container'>
<header><h1>Modularisasi PHP</h1></header>
<nav>
<a href='index.php?page=home'>Home</a>
<a href='index.php?page=user/list'>User</a>
<a href='index.php?page=about'>About</a>
</nav>
```

## **templates/footer.php**

```php
<footer><p>&copy; 2025 - Universitas Pelita Bangsa</p></footer>
</div>
</body>
</html>
```

## **user/list.php**

```php
<?php
$q=mysqli_query($conn,'SELECT * FROM user');
?>
<h2>Data User</h2>
<a href='index.php?page=user/add'>Tambah User</a><br><br>
<table border='1' cellpadding='5'>
<tr><th>ID</th><th>Nama</th><th>Email</th><th>Aksi</th></tr>
<?php while($r=mysqli_fetch_assoc($q)): ?>
<tr>
<td><?= $r['id'] ?></td>
<td><?= $r['nama'] ?></td>
<td><?= $r['email'] ?></td>
<td>
<a href='index.php?page=user/edit&id=<?= $r['id'] ?>'>Edit</a> |
<a onclick="return confirm('Hapus?')" href='index.php?page=user/delete&id=<?= $r['id'] ?>'>Hapus</a>
</td>
</tr>
<?php endwhile; ?>
</table>
```

## **user/add.php**

```php
<h2>Tambah User</h2>
<form method='post'>
<input name='nama' placeholder='Nama' required><br><br>
<input name='email' placeholder='Email' required><br><br>
<button name='submit'>Simpan</button>
</form>
<?php
if(isset($_POST['submit'])){
$n=$_POST['nama']; $e=$_POST['email'];
mysqli_query($conn,"INSERT INTO user(nama,email) VALUES('$n','$e')");
echo "<script>alert('Tersimpan');location='index.php?page=user/list';</script>";
}
?>
```

## **user/edit.php**

```php
<?php
$id=$_GET['id'];
$q=mysqli_query($conn,"SELECT * FROM user WHERE id=$id");
$d=mysqli_fetch_assoc($q);
?>
<h2>Edit User</h2>
<form method='post'>
<input name='nama' value='<?= $d['nama'] ?>' required><br><br>
<input name='email' value='<?= $d['email'] ?>' required><br><br>
<button name='submit'>Update</button>
</form>
<?php
if(isset($_POST['submit'])){
$n=$_POST['nama'];$e=$_POST['email'];
mysqli_query($conn,"UPDATE user SET nama='$n',email='$e' WHERE id=$id");
echo "<script>alert('Updated');location='index.php?page=user/list';</script>";
}
?>
```

## **user/delete.php**

```php
<?php
$id=$_GET['id'];
mysqli_query($conn,"DELETE FROM user WHERE id=$id");
echo "<script>alert('Dihapus');location='index.php?page=user/list';</script>";
?>
```

---

# Hasil Tampilan Di Browser:

* Halaman Home
  
  <img width="598" height="282" alt="image" src="https://github.com/user-attachments/assets/6afa9f7c-cd8a-4d05-9747-6ce9b4d22037" />

  ---
* Halaman User List
  
  <img width="655" height="323" alt="image" src="https://github.com/user-attachments/assets/fd9b8085-1319-4f51-acbd-cfc8ed6cd8a0" />

  ---
* Halaman Tambah User

  <img width="676" height="348" alt="image" src="https://github.com/user-attachments/assets/74ea1da2-3e90-411f-be14-3007f5592136" />

  ---
* Hasil nya

  <img width="818" height="352" alt="image" src="https://github.com/user-attachments/assets/09a58384-8b62-4dc8-a935-c12e4eed7227" />

  ---
* Halaman Edit User

  <img width="673" height="358" alt="image" src="https://github.com/user-attachments/assets/68f909ed-46d2-400d-8621-05ac337f010d" />
  
  ---
* Halaman About

  <img width="741" height="292" alt="image" src="https://github.com/user-attachments/assets/79124cdd-6b5c-44b9-babb-3751765fbaa0" />

  ---
* Struktur Folder Project

  <img width="286" height="415" alt="image" src="https://github.com/user-attachments/assets/97632b2a-65ef-4143-b5b0-c93bd8c68c19" />

  ---

# Kesimpulan

Dalam Praktikum 9 ini:

* Konsep **modularisasi** berhasil diterapkan menggunakan `require()` untuk header dan footer.
* **Routing sederhana** berhasil dibuat menggunakan parameter `page` pada URL.
* Fitur **CRUD user** berjalan dengan baik menggunakan struktur folder yang lebih rapi.
* Project final **berhasil sesuai instruksi modul** dan siap dikumpulkan.
