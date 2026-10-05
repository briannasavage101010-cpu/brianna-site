# Getting briannasavage.nyc live

Two things need an account login, which only you can do. Everything else is
already done — the site is built, committed to git, and the `CNAME` file
already says `briannasavage.nyc`.

---

## The fastest route: Netlify (about 10 minutes)

### Step 1 — put the site online

1. Go to **https://app.netlify.com/drop**
2. Open a Finder window and go to your **home folder** (not Desktop):
   press `Command + Shift + H`
3. Drag the **`brianna-site`** folder onto the Netlify page.
4. It goes live straight away on a temporary address like
   `glittering-marzipan-1a2b3c.netlify.app`. That link already works — you can
   send it to people today.
5. Netlify will ask you to sign up to keep it. Do that (free).

### Step 2 — point your domain at it

1. In Netlify: **Domain management → Add a domain** → type `briannasavage.nyc`
2. Netlify asks "Add DNS records" or "Use Netlify DNS". **Choose "Add DNS
   records"** — do NOT choose Netlify DNS.

   > This matters. You bought Microsoft 365 email on this domain. Moving your
   > whole DNS to Netlify would break your email unless the MX records get
   > copied across perfectly. Keeping DNS at GoDaddy avoids that risk entirely.

3. Netlify shows you the records it wants. They'll look like the table below.

### Step 3 — add those records at GoDaddy

1. Sign in at **godaddy.com** → **My Products** → next to `briannasavage.nyc`
   click **DNS**.
2. Make these changes, and **nothing else**:

| Action | Type | Name | Value |
|---|---|---|---|
| **Edit** the existing one | A | `@` | the IP Netlify gives you |
| **Edit** the existing one | CNAME | `www` | the `.netlify.app` address Netlify gives you |

3. **Do not touch anything of type MX, TXT, or SRV.** Those are your Microsoft
   365 email. If you delete them your email stops working.
4. Save. DNS usually updates within an hour, sometimes up to a day.
5. Back in Netlify, click **Verify DNS configuration**. Once it's happy it adds
   the HTTPS padlock automatically.

### Updating it later
Change the files, then drag the folder onto Netlify again. Or connect the git
repo so it updates on every push.

---

## Alternative: GitHub Pages

Your git credentials already work on this machine, so this is also easy — but
it's three steps instead of one, and the DNS is slightly fiddlier.

1. Go to **https://github.com/new**. Repository name: `brianna-site`.
   Set it to **Public**. Do **not** tick "Add a README".
2. Then run this in Terminal:

```bash
cd ~/brianna-site && git remote add origin https://github.com/briannasavage101010-cpu/brianna-site.git && git push -u origin main
```

3. On GitHub: **Settings → Pages →** under "Branch" pick `main` / `root` → Save.
4. In the same Pages screen, "Custom domain" should already show
   `briannasavage.nyc` (the `CNAME` file sets it). Tick **Enforce HTTPS** once
   it becomes available.
5. At GoDaddy DNS, set these — again, **leave MX/TXT/SRV alone**:

| Type | Name | Value |
|---|---|---|
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| CNAME | `www` | `briannasavage101010-cpu.github.io` |

GoDaddy starts with one parked `A` record on `@` — edit that one to the first
IP, then add the other three.

**Updating it later:**

```bash
cd ~/brianna-site && git add -A && git commit -m "update" && git push
```

---

## Your email address

You bought **Microsoft 365 Email Essentials** with the domain, so
`hello@briannasavage.nyc` can be a real mailbox. Set it up at GoDaddy under
**My Products → Email**. Create the address `hello`.

The site already uses `hello@briannasavage.nyc` on the contact page and in the
enquiry form. If you'd rather use a different name (`brianna@`, `studio@`),
change it everywhere at once:

```bash
cd ~/brianna-site && grep -rl "hello@briannasavage.nyc" . --include="*.html" | xargs sed -i '' 's/hello@briannasavage.nyc/NEW@briannasavage.nyc/g'
```

---

## Checklist

- [ ] Site online (Netlify drop, or GitHub Pages)
- [ ] `briannasavage.nyc` DNS pointed at it
- [ ] HTTPS padlock showing
- [ ] `hello@briannasavage.nyc` mailbox created in Microsoft 365
- [ ] Sent yourself a test enquiry through the form on `/websites/`
