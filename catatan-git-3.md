# Git Remote

## Clone repository dari github ke local (HTTPS method)

  cloning dengan `git clone <url_repo>`

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

## Clone repository dari github ke local (SSH method)

Buka link berikut : [GitHub Docs - About SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/about-ssh)

baca dan ikuti step2nya

## Remote git dari local

cek nama setelah cloning selesai
> note : "origin" is the default name for a remote

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

lakukan `git push <remote> <branch>` untuk mengirimkan perubahan file ke github (login dulu apabila diminta)

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

    push an existing repository from the command line (cara dan command di bawah ditampilkan di github)

    branch yang sebelumnya *master* akan berubah menjadi *main*

    ```bash
    git remote add origin https://github.com/UserName/NamaRepo.git
    git branch -M main
    git push -u origin main
    ```

## Git Fetch dan Pull

Fetch digunakan untuk mendapatkan/melihat perubahan terakhir dari remote repository (github) dan tidak akan mengubah isi local Git

Fetch digunakan untuk mengecek perubahan terakhir dari commit di remote repository

Fetch digunakan apabila terjadi rejection ketika melakukan push karena adanya perubahan pada file/line yang sama yang akan di-push dengan file/line pada remote repository (merge/push conflict)

```bash
$ git push
To https://github.com/hasferrr/belajar-git.git
 ! [rejected]        main -> main (fetch first)
error: failed to push some refs to 'https://github.com/hasferrr/belajar-git.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

`git status` masih menunjukkan origin is ahead/lebih dulu 1 commit karena git mengasumsikan bahwa tidak ada perubahan pada remote repository

```bash
$ git status
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

`git fetch <remote>` digunakan untuk mengecek dulu dimana letak commit pada remote repository dan mengambil data perubahan (tidak dengan file) tersebut dari remote repo

```bash
$ git fetch
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 3 (delta 2), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), 713 bytes | 15.00 KiB/s, done.
From https://github.com/hasferrr/belajar-git
   08a8b76..01b0764  main       -> origin/main
```

cek status lagi, branch akan diverged/dibedakan (karena data telah diambil dari remote dengan fetching)

```bash
$ git status
On branch main
Your branch and 'origin/main' have diverged,
and have 1 and 1 different commits each, respectively.
  (use "git pull" to merge the remote branch into yours)

nothing to commit, working tree clean
```

masih cek status, lihat branch-nya have deverged

```bash
$ git log --all --decorate --oneline --graph
* 6e819a1 (HEAD -> main) menambahkan contoh pada bagian alias
| * 01b0764 (origin/main) Update catatan-git-1.md
|/
* 08a8b76 minor changes
* ae8a2b0 memindahkan referensi dari catatan-git-1 ke README
* 03c8bfd menambahkan file README.md
```

lakukan `git pull <remote>` untuk mengambil file perubahan dan akan langsung melakukan merge ke file di local (pull akan mengubah file local sesuai pada remote repository ! (merging)) (merge conflict akan ditampilkan jika ada)

```bash
$ git pull
Auto-merging catatan-git-1.md
CONFLICT (content): Merge conflict in catatan-git-1.md
Automatic merge failed; fix conflicts and then commit the result.
```

tampilan merge conflict akan seperti sebelumnya

```bash
<<<<<< HEAD
perubahan 1
=======
perubahan 2
>>>>>> 01b07646d7aedeac0a644b0f0d64ae69def529f1
```

lakukan commit apabila conflict sudah di-resolve

```bash
$ git commit -m "menambahkan contoh alias"
[main 537df2a] menambahkan contoh alias
$ git status
On branch main
Your branch is ahead of 'origin/main' by 2 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

lakukan `git push <remote> <branch>`, maka akan dilakukan merging

```bash
$ git push
Enumerating objects: 10, done.
Counting objects: 100% (10/10), done.
Delta compression using up to 4 threads
Compressing objects: 100% (6/6), done.
Writing objects: 100% (6/6), 890 bytes | 890.00 KiB/s, done.
Total 6 (delta 4), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (4/4), completed with 2 local objects.
To https://github.com/hasferrr/belajar-git.git
   01b0764..537df2a  main -> main
```
