# catatan git

## meng-set folder menjadi repository

lakukan change directory terlebih dahulu dengan `cd`

kemudian set folder sebagai repo menggunakan `git init`

```git
$ git status
On branch master
nothing to commit, working tree clean
```

## melakukan commit pada git

Setelah melakukan save file di lokal, untuk melakukan commit, lakukan :

1. memasukkan file yang akan di-commit ke Staging Area

    untuk menambah file ke Staging Area satu per satu

    `git add file.format`

    sekaligus

    `git add .`

2. melakukan commit

    melakukan 'login' (hanya untuk pertama kali menggunakan git bash)

    ```git
    git config --global user.email "you@example.com"
    git config --global user.name "Your Name"
    ```

    melakukan commit

    `git commit -m "Deskripsi commit"`

3. utuk mengetahui commit-commit apa saja yang sudah dilakukan

    melihat **semua** commit yang telah dilakuakan

    `git log`

    misal ingin melihat commit, 3 commit terakhir

    `git log -3`

    misal ingin melihat perubahan pada file tertentu apakah dihapus, diubahnya kapan, dll

    `git log --file file.format`

4. melakukan checkout pada file tertentu

    `git checkout [hash] -- file.format`

    hash disini adalah lima digit pertama dari hash yang ditampilkan pada log (nomor 3) file yang telah di-commit yang ingin di-checkout

    file yang dicheckout akan masuk ke Staging Area
    karena baru masuk ke Staging Area, file tersebut harus di-commit terlebih dahulu
    coba cek menggunakan

    `git status`
    `git commit -m "pesan"`
