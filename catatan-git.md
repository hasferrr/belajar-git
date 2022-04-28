# Catatan git

## Meng-set folder menjadi repository

lakukan change directory terlebih dahulu dengan `cd`

kemudian set folder sebagai repo menggunakan `git init`

cek dulu mengguanakan `git status`

```bash
$ git status
On branch master
nothing to commit, working tree clean
```

## Melakukan commit pada git

Setelah melakukan save file di lokal, untuk melakukan commit, lakukan :

1. Memasukkan file yang akan di-commit ke *Staging Area*

    menambah file ke *Staging Area* satu per satu dengan :

    `git add file.format`

    menambah sekaligus (semua file yang ditambahkan, dihapus, diedit) :

    `git add .`

2. Melakukan commit

    login (digunakan hanya pada saat pertama kali menggunakan git bash)

    `git config --global user.email "you@example.com"`

    `git config --global user.name "Your Name"`

    melakukan commit

    `git commit -m "Deskripsi commit"`

3. Untuk mengetahui commit-commit apa saja yang sudah dilakukan

    melihat **semua** commit yang telah dilakuakan

    `git log`

    misal ingin melihat commit, 3 commit terakhir, atau n commit terakhir

    `git log -3`

    misal ingin melihat perubahan pada file tertentu apakah dihapus, diubahnya kapan, dll

    `git log --file file.format`

4. Melakukan checkout pada file tertentu

    `git checkout [hash] -- file.format`

    hash disini adalah lima digit pertama dari hash yang ditampilkan pada log (nomor 3) file yang telah di-commit yang ingin di-checkout

    file yang di-checkout akan masuk ke *Staging Area*

    karena baru masuk ke *Staging Area*, file tersebut harus di-commit terlebih dahulu
    coba cek menggunakan

    `git status`

    `git commit -m "pesan"`
