# melakukan commit pada git

Setelah melakukan save file di lokal, untuk melakukan commit, lakukan :

1. memasukkan file yang akan dicommit ke Staging area

    untuk menambah file ke staging area satu per satu

    `git add file.format`

    sekaligus

    `git add .`

2. melakukan commit

    melakukan 'login'

    ```git
    git config --global user.email "you@example.com"
    git config --global user.name "Your Name"
    ```

    melakukan commit

    `git commit -m "Deskripsi commit"`
