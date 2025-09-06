# Catatan Kuota (Static)

Aplikasi pencatatan jualan kuota **offline/online** berbasis HTML + JS (tanpa backend). Sudah termasuk **Pagination**, **Export/Import**, dan **Login sederhana** (front‑end).

## Struktur
```
/ (root)
├─ index.html   # aplikasi utama (dengan guard login)
├─ login.html   # halaman masuk (hash SHA‑256 password)
└─ README.md
```

> **Keamanan**: Login ini hanya di sisi klien. Untuk data sensitif, gunakan autentikasi server (mis. Next.js + Vercel Auth) atau proteksi dasar (.htaccess) di hosting lain.

---

## Deploy ke GitHub Pages
1. Buat repo baru di GitHub (mis. `kuota-ledger`).
2. Upload **index.html**, **login.html**, dan **README.md** ke branch `main`.
3. Buka **Settings → Pages**.
4. Di **Build and deployment → Source**, pilih **Deploy from a branch**.
5. Pilih `Branch: main` dan `Folder: /(root)` → **Save**.
6. Tunggu ~1–2 menit. Situsmu akan muncul di:
   - `https://USERNAME.github.io/REPO/`
7. Akses pertama kali: `https://USERNAME.github.io/REPO/login.html`

## Deploy ke Vercel
1. Buat akun di vercel.com → **New Project**.
2. **Import Git Repository** repo yang berisi file di atas.
3. Framework: **Other**. Build command **kosong**, Output directory **root** (`/`).
4. Deploy → URL akan diberikan, mis. `https://kuota-ledger.vercel.app`.

### Tips Vercel
- Bisa tambah **Custom Domain** gratis dari Vercel.
- Bila ingin autentikasi lebih aman, gunakan Next.js + Middleware untuk proteksi route, atau Vercel Password Protection (butuh Pro). 

---

## Ganti password
1. Buka `login.html`, ubah konstanta `PASS_HASH` ke SHA‑256 dari password barumu.
2. Cara membuat SHA‑256:
   - Sementara, ketik password di field login, lalu di DevTools jalankan:
   ```js
   await (async s=>{const e=new TextEncoder().encode(s);const d=await crypto.subtle.digest('SHA-256',e);console.log(Array.from(new Uint8Array(d)).map(b=>b.toString(16).padStart(2,'0')).join(''))})('PASSWORD_BARU')
   ```
   - Salin hash-nya dan tempelkan ke `PASS_HASH`.

## Logout
- Klik tombol **Logout** di kanan atas `index.html`.

## Backup
- Gunakan **Export JSON** untuk restore di aplikasi ini, dan **Export CSV** untuk dibuka di Excel.
