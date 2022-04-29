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
