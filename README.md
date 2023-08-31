
# Catatan Git dasar

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