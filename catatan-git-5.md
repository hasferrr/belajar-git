# Git Rebase

`Rebase` digunakan sebagai alternatif dari `Merge` yang membuat commit baru (*three-way merging*)

Rebase digunakan untuk menggeser/memindahkan dasar branch dari suatu branch tertentu ke commit main/master yang baru (yg menjadi penyebab *three-way merging*)

ilustrasi dari javapoint :

![rebase](https://static.javatpoint.com/tutorial/git/images/git-rebase.png)

selanjutnya, apabila kita melakukan `merging`, tidak lagi *three-way merging*, melainkan *fast forward merging* sehingga tidak menambahkan commit baru ketika nantinya dilakukan merging

rebase digunakan untuk memudahkan pengguna menge-track log/graph history dari commit-commit yang sudah dilakukan

More : [Git Rebase](https://www.javatpoint.com/git-rebase)

## Cara rebase

`git rebase <branch_name>`

## Contoh
