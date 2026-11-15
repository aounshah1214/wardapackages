# Warda Packages — Admin Panel Setup (100% Free)

Hosting: **GitHub Pages** (free) · Admin Panel: custom, **email + password** login · Database: **koi nahi** (products `data/products.json` mein save hote hain)

Sirf domain ka kharcha (jo pehle se hai). Baqi sab free.

---

## Folder mein kya hai

| File / Folder | Kaam |
|---|---|
| `index.html` | Website (products `data/products.json` se load hote hain) |
| `data/products.json` | Saare products — Admin Panel yahi file update karta hai |
| `admin/index.html` | Admin Panel → `wardapackages.com/admin` |
| `admin/auth.json` | Setup ke baad khud ban jati hai (encrypted login). Is mein password nahi hota. |
| `images/` | Logo, hero image. Admin se upload hone wali pictures `images/products/` mein jayengi |
| `CNAME` | GitHub ko batata hai ke domain `wardapackages.com` hai |

---

## Step 1 — GitHub repo banayein

1. https://github.com par account banayein / login karein.
2. **New repository** → naam: `wardapackages` → **Public** (free GitHub Pages ke liye zaroori) → Create.

## Step 2 — Files upload karein

Repo page par **Add file → Upload files** → is folder ki **saari files aur folders** drag karein (zip khud nahi, uske andar ka saman) → **Commit changes**.

## Step 3 — GitHub Pages on karein

1. Repo → **Settings → Pages**
2. Source: **Deploy from a branch** → Branch: `main` / `/ (root)` → Save
3. **Custom domain**: `wardapackages.com` → Save
4. DNS set hone ke baad **Enforce HTTPS** tick karein (admin panel sirf HTTPS par chalta hai).

## Step 4 — Domain ko GitHub par point karein (DNS)

Domain registrar (GoDaddy / Namecheap / Hostinger etc.) ki **DNS settings** mein:

| Type | Name / Host | Value |
|---|---|---|
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| CNAME | `www` | `YOUR-GITHUB-USERNAME.github.io` |

- `@` ke **purane A records delete** karein.
- DNS update mein 10 minute se 24 ghante lag sakte hain.

## Step 5 — GitHub Token banayein (sirf setup ke waqt, ek dafa)

1. GitHub → profile photo → **Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token**
2. Name: `warda-admin` · Expiration: sab se lambi jo mile (expire hone par Step 6 dobara)
3. **Repository access → Only select repositories →** `wardapackages`
4. **Permissions → Repository permissions → Contents: Read and write**
5. Generate → token copy karein.

## Step 6 — Admin login set karein (ek dafa)

1. Kholein: **https://wardapackages.com/admin** → "Admin Panel Setup" screen aayegi.
2. Bharein:
   - **Email:** `wardapackages8@gmail.com` (pehle se bhara hua)
   - **Password** + **Password dobara:** apna admin password
   - **GitHub Repo:** `apna-username/wardapackages`
   - **GitHub Token:** Step 5 wala token
3. **Save & Login** → bas. Token password se encrypt ho kar save ho gaya.

**Iske baad har dafa login sirf Email + Password se.** Token dobara nahi chahiye.

## Step 7 — Admin Panel use karna

| Kaam | Kaise |
|---|---|
| Naya product | **+ Add Product** |
| Picture | Product kholein → **Picture choose karein** (badi photo khud chhoti ho jati hai) |
| Naam / price / description edit | ✎ button |
| Discount dikhana | **Old Price** bharein (price se zyada) — website par kata hua dikhega |
| Hide (delete kiye baghair) | Green switch OFF |
| Delete | 🗑 button |
| Order / sequence | ↑ ↓ buttons |
| Section heading badalna | Upar "Products Section" |
| Email / password badalna | **Settings** |

Changes ke baad neeche **Save & Publish** dabayein → 1–2 minute mein website par live.

Phone par bhi chalta hai — wohi link, wohi email/password.

---

## Password bhool gaye?

Login screen par **"Password bhool gaye? / Setup dobara karein"** → naya GitHub token (Step 5) + naya password → Save. Bina token ke password reset nahi ho sakta — yahi security hai.

## Security notes

- Password kahin save nahi hota. `auth.json` mein sirf encrypted token hai jo sahi email + password ke baghair khul nahi sakta.
- Mazboot password rakhein aur ise kisi aur website par use na karein.
- Token kisi ko na dein, WhatsApp par na bhejein.

## Customer Orders

Checkout pehle ki tarah EmailJS se email par order bhejta hai — koi change nahi.

## Agar kuch kaam na kare

- **"HTTPS chahiye":** GitHub Pages → Enforce HTTPS on karein, `https://` se kholein.
- **"Repo nahi mila":** repo ka naam check karein, aur token mein yehi repo select ho.
- **"Token expire/ghalat":** Setup dobara karein (naya token).
- **Change live nahi hua:** 2 minute ruk kar Ctrl+F5. Repo → **Actions** tab mein deploy status dikhta hai.
