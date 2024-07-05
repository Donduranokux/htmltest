<?php
// MySQL bağlantı bilgileri
$servername = "localhost"; // Sunucu adı
$username = "kullanici_adi"; // MySQL kullanıcı adı
$password = "sifre"; // MySQL şifre
$dbname = "veritabani_adi"; // Kullanmak istediğiniz veritabanı adı

// MySQL bağlantısı oluştur
$conn = new mysqli($servername, $username, $password, $dbname);

// Bağlantıyı kontrol et
if ($conn->connect_error) {
    die("Bağlantı hatası: " . $conn->connect_error);
}

// Formdan gelen verileri al
$name = $_POST['name'];
$email = $_POST['email'];
$password = $_POST['password'];
$hashed_password = password_hash($password, PASSWORD_DEFAULT); // Şifreyi güvenli bir şekilde hash'leme

// SQL sorgusu oluştur
$sql = "INSERT INTO users (name, email, password) VALUES ('$name', '$email', '$hashed_password')";

// Sorguyu çalıştır ve sonucu kontrol et
if ($conn->query($sql) === TRUE) {
    echo "Kayıt başarıyla eklendi.";
} else {
    echo "Hata: " . $sql . "<br>" . $conn->error;
}

// Bağlantıyı kapat
$conn->close();
