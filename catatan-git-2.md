# Catatan Branch dan Merge

## Branch

1. Melihat list branch

    `git branch`

    ```bash
    $ git branch
    * master
    ```

    disitu terlihat ada 1 branch, yaitu branch **master**

2. Membuat branch baru

    `git branch <nama_branch>`

    ```bash
    $ git branch edit-catatan-2
    $ git branch
      edit-catatan-2
    * master
    ```

    branch sudah diduplikat/ditambahkan/di-snapshot, tetapi kita masih berada di branch **master** (yang ada tanda bintang di sebelah kiri dan berwarna hijau pada bash)

    branch yang dibuat/diduplikat merepresentasikan commit-an branch saat ini (ketika membuat branch baru pada branch **master**, maka branch baru tersebut merupakan duplikat dari branch **master**, merupakan perubahan terakhir pada branch **master**)

3. Cara pindah branch

    cara memindah HEAD ke lain branch (pindah branch)

    `git checkout <nama_branch>`

    ```bash
    $ git checkout master
    Switched to branch 'master'
    M       catatan-git-2.md
    ```

4. Cara menghapus branch

    `git branch -d <branch>`

    ```bash
    $ git branch -d edit-catatan-2
    Deleted branch edit-catatan-2 (was 1b5dc6d).
    ```

    branch yang belum di-merge apabila dihapus, akan muncul peringatan bahwa branch tersebut belum dimerge, gunakan `-D` untuk menghapusnya

## Merge

ada 2 tipe merge, yaitu

- *fast forward* = merge yang ada pada jalur langsung (direct path)
- *three-way merging* = merge branch dengan branch (merge dengan commit)

1. Cara merge

    checkout dulu ke branch sebelumnya

    ```bash
    $ git checkout master
    Switched to branch 'master'
    ```

    merge dengan command `git merge <branch>`

    Contoh output :

    ```bash
    $ git merge edit-catatan-2
    Merge made by the 'ort' strategy.
    catatan-git.md => catatan-git-1.md |  0
    catatan-git-2.md                   | 58 +++++++++++++++++++++++++++++++++++++-
    2 files changed, 57 insertions(+), 1 deletion(-)
    rename catatan-git.md => catatan-git-1.md (100%)
    ```

2. Cek branch mana saja yang sudah di-merge

    `git branch --merged`

## Merge conflict

merge conflict dapat terjadi ketika merge dua branch dilakukan, sedangkan kedua branch tersebut mengubah/mengerjakan line/baris yang sama pada suatu file

tipe merge ini adalah *three-way merging*

contohnya, misal branch *master* akan merging dengan branch *branch-2*

```bash
$ git merge add
Auto-merging catatan-git-1.md
CONFLICT (content): Merge conflict in catatan-git-1.md
Automatic merge failed; fix conflicts and then commit the result.
```

akan muncul conflict pada text editor sebagai berikut

```plaintext
<<<<<< HEAD
catatan ini dibuat dari playlist video-video youtube
=======
sumber catatan
>>>>>> branch-2
```

`<<< HEAD` merupakan current change atau branch saat ini, `>>> branch-2` merupakan incoming change atau branch yang mau digabungkan

tinggal diedit sesuai preferensi dari conflict tersebut

git marker-nya juga dihapus (tanda `<<<, >>>, dan ===`)

misalnya, conflict tersebut diedit menjadi seperti ini :

```plaintext
catatan ini dibuat dari playlist youtube
```

setelah itu, lanjutkan proses merging, dengan melakukan commit

```bash
$ git status
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   catatan-git-1.md

no changes added to commit (use "git add" and/or "git commit -a")
$ git add catatan-git-1.md
$ git commit -m "merging branch 'branch-2'"
[master 33cbce7] merging branch 'branch-2'
```

merging selesai
