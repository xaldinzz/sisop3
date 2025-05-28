[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/Eu-CByJh)
|    NRP     |      Name      |
| :--------: | :------------: |
| 5025241181 | Muhammad Naufal Hadaya Setiawan |
| 5025241184 | Naufaldi Faqih Abimanyu |
| 5025221000 | Student 3 Name |

# Praktikum Modul 3 _(Module 3 Lab Work)_

### Laporan Resmi Praktikum Modul 3 _(Module 3 Lab Work Report)_

Di suatu pagi hari yang cerah, Budiman salah satu mahasiswa Informatika ditugaskan oleh dosennya untuk membuat suatu sistem operasi sederhana. Akan tetapi karena Budiman memiliki keterbatasan, Ia meminta tolong kepadamu untuk membantunya dalam mengerjakan tugasnya. Bantulah Budiman untuk membuat sistem operasi sederhana!

_One sunny morning, Budiman, an Informatics student, was assigned by his lecturer to create a simple operating system. However, due to Budiman's limitations, he asks for your help to assist him in completing his assignment. Help Budiman create a simple operating system!_

### Soal 1

> Sebelum membuat sistem operasi, Budiman diberitahu dosennya bahwa Ia harus melakukan beberapa tahap terlebih dahulu. Tahap-tahapan yang dimaksud adalah untuk **mempersiapkan seluruh prasyarat** dan **melakukan instalasi-instalasi** sebelum membuat sistem operasi. Lakukan seluruh tahapan prasyarat hingga [perintah ini](https://github.com/arsitektur-jaringan-komputer/Modul-Sisop/blob/master/Modul3/README-ID.md#:~:text=sudo%20apt%20install%20%2Dy%20busybox%2Dstatic) pada modul!

> _Before creating the OS, Budiman was informed by his lecturer that he must complete several steps first. The steps include **preparing all prerequisites** and **installing** before creating the OS. Complete all the prerequisite steps up to [this command](https://github.com/arsitektur-jaringan-komputer/Modul-Sisop/blob/master/Modul3/README-ID.md#:~:text=sudo%20apt%20install%20%2Dy%20busybox%2Dstatic) in the module!_

**Answer:**

- **Code:**

  1.
  ```
  sudo apt -y update
  sudo apt -y install qemu-system build-essential bison flex libelf-dev libssl-dev bc grub-common grub-pc libncurses-dev libssl-dev mtools grub-pc-bin xorriso tmux
  ```
  2.
  ```
  mkdir -p osboot
  cd osboot
  ```
  3.
  ```
  wget https://cdn.kernel.org/pub/linux/kernel/v6.x/linux-6.1.1.tar.xz
  tar -xvf linux-6.1.1.tar.xz
  cd linux-6.1.1
  ```
  4.
  ```
  make tinyconfig
  make menuconfig
  ```
  5.
  ```
  make -j$(nproc)
  ```
  6.
  ```
  cp arch/x86/boot/bzImage ..
  ```

- **Explanation:**

  1.`Kode pertama untuk mengupdate versi sistem kita lalu kita juga menginstall bebrapa software pendukung seperti qemu,build-essential,flex,bison, dan lainnya`
  2.`Di Sini kita membuat direktori bernama osboot yang akan digunakan untuk menyimpan semua hal tentang mini OS yang akan kita buat`
  3.`Disini kita akan mengunduh sumber kode linux, dan setelah terunduh akan diekstrak ke dalam direktori linux-6.1.1`
  4.`Kernel Linux perlu dikonfigurasi sebelum dikompilasi. Kita akan memulai dengan menggunakan konfigurasi minimal menggunakan make tinyconfig. Setelah itu, kita bisa menyesuaikan konfigurasi lebih lanjut dengan menggunakan make menuconfig untuk mengaktifkan fitur-fitur yang diperlukan oleh sistem operasi yang akan kita buat. Beberapa pengaturan yang penting untuk diaktifkan adalah dukungan untuk virtualisasi, file systems, driver perangkat, serta jaringan. Nah untuk penyesuainnya terdapat di modul sisop bab 3`
  5.`Setelah selesai mengkonfigurasi, Hal selanjutnya yaitu mengkompile source code linux tadi`
  6.`Setelah kompilasi selesai, kita akan mendapatkan file bzImage di dalam direktori arch/x86/boot/. Pindahkan file ini ke direktori osboot untuk persiapan langkah selanjutnya, yaitu pembuatan root filesystem dan emulasi menggunakan QEMU.`

- **Screenshot:**

![imagealt](https://github.com/xaldinzz/sisop3/blob/main/Screenshot%20from%202025-05-28%2021-08-06-2.png?raw=true)

### Soal 2

> Setelah seluruh prasyarat siap, Budiman siap untuk membuat sistem operasinya. Dosen meminta untuk sistem operasi Budiman harus memiliki directory **bin, dev, proc, sys, tmp,** dan **sisop**. Lagi-lagi Budiman meminta bantuanmu. Bantulah Ia dalam membuat directory tersebut!

> _Once all prerequisites are ready, Budiman is ready to create his OS. The lecturer asks that the OS should contain the directories **bin, dev, proc, sys, tmp,** and **sisop**. Help Budiman create these directories!_

**Answer:**

- **Code:**

  ```mkdir -p myramdisk/{bin,dev,proc,tmp,sys,sisop}```

- **Explanation:**

  `Kita disini membuat direktori yang diminta dan dimasukkan dalam direktori myramdisk`

- **Screenshot:**

  `put your answer here`

### Soal 3

> Budiman lupa, Ia harus membuat sistem operasi ini dengan sistem **Multi User** sesuai permintaan Dosennya. Ia meminta kembali kepadamu untuk membantunya membuat beberapa user beserta directory tiap usernya dibawah directory `home`. Buat pula password tiap user-usernya dan aplikasikan dalam sistem operasi tersebut!

> _Budiman forgot that he needs to create a **Multi User** system as requested by the lecturer. He asks your help again to create several users and their corresponding home directories under the `home` directory. Also set each user's password and apply them in the OS!_

**Format:** `user:pass`

```
root:Iniroot
Budiman:PassBudi
guest:guest
praktikan1:praktikan1
praktikan2:praktikan2
```

**Answer:**

- **Code:**
  1.`mkdir -p myramdisk/{home/root,Budiman,guest,praktikan1,praktikan2}`
  2.
  ```
  openssl passwd -1 Iniroot
  openssl passwd -1 PassBudi
  openssl passwd -1 guest
  openssl passwd -1 praktikan1
  openssl passwd -1 praktikan2
  ```
  3.
  ```
  mkdir -p myramdisk/etc/
  nano myramdisk/etc/passwd
  ```
  4.
  ```
  root:<<hasilgeneratorrootpassword>>:0:0:root:/root:/bin/sh
  Budiman:<<hasilgeneratorrootpassword>>:1001:100:Budimam:/home/Budiman:/bin/sh
  guest:<<hasilgeneratorrootpassword>>:1002:100:guest:/home/guest:/bin/sh
  praktikan1:<<hasilgeneratorrootpassword>>:1003:100:praktikan1:/home/praktikan1:/bin/sh
  praktikan2:<<hasilgeneratorrootpassword>>:1004:100:praktikan2:/home/praktikan2:/bin/sh
  ```

- **Explanation:**

  1.
  `Kode pertama untuk membuat direktori home yang di dalamnya berisi direktori user user yang akan dibuat`
2.`Lalu kita akan membuat hash untuk password tiap udernya`
3.`Disini kita akan membuat direktori etc dan membuat file passwd untuk menyimpan info user beserta passwordnya`
4.`Kita memasukkan hash yang telah didapat pada langkah 2 kedalam file passwd dengan template seperti langkah 4`

- **Screenshot:**

  `put your answer here`

### Soal 4

> Dosen meminta Budiman membuat sistem operasi ini memilki **superuser** layaknya sistem operasi pada umumnya. User root yang sudah kamu buat sebelumnya akan digunakan sebagai superuser dalam sistem operasi milik Budiman. Superuser yang dimaksud adalah user dengan otoritas penuh yang dapat mengakses seluruhnya. Akan tetapi user lain tidak boleh memiliki otoritas yang sama. Dengan begitu user-user selain root tidak boleh mengakses `./root`. Buatlah sehingga tiap user selain superuser tidak dapat mengakses `./root`!

> _The lecturer requests that the OS must have a **superuser** just like other operating systems. The root user created earlier will serve as the superuser in Budiman's OS. The superuser should have full authority to access everything. However, other users should not have the same authority. Therefore, users other than root should not be able to access `./root`. Implement this so that non-superuser accounts cannot access `./root`!_

**Answer:**

- **Code:**

  `chown 0:0 OS/home/root

chmod 700 OS/home/root
`

- **Explanation:**
Untuk soal nomor 4 ini kita di minta untuk membuat user root menjadi super user maka dari itu kami membuat kode seperti di atas berikut penjelasannya:
Dengan chmod 700, semua akan ditolak kecuali oleh user root.
Ini memastikan bahwa hanya user dengan UID 0 (root) yang bisa masuk ke folder tersebut. User lain akan ditolak.

- **Screenshot:**
- ![image alt](https://github.com/xaldinzz/sisop3/blob/main/Screenshot%20from%202025-05-23%2019-52-48.png?raw=true)

### Soal 5

> Setiap user rencananya akan digunakan oleh satu orang tertentu. **Privasi dan otoritas tiap user** merupakan hal penting. Oleh karena itu, Budiman ingin membuat setiap user hanya bisa mengakses dirinya sendiri dan tidak bisa mengakses user lain. Buatlah sehingga sistem operasi Budiman dalam melakukan hal tersebut!

> _Each user is intended for an individual. **Privacy and authority** for each user are important. Therefore, Budiman wants to ensure that each user can only access their own files and not those of others. Implement this in Budiman's OS!_

**Answer:**

- **Code:**

chown 1001:100 OS/home/Budiman
chmod 700 OS/home/Budiman


- **Explanation:**
- Untuk nomor 5,, kami harus membuat user-user yang di miliki di sistem operasi kami hanya bisa memakses file file yang berada di direktorinya masih masing. Ini penjelasan dari kode berikut:
  1001 → UID milik user Budiman

100 → GID default user group  
berbeda dengan root tdi yang mengharuskan kita untuk membuat root super user di nomor 5 ini budiman hanya di minta untuk membuat user-user(selain root) hanya bisa mengakses filenya sendiri.

- **Screenshot:**

![image alt](https://github.com/xaldinzz/sisop3/blob/main/Screenshot%20from%202025-05-23%2020-21-25.png?raw=true)

```Penjelasan: Difoto ini aku memberi contoh bahwa aku sedang di dalam sistem operasi Budiman Disaat aku memperintah Ls dia menunjukan file di dalamnya tetapi ketika aku melakukan hal yang sama di User guest dia memberi pesan Access Denied.```
### Soal 6

> Dosen Budiman menginginkan sistem operasi yang **stylish**. Budiman memiliki ide untuk membuat sistem operasinya menjadi stylish. Ia meminta kamu untuk menambahkan tampilan sebuah banner yang ditampilkan setelah suatu user login ke dalam sistem operasi Budiman. Banner yang diinginkan Budiman adalah tulisan `"Welcome to OS'25"` dalam bentuk **ASCII Art**. Buatkanlah banner tersebut supaya Budiman senang! (Hint: gunakan text to ASCII Art Generator)

> _Budiman wants a **stylish** operating system. Budiman has an idea to make his OS stylish. He asks you to add a banner that appears after a user logs in. The banner should say `"Welcome to OS'25"` in **ASCII Art**. Use a text to ASCII Art generator to make Budiman happy!_ (Hint: use a text to ASCII Art generator)

**Answer:**

- **Code:**
  ```                         /$$                                                     /$$                                                /$$$$$$  /$$$$$$$ 
                        | $$                                                    | $$                                               /$$__  $$| $$____/ 
 /$$  /$$  /$$  /$$$$$$ | $$  /$$$$$$$  /$$$$$$  /$$$$$$/$$$$   /$$$$$$        /$$$$$$    /$$$$$$         /$$$$$$   /$$$$$$$      |__/  \ $$| $$      
| $$ | $$ | $$ /$$__  $$| $$ /$$_____/ /$$__  $$| $$_  $$_  $$ /$$__  $$      |_  $$_/   /$$__  $$       /$$__  $$ /$$_____/        /$$$$$$/| $$$$$$$ 
| $$ | $$ | $$| $$$$$$$$| $$| $$      | $$  \ $$| $$ \ $$ \ $$| $$$$$$$$        | $$    | $$  \ $$      | $$  \ $$|  $$$$$$        /$$____/ |_____  $$
| $$ | $$ | $$| $$_____/| $$| $$      | $$  | $$| $$ | $$ | $$| $$_____/        | $$ /$$| $$  | $$      | $$  | $$ \____  $$      | $$       /$$  \ $$
|  $$$$$/$$$$/|  $$$$$$$| $$|  $$$$$$$|  $$$$$$/| $$ | $$ | $$|  $$$$$$$        |  $$$$/|  $$$$$$/      |  $$$$$$/ /$$$$$$$/      | $$$$$$$$|  $$$$$$/
 \_____/\___/  \_______/|__/ \_______/ \______/ |__/ |__/ |__/ \_______/         \___/   \______/        \______/ |_______/       |________/ \______/ 
EOF


- **Explanation:**

Disoal No 6 ini Budiman disuruh untuk membuat banner agar memperindah sistem operasi Budiman

- **Screenshot:**

![image alt](https://github.com/xaldinzz/sisop3/blob/main/Screenshot%20from%202025-05-23%2020-55-44.png?raw=true)

### Soal 7

> Melihat perkembangan sistem operasi milik Budiman, Dosen kagum dengan adanya banner yang telah kamu buat sebelumnya. Kemudian Dosen juga menginginkan sistem operasi Budiman untuk dapat menampilkan **kata sambutan** dengan menyebut nama user yang login. Sambutan yang dimaksud berupa kalimat `"Helloo %USER"` dengan `%USER` merupakan nama user yang sedang menggunakan sistem operasi. Kalimat sambutan ini ditampilkan setelah user login dan setelah banner. Budiman kembali lagi meminta bantuanmu dalam menambahkan fitur ini.

> _Seeing the progress of Budiman's OS, the lecturer is impressed with the banner you created. The lecturer also wants the OS to display a **greeting message** that includes the name of the user who logs in. The greeting should say `"Helloo %USER"` where `%USER` is the name of the user currently using the OS. This greeting should be displayed after user login and after the banner. Budiman asks for your help again to add this feature._

**Answer:**

- **Code:**

  `cat /etc/banner
echo "Helloo $USER"
export PS1="\[\e[1;32m\]\u@\h:\w\$ \[\e[0m\]"
`

- **Explanation:**

  `Untuk soal nomor 7 Sitem Operasi Budiman diharuskan untuk menyambut user yang sedang login, Disitu terdapat banner dan juga ucapan Hello user yang sedang login. untuk PS1 adalah prompt seperti terminal asli Linux.`

- **Screenshot:**

![image alt](https://github.com/xaldinzz/sisop3/blob/main/Screenshot%20from%202025-05-23%2021-04-36.png?raw=true)

### Soal 8

> Dosen Budiman sudah tua sekali, sehingga beliau memiliki kesulitan untuk melihat tampilan terminal default. Budiman menginisiatif untuk membuat tampilan sistem operasi menjadi seperti terminal milikmu. Modifikasilah sistem operasi Budiman menjadi menggunakan tampilan terminal kalian.

> _Budiman's lecturer is quite old and has difficulty seeing the default terminal display. Budiman takes the initiative to make the OS look like your terminal. Modify Budiman's OS to use your terminal appearance!_

**Answer:**

- **Code:**

  ```
  echo "[INFO] getty running on ttyS0" > /dev/console
  /bin/getty -L ttyS0 115200 vt100
  sleep 1
done```

- **Explanation:**
Untuk no. 8 Dikarenakan Dosen budiman memiliki kesulitan untuk melihat Budiman di Harus membuat Sistem Operasi Budiman harus menampilkan tampilan terminal ketika menjalankan Sistem Operasi.
`palankan getty di ttyS0, yaitu serial console QEMU (-nographic mode).
getty adalah program yang:
Membuka terminal (tty)
Menampilkan prompt login:
Setelah user isi username, getty akan menjalankan login
-L → jangan coba deteksi modem
ttyS0 → serial terminal aktif di QEMU
`

- **Screenshot:**

![image alt](https://github.com/xaldinzz/sisop3/blob/main/Screenshot%20from%202025-05-23%2021-04-54.png?raw=true)

### Soal 9

> Ketika mencoba sistem operasi buatanmu, Budiman tidak bisa mengubah text file menggunakan text editor. Budiman pun menyadari bahwa dalam sistem operasi yang kamu buat tidak memiliki text editor. Budimanpun menyuruhmu untuk menambahkan **binary** yang telah disiapkan sebelumnya ke dalam sistem operasinya. Buatlah sehingga sistem operasi Budiman memiliki **binary text editor** yang telah disiapkan!

> _When trying your OS, Budiman cannot edit text files using a text editor. He realizes that the OS you created does not have a text editor. Budiman asks you to add the prepared **binary** into his OS. Make sure Budiman's OS has the prepared **text editor binary**!_

**Answer:**

- **Code:**
```
git clone https://github.com/morisab/budiman-text-editor.git
cd budiman-text-editor

g++ main.cpp -o budiman
./budiman
```

- **Explanation:**

  `untuk nomor 9 kami di kasih github untuk mendownload binary text editor, Jadi yang Budiman lakukan adalah melakukan git clone kepada github dan menjalankan eksekusinya`

- **Screenshot:**

  `![image alt](https://github.com/xaldinzz/sisop3/blob/main/Screenshot%20from%202025-05-28%2017-23-30.png?raw=true)`

### Soal 10

> Setelah seluruh fitur yang diminta Dosen dipenuhi dalam sistem operasi Budiman, sudah waktunya Budiman mengumpulkan tugasnya ini ke Dosen. Akan tetapi, Dosen Budiman tidak mau menerima pengumpulan selain dalam bentuk **.iso**. Untuk terakhir kalinya, Budiman meminta tolong kepadamu untuk mengubah seluruh konfigurasi sistem operasi yang telah kamu buat menjadi sebuah **file .iso**.

> After all the features requested by the lecturer have been implemented in Budiman's OS, it's time for Budiman to submit his assignment. However, Budiman's lecturer only accepts submissions in the form of **.iso** files. For the last time, Budiman asks for your help to convert the entire configuration of the OS you created into a **.iso file**.

**Answer:**

- **Code:**
```
  mkdir -p iso/boot/grub
cp bzImage iso/boot/
cp initramfs.cpio.gz iso/boot/

cat > iso/boot/grub/grub.cfg <<EOF
set timeout=0
set default=0

menuentry "OS Budiman" {
    linux /boot/bzImage console=ttyS0
    initrd /boot/initramfs.cpio.gz
}
EOF

grub-mkrescue -o osbudiman.iso iso/
```

- **Explanation:**

  `Membuat struktur direktori iso/boot/grub sebagai dasar sistem ISO berbasis GRUB.
Menyalin bzImage (kernel hasil kompilasi) dan initramfs.cpio.gz (initramfs yang sudah dibuat) ke dalam folder ISO.
Membuat file konfigurasi grub.cfg yang berisi instruksi boot GRUB:
Memuat kernel dengan linux /boot/bzImage console=ttyS0
Memuat initramfs dengan initrd /boot/initramfs.cpio.gz
Menggunakan grub-mkrescue untuk membungkus semuanya menjadi file ISO bernama osbudiman.iso.`

- **Screenshot:**

![image alt](https://github.com/xaldinzz/sisop3/blob/main/Screenshot%20from%202025-05-28%2017-28-47.png?raw=true)

---

Pada akhirnya sistem operasi Budiman yang telah kamu buat dengan susah payah dikumpulkan ke Dosen mengatasnamakan Budiman. Kamu tidak diberikan credit apapun. Budiman pun tidak memberikan kata terimakasih kepadamu. Kamupun kecewa tetapi setidaknya kamu telah belajar untuk menjadi pembuat sistem operasi sederhana yang andal. Selamat!

_At last, the OS you painstakingly created was submitted to the lecturer under Budiman's name. You received no credit. Budiman didn't even thank you. You feel disappointed, but at least you've learned to become a reliable creator of simple operating systems. Congratulations!_
