
# BAB : Git Dasar

install code di command : view -> command palette -> install 'code' command in PATH

Sinkron username dan email

```bash
  git config --global user.name "nandoperd"
  git config --global user.email "nandoperd@gmail.com"
```

Setting visual studio menjadi default editor untuk git dan default diff tool

```bash
  git config --global core.editor "code --wait"
  git config --global diff.tool "default-difftool"
  git config --global difftool.default-difftool.cmd "code --wait --diff \$LOCAL \$REMOTE"
```

Melihat seluruh konfigurasi

```bash
  git config --list --show-origin
```

Membuat repository

```bash
  git init
```

Cek status repository

```bash
  git status
```

## Workflow

| Three States | Keterangan | Three Section         |
| :-------- | :------- | :------------------------- |
| **Modified** | add, edit, delete, namun belum disimpan permanen di repository | **Working Directory** |
| **Staged** | penanda modifikasi pada file yang akan disimpan permanen di repository | **Staging Area** |
| **Committed** | data sudah disimpan di repository | **Repository** |

## Snapshot & Hash

**Snapshot** adalah perubahan yang terjadi dan akan direkam, snapshot berisikian semua perubahan yang kita commit, setiap snapshot ini menghasilkan **hash** (seperti id)

## Alur

Buat file --> git add --> masuk ke staging area --> git commit -m --> masuk ke repository

## Ubah File

Cek perubahan
```bash
  git diff
```

Contoh add satu persatu ke staging
```bash
  git add file1.txt file2.txt
```

add semua file ke staging
```bash
  git add .
```

## Hapus File

Pada dasarnya menghapus file sama dengan menambah, alurnya :
git add file yang dihapus --> file nya masuk ke staging --> git commit file yang dihapus --> file yang dihapus tidak lagi di repository

## Membatalkan perubahan
#### -- Area Working directory --
Membatalkan penambahan file
```bash
  git clean -f
```

Membatalkan perubahan file
```bash
  git restore namafile
```

Membatalkan penghapusan file
```bash
  git restore namafile
```

#### -- Area Staging Index --

Jika ingin melakukan perubahan pada staging index, perlu untuk mengembalikannya ke working directory terlebih dahulu dengan cara :
```bash
  git restore --staged namafile
```

#### -- Area Repository --

Jika file sudah dicommit, tidak ada cara yang bisa dilakukan.
Ada 2 cara yang bisa dilakukan yaitu **Rollback Commit** atau **Revert Commit**

## Commit Log

commit log adalah riwayat (log) yang dilakukan pada file di dalam git

Cek commit log
```bash
  git log
```

Cek commit log lebih ringkas
```bash
  git log --oneline
```

Cek commit log graph
```bash
  git log --oneline --graph
```

Cek detail commit
```bash
  git show hash
```

Cek detail commit terbaru
```bash
  git show HEAD
```

Compare commit
```bash
  git diff hash hash
```

Compare commit menggunakan difftool (difftool harus diset seperti di atas terlebih dahulu)
```bash
  git difftool hash hash
```

## Rename File

ketika melakukan rename file, git membacanya file sebelumnya dihapus dan file dengan nama baru dianggap sebagai file baru. tapi jika file dengan nama lama dan baru diadd ke staging index, git akan membacanya sebagai rename.

alur : rename file -> add nama baru & lama -> staging area terdeteksi rename -> commit

## Reset Commit

git reset pada dasarnya adalah menggeser HEAD (hash terakhir) ke hash yang kita inginkan, kemudian hash yang di atasnya (lebih baru) akan dihapus

#### Mode git reset
- --soft   : perubahan pada hash setelahnya tidak direset di staging index dan working directory
- --mixed  : perubahan pada hash setelahnya tidak direset di working directory
- --hard   : perubahan pada hash direset semua

Contoh
```bash
  git reset --soft e3ac3c5
```

## Amend Commit
commit amend digunakan untuk melakukan commit sekaligus bersamaan dengan file yang belum dicommit. cara ini adalah yang lebih praktis dari commit reset. cara ini biasanya digunakan jika ada revisi pada isi file yang telah dicommit
note : commit ini akan mengganti nilai hash

Contoh
```bash
  git commit --amend -m "add file3.txt"
```

