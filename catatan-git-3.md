# Catatan Git Remote HTTPS method

## Clone repository dari github ke local

  cloning dengan `git clone <link_https_repo>`

  ```bash
  $ git clone https://github.com/hasferrr/lagi-belajar.git
  Cloning into 'lagi-belajar'...
  remote: Enumerating objects: 107, done.
  remote: Counting objects: 100% (21/21), done.
  remote: Compressing objects: 100% (21/21), done.
  Receiving objects:  75% (81/107)
  Receiving objects: 100% (107/107), 50.33 KiB | 613.00 KiB/s, done.
  Resolving deltas: 100% (22/22), done.
  ```

## Remote git dari local

cek nama setelah cloning selesai (origin adalah nama default)

```bash
$ git remote
origin
$ git remote -v
origin  https://github.com/hasferrr/lagi-belajar.git (fetch)
origin  https://github.com/hasferrr/lagi-belajar.git (push)
```

cek status

```bash
$ git status
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```

apabila commit di-execute pada local, status akan berubah

```bash
$ git status
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

lakukan `git push` untuk mengirimkan perubahan file ke github (login dulu apabila diminta)

```bash
$ git push
info: please complete authentication in your browser...
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Delta compression using up to 4 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 220 bytes | 110.00 KiB/s, done.
Total 2 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/hasferrr/lagi-belajar.git
   6a18bd2..46a08cb  main -> main
```

## 'Clone' atau remote repository dari local ke github (di github belum ada repository tersebut)

1. Buat repo baru di github dengan nama repo yang sama **tanpa** file README.md

    buat repo di github dengan nama repo yang sama dengan repo di local yang akan ditambahkan remotnya ke github

    jangan initialize repository (di github) dengan README.md (kosongan)
  
2. Tambahkan remote

    push an existing repository from the command line (cara ini ditampilkan di github)

    branch yang sebelumnya *master* akan berubah menjadi *main*

    ```bash
    git remote add origin https://github.com/UserName/NamaRepo.git
    git branch -M main
    git push -u origin main
    ```
