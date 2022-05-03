# Multiple Remote

## Asumsi

asumsikan bahwa telah dilakukan :

```bash
alias graph="git log --all --decorate --oneline --graph"
```

## Contoh case

- Multiple remote dimaksudkan untuk menghubungkan/mensinkronkan repository ke beberapa remote sekaligus (lokal dan 2 remote yang berbeda)

- misalkan *hasferrr* melakukan **fork** salah satu repository yang ada di *moe-channel-id* (di github)

- fork dilakukan (*hasfer* melakukan forking repository *moe-channel-id*)

- kemudian, `clone` repository hasil fork *hasferrr* dilakukan, menyimpannya di lokal, dengan cara `git clone <url>`

    ```bash
    $ git clone https://github.com/hasferrr/simple-landing-page.git
    Cloning into 'simple-landing-page'...
    remote: Enumerating objects: 92, done.
    remote: Counting objects: 100% (41/41), done.
    remote: Compressing objects: 100% (22/22), done.
    Receiving objects: 100% (92/92), 1.98 MiB | 1.84 MiB/s, done.d 51

    Resolving deltas: 100% (35/35), done.
    ```

- ketika melakukan cloning, nama default remote-nya adalah **origin**, yaitu remote yang terhubung ke *hasferrr*

    ```bash
    $ git remote -v
    origin  https://github.com/hasferrr/simple-landing-page.git (fetch)
    origin  https://github.com/hasferrr/simple-landing-page.git (push)
    ```

- akan tetapi apabila di repository *moe-channel-id* melakukan perubahan, git di lokal tidak akan mendeteksinya karena belum menambahkan remote repository aslinya
- maka dari itu, dilakukan `remote add` sumber repository/repository aslinya yang telah di fork tersebut agar dapat di-track perubahannya, dalam hal ini adalah *moe-channel-id*
- dilakukan dengan `git remote add <name> <url>`
- `<name>` tidak harus exact nama repository (bebas)

    ```bash
    $ git remote add moe-channel-id https://github.com/moe-channel-id/simple-landing-page.git

    $ git remote -v
    moe-channel-id  https://github.com/moe-channel-id/simple-landing-page.git (fetch)
    moe-channel-id  https://github.com/moe-channel-id/simple-landing-page.git (push)
    origin  https://github.com/hasferrr/simple-landing-page.git (fetch)
    origin  https://github.com/hasferrr/simple-landing-page.git (push)
    ```

- berikut adalah history perubahan commit **lokal** (yang terhubung ke *hasferrr*) dan ***hasferrr***

    ```bash
    $ graph
    * 034de12 (HEAD -> master, origin/master, origin/HEAD) mengubah title
    * bd7b908 mengubah tulisan brand menjadi sandhika
    * db75944 mengubah warna tombol our work
    ```

- untuk melihat history perubahan sumber repository-nya, gunakan `git fetch <repository>` untuk mengambil data perubahan dari remote repository tersebut (dalam kasus ini, fetching remote repository asal yaitu *moe-channel-id*)
- `<repository>` adalah nama remote repository
- graph berikut ini juga memperlihatkan bahwa posisi HEAD/commit ketiga repository-nya sudah sama

    ```bash
    $ git fetch moe-channel-id
    From https://github.com/moe-channel-id/simple-landing-page
    * [new branch]      master     -> moe-channel-id/master

    $ graph
    * 034de12 (HEAD -> master, origin/master, origin/HEAD, moe-channel-id/master) mengubah title
    * bd7b908 mengubah tulisan brand menjadi sandhika
    * db75944 mengubah warna tombol our work
    ```

- beberapa saat kemudian, dilakukan *fetch* kembali untuk mengecek perubahan dan ternyata *moe-channel-id* membuat perubahan di repository-nya
- pada graph, terlihat bahwa `moe-channel-id` mendahului satu commit

    ```bash
    $ git fetch moe-channel-id
    remote: Enumerating objects: 5, done.
    remote: Counting objects: 100% (5/5), done.
    remote: Compressing objects: 100% (3/3), done.
    remote: Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
    Unpacking objects: 100% (3/3), 744 bytes | 82.00 KiB/s, done.
    From https://github.com/moe-channel-id/simple-landing-page
    034de12..efbfe3b  master     -> moe-channel-id/master

    $ graph
    * efbfe3b (moe-channel-id/master) mengupdate title
    * 034de12 (HEAD -> master, origin/master, origin/HEAD) mengubah title
    * bd7b908 mengubah tulisan brand menjadi sandhika
    * db75944 mengubah warna tombol our work
    ```

- untuk menyamakan file/git lokal dengan file/git pada repository sumber (yaitu *moe-channel-id*), lakukan `merge` git lokal ke remote repository sumber
- lakukan dengan cara `git merge <remote>/<branch>`
- lokal sekarang sudah sama dengan repo aslinya, terlihat dari graph berikut

    ```bash
    $ git merge moe-channel-id/master
    Updating 034de12..efbfe3b
    Fast-forward
    index.html | 2 +-
    1 file changed, 1 insertion(+), 1 deletion(-)

    $ graph
    * efbfe3b (HEAD -> master, moe-channel-id/master) mengupdate title
    * 034de12 (origin/master, origin/HEAD) mengubah title
    * bd7b908 mengubah tulisan brand menjadi sandhika
    * db75944 mengubah warna tombol our work
    ```

- lakukan `push` untuk menyamakan repository lokal (yang sudah sama dengan *moe-channel-id*) dengan *hasferrr*

    ```bash
    $ git push -u origin master
    Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
    To https://github.com/hasferrr/simple-landing-page.git
    034de12..efbfe3b  master -> master

    $ graph
    * efbfe3b (HEAD -> master, origin/master, origin/HEAD, moe-channel-id/master) mengupdate title
    * 034de12 mengubah title
    * bd7b908 mengubah tulisan brand menjadi sandhika
    * db75944 mengubah warna tombol our work
    ```

- ketiga repository sudah tersinkron

## Recap dan commands

**repo lokal** <---*clone*--- **repo hasferrr (origin)** <---*forking*--- **repo moe-channel-id (moe-channel-id)**

commands :

```bash
git clone <url>
git remote add <name> <url>
git remote -v
git fetch <repository>
git merge <remote>/<branch>
git push -u origin master
```

## Referensi tambahan

[3.5 Git Branching - Remote Branches](https://git-scm.com/book/en/v2/Git-Branching-Remote-Branches)
