
# git dasar

Catatan git dasar


## Catatan

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