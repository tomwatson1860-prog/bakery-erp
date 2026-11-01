# Bakery Project ERP

Website: https://tomwatson1860-prog.github.io/bakery-erp/

The website copy of the Bakery Project ERP: sales orders, bake sheets, purchasing, inventory, recipes and costing, and CG02-style specifications.

The site asks for an access code. The ERP and its records are stored in `index.html` in encrypted form (AES-256-GCM, with the key derived from the access code) and are decrypted in the visitor's browser, so this repository holds no readable copy of them. Ask the owner for the code.

Records start from a snapshot of the ERP in Claude (November 1, 2026) and are saved in each visitor's browser. **Setup › Export / Import** moves records between browsers and back into the Claude version. Asking Claude questions in Query needs the Claude version; search works here.

## On a phone

In Safari on an iPhone, tap Share, then Add to Home Screen. The site gets its own app icon (`icons/`) and opens full-screen like an app (`manifest.webmanifest`, and the tags in `tools/head.html`, which the build adds to both the code screen and the unlocked ERP). The home-screen app keeps its own records, separate from Safari's.

## Updating the site

```
ACCESS_CODE=<code> node tools/build_site.js <ERP page app.html> - index.html
ACCESS_CODE=<code> NODE_PATH=$(npm root -g) node tools/check_site.js index.html - --expect "#nav button"
```

`build_site.js` applies the safety rules below, encrypts the page with the code screen in `tools/gate.html` and checks its own output. `check_site.js` opens the result in a headless browser and only passes when a wrong code is refused, the right code opens the ERP, nothing loads from other servers, the home-screen icon and manifest are in place, and an altered copy of the fingerprinted font file is refused. The access code is never stored in this repository.

## Safety

- Everything the page needs is served from this site. The fonts (Bricolage Grotesque, IBM Plex Sans and IBM Plex Mono, from Fontsource) are in `fonts/` with their licences, and `fonts/fonts.css` is fingerprinted (Subresource Integrity, SHA-384), so a browser refuses an altered copy.
- The code screen and the ERP set a Content Security Policy that blocks loading anything from other servers, and send no referrer when visitors follow a link out.
- No cookies, analytics or forms that send data; the access code is checked in the visitor's browser and never leaves it.
- The home-screen icon and app manifest are files on this site too; the build stops if they point anywhere else.
