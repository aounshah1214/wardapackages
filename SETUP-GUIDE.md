# Warda Packages — Website & Admin Panel Guide

- **Hosting:** GitHub Pages (free)
- **Admin Panel:** `https://wardapackages.com/admin` (email + password login)
- **Database:** none. Products are stored in `data/products.json` and store details in `data/settings.json`.

The only running cost is the domain.

---

## What's in this repository

| File / Folder | Purpose |
|---|---|
| `index.html` | The website |
| `data/products.json` | Products (edited from the Admin Panel) |
| `data/settings.json` | Phone, WhatsApp, email, address, delivery time, bank details, social links (edited from the Admin Panel) |
| `admin/index.html` | The Admin Panel |
| `admin/auth.json` | Created during setup. Holds the encrypted login. It does **not** contain the password. |
| `images/` | Logo and hero image. Product pictures uploaded from the Admin Panel go into `images/products/`. |
| `CNAME` | Tells GitHub Pages to use `wardapackages.com` |

---

## 1. Turn on GitHub Pages

1. Open **https://github.com/aounshah1214/wardapackages/settings/pages**
2. Under **Build and deployment → Branch**, choose `main` and `/ (root)`, then **Save**.
3. Under **Custom domain**, enter `wardapackages.com` and **Save**.

## 2. Point the domain to GitHub (DNS)

At your domain registrar (GoDaddy, Namecheap, Hostinger, etc.), open the **DNS settings** for `wardapackages.com`:

1. **Delete** the existing **A** records for `@`.
2. Add these four **A** records (Host/Name: `@`):

   | Type | Name | Value |
   |---|---|---|
   | A | `@` | `185.199.108.153` |
   | A | `@` | `185.199.109.153` |
   | A | `@` | `185.199.110.153` |
   | A | `@` | `185.199.111.153` |

3. Add one **CNAME** record: Name `www` → Value `aounshah1214.github.io`

DNS changes can take from 10 minutes up to 24 hours. Once GitHub Pages shows the domain as verified, tick **Enforce HTTPS** on the same Pages settings screen. The Admin Panel only works over HTTPS.

## 3. Create a GitHub token (one time, for setup only)

1. Open **https://github.com/settings/personal-access-tokens/new**
2. **Token name:** `warda-admin`
3. **Expiration:** the longest available
4. **Repository access:** *Only select repositories* → `wardapackages`
5. **Permissions → Repository permissions → Contents:** *Read and write*
6. Click **Generate token** and copy it.

> Treat the token like a password. Never share it.

## 4. Set up the Admin login (one time)

1. Open **https://wardapackages.com/admin** (or `http://localhost:8000/admin/` when testing locally).
2. On the **Admin Panel Setup** screen:
   - **Admin Email:** `wardapackages8@gmail.com` (pre-filled)
   - **Password / Confirm Password:** choose the admin password
   - **GitHub Repository:** `aounshah1214/wardapackages` (pre-filled)
   - **GitHub Token:** paste the token from step 3
3. Click **Save & Log In**.

From now on, log in with **email + password only**. The token is stored encrypted with the password.

---

## Using the Admin Panel

### Products tab

| Task | How |
|---|---|
| Add a product | **+ Add Product** |
| Add / change a picture | Open the product → **Choose Picture** (large photos are resized automatically) |
| Edit name, price, description | ✎ button |
| Show a discount | Fill in **Old Price** (higher than the price). It shows crossed out. |
| Hide a product without deleting it | Turn its switch off |
| Delete a product | 🗑 button |
| Change the order on the website | ↑ ↓ buttons |
| Change the section heading | "Products Section" at the top |

### Store Settings tab

| Setting | Where it appears on the website |
|---|---|
| Phone Number | Footer, customer order page |
| WhatsApp Number | WhatsApp button in the footer |
| Email | Footer |
| Address | Footer (leave empty to hide) |
| Delivery Time | Footer, customer order page |
| Bank Name / Account Number / Account Holder | Checkout, when the customer picks Bank Transfer |
| Instagram / Facebook / TikTok | Social icons in the footer (leave empty to hide) |

After making changes, click **Save & Publish** at the bottom. Changes go live in 1–2 minutes.

### Account

**Account** (top right) lets you change the admin email or password.

---

## Forgot the password?

On the login screen, click **Forgot password? Reset login**, create a new GitHub token (step 3) and set a new password. A password can't be reset without a token. That is what keeps the panel secure.

## Customer orders

Orders are still sent by email through EmailJS, as before.

## Testing locally

```
python -m http.server 8000
```

Then open `http://localhost:8000` (website) and `http://localhost:8000/admin/` (admin). Admin changes are saved to GitHub. To see them in your local copy, pull the latest changes (VS Code: **Source Control → Sync Changes**, or `git pull`).

## Troubleshooting

- **"HTTPS required":** enable **Enforce HTTPS** in GitHub Pages and open the site with `https://`.
- **"Repository not found":** check the repository name and that the token has access to it.
- **"Token is invalid or has expired":** use **Forgot password? Reset login** with a new token.
- **Change not showing:** wait 2 minutes and hard-refresh (Ctrl+F5). Deploy progress is in the repository's **Actions** tab.
