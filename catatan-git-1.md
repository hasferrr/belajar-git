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

    menambah sekaligus file ke *Staging Area* (semua file yang ditambahkan, dihapus, diedit) :

    `git add .`

2. Melakukan commit

    login (digunakan hanya pada saat pertama kali menggunakan git bash) (user dan email bisa disamakan dengan user dan email github)

    ```bash
    git config --global user.email "you@example.com"
    git config --global user.name "Your Name"
    ```

    config bisa dicek di `git config --list`

    melakukan commit

    `git commit -m "Deskripsi commit"`

    melakukan commit tanpa memasukkannya ke *Staging Area* terlebih dahulu (tanpa step 1) (atau tanpa melaukan `git add`) (hanya berlaku untuk *modified* file, bukan *untrack* file, in which *untrack* file harus dimasukkan ke *Staging Area* terlebih dahulu)), commit dilakukan dengan cara

    `git commit -am "Deskripsi commit"`

3. Untuk mengetahui commit-commit apa saja yang sudah dilakukan

    melihat **semua** commit yang telah dilakuakan

    `git log`

    misal ingin melihat commit, 3 commit terakhir, atau n commit terakhir

    `git log -3`

    misal ingin melihat perubahan pada file tertentu apakah dihapus, diubahnya kapan, dll

    `git log --file file.format`

    menampilkan visualisasi log atau branch dalam bentuk graph

    `git log --all --decorate --oneline --graph`

    ```bash
    $ git log --all --decorate --oneline --graph
    * 8222d0f (HEAD -> master, edit-catatan-2) mengubah catatan-git dan menambahkan file catatan-git-2.md
    * a8fcee8 Mengubah file hasfer-resolusi
    * d5c2769 update dan merapihkan catatan-git
    * f5ccd5f menambahkan cara meng-set repo dengan git init pada catatan dan perubahan kecil lainnya
    * fe8552c menambahkan nomor 3 dan 4 pada catatan-git.md
    * bce4316 mengubah isi file catatan-git
    * 110231e menambahkan file catatan-git.md dan hasfer-resolusi.md
    ```

4. Melakukan checkout pada file tertentu

    `git checkout <hash> -- file.format`

    hash ini adalah lima digit pertama dari hash yang ditampilkan pada log (nomor 3) file yang telah di-commit yang ingin di-checkout

    file yang di-checkout akan masuk ke *Staging Area*

    karena baru masuk ke *Staging Area*, file tersebut harus di-commit terlebih dahulu apabila ingin melakukan perubahan tersebut (rollback)

    coba cek menggunakan

    `git status`

    untuk commit, seperti biasa

    `git commit -m "pesan"`

## Membuat *alias*

`alias <nama alias>="commandnya"` digunakan untuk menyubstitusikan nama atau alias dengan command tertentu menjadi command tersebut

alias hanya berlaku satu sesi, sampai git bash di-close

```bash
$ alias wkwk="git status"
$ wkwk
On branch master
nothing to commit, working tree clean
```

alias yang sering digunakan

```bash
$ alias graph="git log --all --decorate --oneline --graph"
$ graph
* 08a8b76 (HEAD -> main, origin/main) minor changes
* ae8a2b0 memindahkan referensi dari catatan-git-1 ke README
* 03c8bfd menambahkan file README.md
* f72a789 menambahkan file catatan-git-3.md
* c672da4 minor changes in catatan-git-1
* db8a1aa menghapus file hasfer-resolusi.md
* 76b3cd4 menambahkan cara merge conflict
*   33cbce7 merging branch 'add'
|\
| * 1a7fa3c menambahkan sumber catatan 1
* | ea5ca5a menambahkan link sumber pada catatan-git-1
|/
* 644c245 mengedit catatan-git-1
* 16a6b43 mengedit catatan-git-2
```
