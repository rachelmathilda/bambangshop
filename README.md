### Reflection Publisher-1
1. Observer design pattern bekerja dengan melibatkan subjek dan observer. Subscriber sendiri didefinisikan sebagai interface.
Meskipun struct model tunggal mungkin tampak cukup untuk sistem yang sederhana dan tidak berubah, menggunakan antarmuka (trait) bisa jadi opsi lain yang lebih mematuhi prinsip pola observer. 

2. DashMap diperlukan karena kita menggunakan concurrency dimana banyak thread yang mengakses data subscriber secara bersamaan.
Dalam multithreaded, penggunaan Vec perlu dibungkus dalam Mutex. Selain itu, karena progrum mencari subscriber perdasarkan url maka DashMap (key-value) lebih efisien dibanding Vec yang harus mengiterasi sebanyak O(N). 
Hal demikian juga berlaku pada insert (add), delete, dan collect (read) yang hanya perlu O(1) jika menggunakan DashMap sedangkan jika menggunakan Vec perlu O(N). 

3. DashMap sendiri merupakan struktur data yang merupakan alternatif dari HashMap yang dapat digunakan untuk concurrency tanpa Mutex atau RwLock secara eksplisit. Singleton sendiri merupakan pola desain yang memastikan hanya ada satu instance dari suatu objek dalam aplikasi dan bisa diakses global.
project ini menggunakan multi-threaded, dengan itu Singleton saja tidak cukup karena perlu memanfaatkan kelebihan DashMap dalam mengaplikasikan fitur concurrency (melayani banyak request secara bersamaan).


### Reflection Publisher-2
1. Dalam konsep MVC, model memang bisa mencakup penyimpanan dan logika bisnis namun project yang besar dan kompleks menggabungkan service dan repository tidak maintanable. 
Design principle adalah salah satu faktor yang bisa dipakai untuk menentukan apakah aplikasi maintanable. Jika ditinjau dari design principle terdapat beberapa prinsip yang dilanggar jika menggabungkan service dan repository ke model. 
Prinsip pertama adalah single responsibility principle, setiap kelas atau modul hanya memiliki satu fungsi saja. Selanjutnya dependency inversion principle ketergantungan harus mengarah ke abstraksi bukan implementasi concrete, penggabungan membuat service bergantung pada repository. 
Oleh karena itu perlu ada pemisahan service dan repository dari model agar aplikasi maintanable. 

2. Kode akan sulit untuk diganti/diperluas, sulit dibaca, skalabilitas terbatas, dan rumit untuk diuji. Interaksi antara model program, subscriber, dan notification yang terjadi adalah subscriber berperan sebagai model utama dan notification sebagai model pendukung. 
Karena tidak ada abstraksi dan pemisahan maka setiap operasi bergantung pada implementasi konkret di Subscriber. 

3. Postman digunakan khususnya untuk menguji endpoint api. Tetapi selain itu dapat juga untuk otomatisasi pengujian serta debugging dan validasi. 


### Reflection Publisher-3
1. Tutorial ini menggunakan observer pattern push model karena NotificationService mengirimkan objek notification langsung ke Subscriber melalui metode update. Selain itu Subscriber tidak perlu meminta informasi tambahan dari NotificationService. 

2. Kelebihan => observer bekerja dengan efisien tanpa melakukan proses tambahan (meminta data), Notification dimplementasi dengan sederhana yaitu hanya perlu mengirimkan payload
Kekurangan => observer gabisa milih data yang mereka terima (kurang fleksibel), bisa terjadi overhead jika payload kompleks. 

3. Notifikasi akan dikirim satu per satu secara berurutan dimana hal ini dapat memperlambat jaringan dan latensi tinggi.