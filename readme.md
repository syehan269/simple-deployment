# Daftar isi
- [Daftar isi](#daftar-isi)
- [Setup Git Repository](#setup-git-repository)
- [Setup Folder Project](#setup-folder-project)
  - [Caching Assets Project](#caching-assets-project)
- [Setup Server](#setup-server)
  - [Setup Apache](#setup-apache)
  - [Setup Nginx](#setup-nginx)

# Setup Git Repository

* langkah pertama melakukan inisialisasi git pada folder yang digunakan dengan menggunakan command berikut:

  `git init`

* lalu, anda dapat membuat repository melalui github, gitlab, bitbucket, dll.

* setelah itu, anda dapat menambahkan url repository yang telah dibuat dengan menggunakan command berikut:

  `git remote add [remote-name] [repository-url]`

* jika sudah selesai anda dapat melakukan staging seluruh file yang akan dikirim ke repository dengan command:

  `git add .`

* kemudian anda dapat membuat commit atau perubahan yang dilakukan dengan command berikut:

  `git commit -m "[masukkan keterangan commit]"`

* lalu, untuk mengirim commit yang dibuat anda dapat menggunakan command berikut. untuk default branch yang digunakan akan sesuai dengan konfigurasi git di OS anda, tapi nama yang biasa digunakan seperti: main atau master.
  
  `git push [remote-name] [branch-name]`

* untuk melakukan update dari repository atau pull dapat menggunakan command berikut:

  `git pull [remote-name] [branch-name]`

untuk lebih penggunaan command lebih lanjut, anda dapat melihat cheatsheet berikut: [Git Command Cheatsheet](https://education.github.com/git-cheat-sheet-education.pdf)

# Setup Folder Project

* yang pertama anda perlu melakukan clonning dari repository yang telah dibuat dengan command berikut, lalu masuk ke folder projectnya.
  
  `git clone [repository-url]`

* lalu anda perlu menduplikat file konfigurasi, secara default laravel akan menamainya .env.example.

  `cp .env.example .env`

* setelah itu, anda dapat melakukan instalasi dependancy project dengan command berikut:

  `composer install --no-dev`

  untuk melakukan test apakah dependancy dapat dilakukan tanpa error anda dapat menambahkan flag `--dry-run`.

  contoh:

  `composer install --no-dev --dry-run`

* untuk versi laravel 9+ anda dapat melewati langkah ini, tapi untuk versi sebelumnya anda perlu menjalankan command berikut untuk membuat special key di file .env.

  `php artisan key:generate`

* terakhir, anda perlu melakukan konfigurasi file log yang ada di folder /public/logs/ untuk memiliki akses write, gunakan command dibawah ini untuk merubah hak aksesnya.
  `sudo chmod -R o+wx`

untuk melihat daftar flag yang tersedia untuk `install` anda dapat melihat pada dokumentasi composer: [Composer CLI Documentation](https://getcomposer.org/doc/03-cli.md#install-i)

untuk panduan tentang command untuk mengatur hak akses pada linux, anda dapat melihat artikel berikut: [File Permission in Linux](https://www.guru99.com/file-permissions.html)

## Caching Assets Project

setelah dependancy sudah terinstall, anda dapat melakukan caching view, route, dan konfigurasi yang ada di file .env. command yang digunakan untuk melakukan caching yaitu:

`php artisan view:cache`

`php artisan route:cache`

`php artisan config:cache`

dan untuk membersihkan cache yang telah dibuat anda dapat menjalankan sesuai jenis komponennya:

`php artisan view:clear`

`php artisan route:clear`

`php artisan config:clear`

lalu, untuk informasi mengenai deployment di laravel anda juga dapat melihat pada dokumentasinya: [Deployment - laravel Documentation](https://laravel.com/docs/master/deployment)

# Setup Server

## Setup Apache

* Masuk ke directory dari apache untuk melakukan konfigurasi.
  * Debian based distros: `/etc/apache2/sites-available`

* Untuk konfigurasi awal dapat langsung menggunakan konfigurasi default yang ada pada file 000-default.conf.
  
  contoh:

  `cp 000-default.conf test-web.conf`

* Jika sudah melakukan duplikat maka anda perlu melakukan menyesuaikan beberapa konfigurasinya, yaitu bagian:
  * ServerName: isi kolom ini sesuai dengan domain yang telah didapatkan
  * DocumentRoot: isi kolom ini sesuai lokasi dari project yang ada pada server, **perlu diingat, pada Laravel lokasi index.php ada di folder public**.

* Lalu, setelah disesuaikan anda dapat menjalankan command berikut untuk melakukan test konfigurasinya.
  
  `apachectl configtest`

* Dan terakhir setelah berhasil menjalankan test anda dapat melakukan restart service apache.
  * Debian based distro: `sudo service apache2 restart`

## Setup Nginx

to be added later...