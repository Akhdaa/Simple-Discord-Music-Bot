# Simple Discord Music Bot

Bot Discord buat muter lagu dari YouTube di voice channel. Bisa dikontrol pakai slash command (`/play`) atau prefix (`!play`), dan di pesan player ada tombol buat pause, skip, dan loop.

Yang bisa dilakukan:

- Putar lagu dari judul atau link YouTube
- Antrian, loop satu lagu, dan autoplay (muter lagu terkait kalau antrian habis)
- `/search` untuk milih dari beberapa hasil pencarian
- Pesan player dengan progress bar dan tombol replay, pause, skip, stop, loop

## Yang dibutuhkan

- Node.js 22.12 atau lebih baru
- Token bot Discord

ffmpeg dan yt-dlp ikut terpasang lewat `npm install`, jadi tidak perlu dipasang sendiri.

## Bikin bot di Discord

1. Buka [Discord Developer Portal](https://discord.com/developers/applications), klik **New Application**, kasih nama.
2. Di tab **Bot**, klik **Reset Token** lalu salin tokennya. Jangan dibagikan ke siapa pun.
3. Masih di tab **Bot**, nyalakan **Message Content Intent**. Ini dipakai buat command berawalan `!`. Intent lainnya tidak perlu.
4. Di **OAuth2 → URL Generator**, pilih scope `bot` dan `applications.commands`, lalu permission berikut: View Channels, Send Messages, Embed Links, Read Message History, Connect, Speak.
5. Buka URL yang dihasilkan, pilih server tujuan.

## Menjalankan

### Di komputer sendiri

```bash
git clone https://github.com/Akhdaa/Simple-Discord-Music-Bot.git
cd Simple-Discord-Music-Bot
cp .env.example .env     # lalu isi DISCORD_TOKEN di file .env
npm install
npm start
```

Kalau muncul `Bot online sebagai ...`, bot sudah jalan. Slash command didaftarkan otomatis tiap bot nyala. Kalau belum muncul di Discord, refresh dulu dengan Ctrl+R.

Di Windows bisa juga klik `bot_start.bat`: dia menjalankan `npm install` kalau belum pernah, lalu `npm start`. File `.env` tetap harus dibuat dulu.

`npm run dev` menjalankan bot dan restart otomatis tiap ada file yang berubah.

### Di GitHub Codespaces

Buka repo, klik **Code → Codespaces → Create codespace on main**. Dependensi terpasang sendiri. Setelah itu buat `.env` seperti di atas dan jalankan `npm start`.

Bot ikut mati begitu codespace berhenti, jadi cara ini cocok buat coba-coba, bukan buat jalan terus.

## Command

| Slash | Prefix | Fungsi |
|---|---|---|
| `/play`, `/p` | `!play`, `!p` | Putar lagu dari judul atau link YouTube |
| `/search`, `/sc` | `!search`, `!sc` | Cari lagu lalu pilih dari hasilnya |
| `/skip`, `/s` | `!skip`, `!s` | Lewati lagu yang sedang diputar |
| `/pause` | `!pause` | Jeda |
| `/resume`, `/r` | `!resume`, `!r` | Lanjutkan |
| `/stop` | `!stop` | Berhenti dan bot keluar dari voice channel |
| `/loop`, `/l` | `!loop`, `!l` | Ulang lagu yang sedang diputar |
| `/autoplay`, `/ap` | `!autoplay`, `!ap` | Putar lagu terkait kalau antrian habis |
| `/queue`, `/q` | `!queue`, `!q` | Lihat antrian |
| `/clear` | `!clear` | Kosongkan antrian |
| `/nowplaying`, `/np` | `!nowplaying`, `!np` | Lagu yang sedang diputar |
| `/controls`, `/c`, `/ct` | | Panel kontrol dengan tombol |
| `/help`, `/h` | `!help`, `!h` | Daftar command |
| `/aliases` | `!aliases` | Semua shortcut |
| `/changelog` | | Riwayat versi |

Contoh:

```
/play lofi hip hop
!p https://www.youtube.com/watch?v=xxxxx
```

## Cookies YouTube (opsional)

Kalau YouTube minta login atau menolak dengan pesan "confirm you're not a bot", taruh cookies di `src/cookies.txt`. Isinya bisa file format Netscape (hasil ekspor ekstensi cookies.txt) atau string header `Cookie` mentah (`nama=nilai; nama2=nilai2`). Format kedua dikonversi bot sendiri.

File itu sudah masuk `.gitignore`, jangan di-commit. Lebih aman pakai akun cadangan, bukan akun utama.

## Catatan

- Streaming audio dari YouTube melanggar ToS YouTube. Pakai di server pribadi.
- Kalau suara tidak keluar, cek bot tidak di-deafen di server dan punya izin Connect dan Speak di voice channel itu.
- Kalau `npm install` mengeluh soal versi Node, update Node dulu. `@discordjs/voice` versi 0.19 minta 22.12 ke atas.
