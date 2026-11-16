# Northumberland Home, Garden & Leisure Show: Vendor Booking

Vendor booking page for the 2027 show (April 9–11, 2027, Cobourg Community Centre).
Hosted by myFM 93.3, Classic Rock 107.9 and 100.9 WOW FM. Presented by the Ryan Huffman Real Estate Team.

The page includes:

- an interactive 3D floor plan of the gymnasium, with vendors and multi-booth spaces
- a flip-through 2026 Guide Book, with a full-size reading view
- the 2027 Guide Book ad offer ($299 home show special, payment due February 26, 2027)
- the booth renewal form, which sends through Web3Forms

It's a plain static site with no build step.

```
index.html      the whole page: styles, markup and script
assets/         station and presenter logos
guide/          guide book pages (pN.jpg for the flip book, pN-full.jpg for the reading view)
.nojekyll       tells GitHub Pages to serve the files as they are
```

## Put it on GitHub Pages

1. Create a new repository on GitHub, for example `home-show-vendors`.
2. Upload everything in this folder, including the hidden `.nojekyll` file. You can drag the files onto the repository page, or push them with git:
   ```
   git init
   git add .
   git commit -m "Vendor booking page"
   git branch -M main
   git remote add origin https://github.com/YOUR-ACCOUNT/home-show-vendors.git
   git push -u origin main
   ```
3. In the repository, go to **Settings → Pages**. Under **Build and deployment**, choose **Deploy from a branch**, select **main** and **/ (root)**, then click **Save**.
4. After a minute or two, the site is live at `https://YOUR-ACCOUNT.github.io/home-show-vendors/`.

To use your own domain (for example `vendors.northumberlanddaily.ca`), add it under **Settings → Pages → Custom domain** and point a CNAME record at `YOUR-ACCOUNT.github.io`.

## Turn on automatic form sending (Web3Forms)

1. Go to <https://web3forms.com>, click **Create your Access Key** and enter `tommyw@mbcmedia.ca`. The key arrives by email.
2. Open `index.html` and find this line near the top of the script:
   ```js
   const WEB3FORMS_KEY = "";
   ```
3. Paste the key between the quotes, then commit the change.

Each renewal request then lands in Tommy's inbox. The email includes the business name, contact name, phone, email and guide book choice, and the vendor's address is set as the reply-to. The free plan allows 250 submissions a month.

If the key is empty, or a send fails, the form falls back to an "Open in my email app" button and a "Copy request" button, so vendors can always get a request through.

## Common updates

All of these are in the script section of `index.html`.

| What | Where |
|---|---|
| Vendors on the floor plan | The `VENDORS` list. Each entry looks like `"B07": {"status": "Booked", "name": "Business Name"}`. Status is `Booked` or `Held for renewal`. Booths not listed show as open. Businesses in touching booths are shown as one larger space automatically. |
| Facebook page link | `FACEBOOK_URL` |
| Booth payment deadline | The countdown uses `Date.UTC(2026,11,23,22,0,0)`, which is December 23, 2026 at 5 PM Toronto time. The deadline text appears in the hero bar, the steps, the warning box and the form. |
| Guide book pages | Replace the images in `guide/`, keeping the same file names. |

The vendor list comes from the "Home Show 2027 Booth Assignments" Google Sheet.