alur : commit file -> edit isi file -> add file -> commit ammend -> file berhasil dicommit bersama file lainnya

## Cek Versi File Sebelumnya
kita bisa melihat file pada versi sebelumnya dengan melakukan perintah checkout pada hash yang dituju. nantinya file tsb akan berpindah ke staging index

Contoh
```bash
  git checkout 5082d50 -- file1.txt
```

## Lihat Snapshot Sebelumnya
ini adalah cara untuk melihat snapshot yaitu file secara keseluruhan

alur : cek branch -> checkout branch --> checkout head yang dituju -> checkout branch (kembali)

cek branch (bisa master/main)
```bash
  git branch --show-current
```

contoh checkout
```bash
  git checkout 3183fea
```

contoh checkout kembali
```bash
  git checkout master
```

## Revert Commit
fungsinya adalah untuk membalik commit sebelumnya, jika reset adalah mengganti semua file commit, revert digunakan untuk mengembalikan hanya commit yang dituju

contoh : pada commit dengan hashe3ac3c5 saya melakukan rename file2.txt ke file_2.txt, dengan revert, maka file nya akan kembali jadi file2.txt

```bash
  git revert e3ac3c5
```

## Ignore
fungsinya untuk mengecualikan file yang tidak ingin disimpan di dalam git

alur : buat file .gitignore -> tulis di dalam .gitignore file yang dikecualikan -> commit .gitignore

## Blame
fungsinya untuk mencari tahu siapa yang melakukan perubahan dan juga commitnya

Contoh
```bash
  git blame file2.txt
```

Untuk melihat detailnya, gunakan hash nya contoh :
```bash
  git show 516384fe
```

## Alias
fungsinya seperti membuat shortcut pada perintah git

Contoh
```bash
  git config --global alias.logone "log --oneline"
```

maka hasilnya jika kita tuliskan perintah "git logone" hasilnya akan sama seperti perintah "git log --oneline"

# BAB : BRANCH

cek branch saat ini
```bash
  git branch --show-current
```

buat branch
```bash
  git branch namabranch
```

cek branch 
```bash
  git branch 
```

pindah ke branch yang dituju
```bash
  git switch namabranch
```
atau
```bash
  git checkout namabranch
```

ubah nama branch
```bash
  git branch -m namabranch
```

hapus branch
```bash
  git branch -d namabranch
```

## Multiple Branch
Membuat percabangan pada commit

alur : buat branch -> pindah ke branch yang dituju -> add & commit file pada branch



## Merge
Menggabungkan (melakukan penarikan) percabangan pada commit

alur : pindah ke lokasi branch yang akan dimerge

Contoh
```bash
  git merge fitur/1
```

## Merge Conflict
adalah situasi ketika melakukan merge file pada branch yang berbeda

Membatalkan conflict
```bash
  git merge --abort
```
Memperbaiki conflict
untuk memperbaiki conflict harus dilakukan secara manual pada file yang error

alur : merge conflict -> perbaiki manual file yang conflict -> add & commit file

## Cherry Pick
digunakan untuk mengambil commit pada branch lain yang ingin ditambahkan pada branch utama

```bash
  git cherry-pick commitid
```

# Git Remote
ketika git sudah siap untuk diupload, saatnya untuk menyimpannya di server git

alur : buat ssh di desktop -> menambahkan SSH public key ke github (github.com/settings/keys) -> buka id_rsa.pub copy dan add di SSH keys github -> tes SSH ke github 

Membuat SSH (Secure Shell)
```bash
  ssh-keygen
```

Tes SSH
```bash
  ssh -T git@github.com
```

## Remote Repository
untuk melakukan remote repository dapat menggunakan git remote add nama ssh-url

contoh
```bash
  git remote add origin git@github.com:nandoperd/git.git
```

melihat remote
```bash
  git remote
  git remote get-url origin
```

hapus remote
```bash
  git remote rm origin
```

## Push
melakukan upload ke github

push dengan nama yang sama (origin : branch, master : commit di local)
```bash
  git push origin master
```

push dengan nama yang beda
```bash
  git push origin master:development
```

push semua branch local ke github
```bash
  git push origin --all
```

menghapus branch (di remote)
```bash
  git push --delete origin fitur/d
```
