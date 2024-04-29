# Protecting Your REST API

## Stateful VS Stateless

- **Stateful** adalah tipe authentication process yang menyimpan data user dan keep track data user yang sedang login di server. **E.g. : Session**


- **Stateless** adalah tipe authentication prosess yang setiap request client ke server harus mencantumkan informasi2 yang dibutuhkan untuk menverifikasi user tersebut, sehingga maksudnya adalah client yang bertanggung jawab untuk menyimpan semua informasi user yang sedang login dan kirim ke server (server tidak menyimpan infonya)**E.g. : JWT**

## Authentication VS Authorization
- **Authentication** adalah proses identifikasi user siapa yang sedang login

- **Authorization** is proses perlindungan dengan cara membatasi hak user tertentu yang sedang login, contohnya pembatasan user biasa sehingga tidak bisa melakukan delete, namun user admin bisa melakukan delete

## Register Process
- Proses register hanyalah membuat user baru, tetapi ada hal yang perlu diperhatikan yaitu password, password user baru harus kita lindungi agar tidak mudah di hack. Kita menggunakan bantuan package yaitu **bcryptjs**(https://www.npmjs.com/package/bcryptjs)
- Bcryptjs digunakan pada saat pembuatan user baru, alias sebelum data user baru masuk ke database, jadi kita bisa memanfaatkan hooks sequelize yaitu **beforeCreate** dan melakukan hash password
- Sama halnya seperti membuat user baru, proses seeding juga perlu melakukan hash terhadap password user yang akan di seeding

## Login Process
- Proses login diawali dengan menerima email/username dan password yang diberi oleh user
- Karena login tidak membuat data baru, jadi sequelize validation tidak ketrigger, sehingga kita wajib membuat validasi manual untuk mengechek apakah data email & password yg dimasukkan valid atau tidak
- Setelah data valid, kita mencari user di database bedasarkan email yang di input, lakukan validasi manual juga untuk mengecek apakah ada usernya atau tidak
- Setelah itu kita mencocokan (compare) password yang diinput user dan yang ada didatabase(sudah terencrypt) menggunakan function **bcryptjs** compareSync , jika salah kita juga bikin validasi manual
- lalu, kita harus menyimpan hal-hal yang penting agar nanti bisa di identifikasi siapa user yang sedang login. **jsonwebtoken**(https://www.npmjs.com/package/jsonwebtoken) disini tugasnya untuk menggantikan session (soalnya session dianggap kurang aman, dan di refresh jg langsung hilang)
- jadi pada saat login , sekarang kita bisa membuat payload (data-data yang akan disimpan) yang berisi contohnya id yang lagi login, rolenya, dan username/email 
- Tidak seperti session , data2 yang akan disimpen itu ibaratnya di encode dulu (supaya lebih aman) dan dijadikan acesss token
- Karena kita sekarang udah gak server side rendering, udah jadi REST API, kita kirim access tokennya di res.statusnya

## DOTENV
[Dokumentasi DOTENV](https://www.npmjs.com/package/dotenv)

Dikarenakan pada saat kita menggunakan jwt, mereka membutuhkan **secret key** yang merupakan variabel buatan kita sendiri yang ditujukan hanya kita yang mengetahui variabel tersebut. Maka dari itu kita menggunakan **DOTENV**