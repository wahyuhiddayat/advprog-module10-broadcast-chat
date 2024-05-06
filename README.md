# Tutorial 10 
Wahyu Hidayat - 2206081894 - Advanced Programming B

***Experiment 2.1: Original code, and how it run***

<img width="1158" alt="Screenshot 2024-05-06 at 4 56 08 PM" src="https://github.com/wahyuhiddayat/advprog-module10-broadcast-chat/assets/119432989/c0960f33-cbd7-4c39-8f40-c7bbd1b38cde">

Untuk menjalankan server dan tiga client:
1. Buka empat terminal terpisah.
2. Terminal pertama akan digunakan untuk menjalankan server menggunakan perintah:
   ```bash
   cargo run --bin server
   ```
   Server akan mendengarkan koneksi pada port `2000` dan akan menampilkan log saat client terhubung.

3. Terminal kedua hingga keempat akan digunakan untuk menjalankan client dengan menjalankan perintah berikut di masing-masing terminal:
   ```bash
   cargo run --bin client
   ```

3. Setiap client akan terhubung ke server dan menerima pesan sambutan: "Welcome to chat! Type a message."

4. Saat mengetik pesan di masing-masing client, pesan tersebut akan dikirim ke server dan diteruskan ke semua client yang terhubung. Contohnya:
   - Ketik "Client 1 from wahyu's computer" di client 1.
   - Ketik "Client 2 from wahyu's computer" di client 2.
   - Ketik "Client 3 from wahyu's computer" di client 3.

   Hasilnya adalah setiap client akan menerima pesan dari semua client lainnya.

5. Penjelasan:

   Server menggunakan `broadcast channel` untuk menyiarkan pesan dari satu client ke semua client lainnya. Setiap pesan yang dikirim oleh satu client diterima oleh server dan kemudian disiarkan ke semua client yang terhubung, termasuk pengirimnya sendiri. Oleh karena itu, setiap client melihat pesan mereka sendiri dan pesan dari client lain dalam urutan kedatangan mereka.

***Experiment 2.2: Modifying port***

Port client dan server sama
<img width="1160" alt="Screenshot 2024-05-06 at 5 21 05 PM" src="https://github.com/wahyuhiddayat/advprog-module10-broadcast-chat/assets/119432989/0fe7443c-b1e3-4e05-9c04-37f827921bc1">

Port client dan server berbeda
<img width="1156" alt="Screenshot 2024-05-06 at 5 24 30 PM" src="https://github.com/wahyuhiddayat/advprog-module10-broadcast-chat/assets/119432989/1a4cd94d-fb41-48ab-81e9-85aee9cfb89c">

Jika port antara server dan client sama, program akan berjalan tanpa error. Namun, jika port antara server dan client berbeda, misalnya port 8080 untuk server dan port 2000 untuk client, maka akan muncul error "Connection refused". Ini menunjukkan bahwa client mencoba terhubung ke port yang tidak ada server yang mendengarkan.

Dalam kasus ini, client mencoba menghubungi port 2000, tetapi server mendengarkan di port 8080. Agar client dan server dapat berkomunikasi, port yang digunakan harus sama. Misalnya, jika server mendengarkan di port 8080, client juga harus terhubung ke port yang sama.

***Experiment 2.3: Small changes, add IP and Port***

<img width="1156" alt="Screenshot 2024-05-06 at 6 27 23 PM" src="https://github.com/wahyuhiddayat/advprog-module10-broadcast-chat/assets/119432989/19f44572-b2c4-42ee-bb7c-5c2da61d2667">

Saya melakukan beberapa modifikasi pada server.rs dan client.rs. 

Pada `server.rs` saya memodifikasinya menjadi:
```rust
println!("New connection from Wahyu's Computer{addr:?}");
```

dan
```rust
bcast_tx.send(format!("{addr}: {text}"))?;
```

Pada `client.rs` saya memodifikasinya menjadi:
```rust
if let Some(text) = msg.as_text() {
    println!("Wahyu's Computer - From server: {}", text);
}
```
