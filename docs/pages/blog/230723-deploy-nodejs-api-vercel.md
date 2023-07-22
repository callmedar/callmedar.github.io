---
template: post
title: "Dokumentasi Mendeploy API Express dan Nodejs di Vercel"
author: Syuhendar
author_link: https://instagram.com/syuhendar729
date_published: 8 Juli, 2023
---

Pada halaman ini saya ingin berbagi kisah saya mengenai deploying sebuah aplikasi back-end di Vercel.

Jadi setelah saya membuat sebuah Rest API dengan Nodejs dan Express, saya kepikiran bagaimana caranya mendeploy API tersebut
di sebuah platform yang gratis. Kemudian saya pernah tau bahwa Vercel itu bisa mendeploy project yang didasari dengan Nodejs.
Karena saya tertarik, saya mencoba mencari cara untuk mendeploy-nya disana.

Pada percobaan pertama seperti pada umumnya, mau sehebat apapun orang biasanya mereka gagal di tahap ini.
Kegagalan pertama saya adalah tampilnya 500 internal server error ketika API diakses.
Fyi project pertama saya adalah project Nodejs, Express, dan MongoDB yang mana disitu kita bisa melakukan CRUD sederhana ke database.

Setelah dicari tahu ternyata kegagalan tersebut dapat disolve dengan konfigurasi Vercel yang sesuai.
Disini saya hanya akan memberitahu video penjelasan saya saja karna sepertinya itu sudah lebih dari cukup.

Berikut adala link videonya:

<iframe width="800" height="450" src="https://www.youtube.com/embed/BuIhsqWYKaw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen
style="margin-bottom: 50px;"></iframe>


Nah, kemudian setelah project itu selesai saya sempat ada trouble lagi dengan project lain. Projectnya adalah project API Firebase yang mana kita membutuhkan sebuah file `ServiceAccountKey.json` yang berisi credential kita. Padahal ketika kita push ke github kita tidak mau file tersebut ikut terbawa. Akhirnya disini saya mencari cara yang agak tricky untuk berhasil mendeploy-nya.

Cara yang saya gunakan adalah dengan memasukkan satu-satu environment variable yang kita inputkan di Vercel sebelum mendeploy project. Kemudian environment variable tersebut saya panggil dengan `process.env.NAMA_VAR` di file konfigurasi yang tidak ada credential-nya.

Karna saya tau konfigurasi `ServiceAccountKey.json` adalah file yang berisi object JSON dan kemudian dipanggil ketika ingin menjalankan aplikasi firebase, saya bisa menjadikannya sebagai kode berikut:

```javascript
vercelConfig.js
--------------------------------------
const serviceAccount = {
    type: "service_account",
    project_id: process.env.PROJECT_ID,
    private_key_id: process.env.PRIVATE_KEY_ID,
    private_key: process.env.PRIVATE_KEY,
    client_email: process.env.CLIENT_EMAIL,
    client_id: process.env.CLIENT_ID,
    auth_uri: "https://accounts.google.com/o/oauth2/auth",
    token_uri: "https://oauth2.googleapis.com/token",
    auth_provider_x509_cert_url: "https://www.googleapis.com/oauth2/v1/certs",
    client_x509_cert_url: process.env.CLIENT_CERT_URL,
    universe_domain: "googleapis.com"
}

module.exports = serviceAccount
```

- Dari yang awalnya adalah seperti ini:
```json
ServiceAccountKey.json
--------------------------------------

{
    "type": "service_account",
    "project_id": "***",
    "private_key_id": "***",
    "private_key": "-----BEGIN PRIVATE KEY-----***-----END PRIVATE KEY-----\n",
    "client_email": "***",
    "client_id": "***",
    "auth_uri": "https://accounts.google.com/o/oauth2/auth",
    "token_uri": "https://oauth2.googleapis.com/token",
    "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
    "client_x509_cert_url": "***",
    "universe_domain": "googleapis.com"
}

```

Nah saran saya lebih baik kalian kalau mau coba, coba dulu di local dengan `.env` apakah bekerja atau tidak. Jangan lupa kalau pake Nodejs dan Express install dulu `dotenv` nya ya dengan `npm`. Kemudian kita panggil juga confignya seperti ini:
```bash
PROJECT_ID=""
PRIVATE_KEY_ID=""
PRIVATE_KEY=""
CLIENT_EMAIL=""
CLIENT_ID=""
CLIENT_CERT_URL="" 
```

Terus panggil config di `app.js` kalian atau sesuaikan dengan file utama Nodejs kalian.
```javascript
require('dotenv').config()
```


Nah langkah terakhir tinggal `import` deng `.env` nya ke Vercel. Biar ga repot-repot nulis lagi.
