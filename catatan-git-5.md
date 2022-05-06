# Git Rebase

`Rebase` digunakan sebagai alternatif dari `Merge` yang membuat commit baru (*three-way merging*)

Rebase digunakan untuk menggeser/memindahkan dasar branch dari suatu branch tertentu ke commit main/master yang baru (yg menjadi penyebab *three-way merging*)

ilustrasi dari javatpoint :

![rebase](https://static.javatpoint.com/tutorial/git/images/git-rebase.png)

selanjutnya, apabila kita melakukan `merging`, tidak lagi *three-way merging*, melainkan *fast forward merging* sehingga tidak menambahkan commit baru ketika nantinya dilakukan merging

rebase digunakan untuk memudahkan pengguna menge-track log/graph history dari commit-commit yang sudah dilakukan

## Cara rebase

`git rebase <branch_name>`

## Contoh

user menggunakan git bash membuat `branch` *cat5* baru pada salah satu repository

```bash
$ git branch cat5
$ git checkout cat5
Switched to branch 'cat5'
```

kemudian melakukan `commit`

```bash
git commit -m "menambahkan deskripsi rebase"
 ```

berikut tampilan graph-nya

```bash
$ gh
* d4bf09c (HEAD -> cat5) menambahkan deskripsi rebase
* 5d8aa00 (origin/main, origin/HEAD, main) Create catatan-git-5.md
* 248b13f mengubah command dan menambahkan link referensi
* 4eff721 minor changes catatan git 3
```

setelah itu, sebelum dilakukan merge, lakukan `fetch` terlebih dahulu

```bash
$ git fetch
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), 688 bytes | 57.00 KiB/s, done.
From https://github.com/hasferrr/belajar-git
   5d8aa00..686ad32  main       -> origin/main
```

ternyata **ada perubahan** pada remote repository-nya, dan sekarang ada 2 cabang (*main* menambahkan 1 commit, *cat5* menambahkan 1 commit)

```bash
$ gh
* d4bf09c (HEAD -> cat5) menambahkan deskripsi rebase
| * 686ad32 (origin/main, origin/HEAD) menambahkan cara rebase
|/
* 5d8aa00 (main) Create catatan-git-5.md
* 248b13f mengubah command dan menambahkan link referensi
* 4eff721 minor changes catatan git 3
```

lakukan `pull` untuk mengambil perubahan tersebut

pindah/`checkout` dulu ke branch *main* untuk melakukan pull

```bash
$ git checkout main
Switched to branch 'main'
Your branch is behind 'origin/main' by 1 commit, and can be fast-forwarded.
  (use "git pull" to update your local branch)

$ git pull
Updating 5d8aa00..686ad32
Fast-forward
 catatan-git-5.md | 2 ++
 1 file changed, 2 insertions(+)
```

selanjutnya, apabila dilakukan merge, akan menjadikannya three-way merging (menambahkan commit baru untuk merging)

akan tetapi, kita akan melakukan `rebase` untuk menggeser **base** branch *cat5* ke commit baru yang dilakukan di *main* (jadi seakan-akan branch *cat5* dibuat setelah 1 commit yang ditambahkan pada *main*)

`rebase` dilakukan di branch yang akan di-rebase

pindah dulu ke branch *cat5*

lakukan `git rebase <branch_name>`

```bash
$ git checkout cat5
Switched to branch 'cat5'

$ git rebase main
Auto-merging catatan-git-5.md
CONFLICT (add/add): Merge conflict in catatan-git-5.md
error: could not apply a9b351e... menambahkan file catatan-git-5.md
hint: Resolve all conflicts manually, mark them as resolved with
hint: "git add/rm <conflicted_files>", then run "git rebase --continue".
hint: You can instead skip this commit: run "git rebase --skip".
hint: To abort and get back to the state before "git rebase", run "git rebase --abort".
Could not apply a9b351e... menambahkan file catatan-git-5.md
```

> jika rebase ada conflict, resolve dulu dan lakukan **`git add`** lalu dilanjutkan dengan **`git rebase --continue`**

> Watch this video : [Resolve merge conflict during git rebase](https://www.youtube.com/watch?v=RGtwxYqkkas)

lihat graph-nya setelah rebase, sudah sejajar (artinya *cat5* seakan-akan dibuat setelah commit pada *main* 686ad32 "menambahkan cara rebase", bukan setelah commit 5d8aa00 "Create catatan-git-5.md" seperti sebelumnya)

```bash
$ gh
* 620dc53 (HEAD -> cat5) menambahkan deskripsi rebase
* 686ad32 (origin/main, origin/HEAD, main) menambahkan cara rebase
* 5d8aa00 Create catatan-git-5.md
* 248b13f mengubah command dan menambahkan link referensi
* 4eff721 minor changes catatan git 3
```

selanjutnya, dapat dilakukan `merge` (fast forward) atau `rebase` (sama aja kayak merge (soalnya fast forward))

## Lain-lain mengenai git rebase

[A Better Git Workflow with Rebase](https://www.youtube.com/watch?v=f1wnYdLEpgI)

[Git Rebase - javatpoint](https://www.javatpoint.com/git-rebase)
