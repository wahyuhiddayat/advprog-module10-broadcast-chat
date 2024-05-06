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
