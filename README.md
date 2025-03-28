### Reflection Publisher-1
1. Observer design pattern bekerja dengan melibatkan subjek dan observer. subscriber sendiri didefinisikan sebagai interface.
single Model struct cukup jika subscriber menunjukan perliaku notifikasi yang sama. akan tetapi, jika 

2. DashMap diperlukan karena kita menggunakan concurrency dimana banyak thread yang mengakses data subscriber secara bersamaan.
Dalam multithreaded, penggunaan Vec perlu dibungkus dalam Mutex. Selain itu, karena progrum mencari subscriber perdasarkan url maka DashMap (key-value) lebih efisien dibanding Vec yang harus mengiterasi sebanyak O(N). 
Hal demikian juga berlaku pada insert (add), delete, dan collect (read) yang hanya perlu O(1) jika menggunakan DashMap sedangkan jika menggunakan Vec perlu O(N)
