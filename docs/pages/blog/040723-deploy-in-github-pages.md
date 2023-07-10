---
template: post
title: "Menghosting Rust Project di Github Pages"
author: Syuhendar
author_link: https://instagram.com/syuhendar729
date_published: 3 Juli, 2023
---

### Cara Menghosting
- Clone repository ini di local
- Buat organizations di github baru dengan nama yang diinginkan (ex: myorganisasi)
- Buat repository organisasi.github.io
- Masuk settings organizations (bukan repository) 
- Masuk ke bagian *Member Privileges*
- Ubah *Pages Creation* dan *Repository Creation* menjadi public dan hanya public
- Ubah seperti biasa remote folder local yang berasal dari clone tadi
- Kemudian push ke remote tersebut repository organisasi.github.io
- Tunggu proses build
- Selesai, web dapat diakses di organisasi.github.io

### Fyi
- Membuat organisasi baru bertujuan agar repository root memiliki domain yang diinginkan sesuai nama organisasi
- Untuk project rust lainnya pelajarilah CI/CD github actions terutama dalam mendeploy Rust project
- Yang perlu di garis bawahi adalah CI/CD di dalam folder `.gihub/workflow/` lah yang membuat situs ini bisa
dihosting di dalam github pages
- Kalian bisa mengubah:
```yml
# Sesuaikan dengan page_url, btw biasanya inilah penyebab terbesar gagal dideploy
url: ${{ steps.deployment.outputs.page_url }}
```
- Oleh karena itu disarankan menggunakan domain sendiri atau organisasi baru agar konfigurasi bisa mendapatkan
`page_url` yang sesuai
- Kalau semisalnya mau dipublish ke `username.github.io` juga bisa, tetapi tidak disarankan kalau repository
tersebut sudah ada.

