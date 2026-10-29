# PrankPay

Landing page, playable demo and iOS project for **PrankPay**, a joke wallet app that "charges" your friends a ridiculous amount, then reveals the prank. No real payments, no data saved.

## Structure

```
.
├── index.html             Landing page
├── css/styles.css         Landing page styles (light and dark mode)
├── icons/                 App and social-sharing images
├── app/
│   ├── index.html         PrankPay app, embedded on the landing page
│   └── manifest.webmanifest
├── ios/                   Native iOS wrapper (Xcode project source)
│   ├── project.yml        XcodeGen spec
│   └── PrankPay/          Swift sources, assets, bundled web app
├── robots.txt
├── sitemap.xml
└── README.md
```

## Run the site locally

```
python3 -m http.server 8000
```

Visit http://localhost:8000.

## Getting it onto iPhones

iOS does not let people install an app file (.ipa) from a website. There are two real routes:

**1. Add to Home Screen (works today, free).** Host the site over HTTPS, open `/app/` in Safari, tap Share, then "Add to Home Screen". The landing page already explains this to visitors.

**2. A real app (App Store or TestFlight).** Needs a Mac with Xcode and an Apple Developer account ($99/year).

```
brew install xcodegen
cd ios
xcodegen                 # creates PrankPay.xcodeproj
open PrankPay.xcodeproj
```

In Xcode: select the PrankPay target, set your Team and a unique Bundle Identifier under Signing & Capabilities, then pick your iPhone and press Run. To distribute, choose Product > Archive, then upload to App Store Connect and release via TestFlight (public link) or the App Store. Add that link to the landing page's "Get" button.

When you change `app/index.html`, copy it to `ios/PrankPay/web/index.html` too.

### Known limits inside iOS

The app's "Scan NFC tag" and vibration use browser features iOS web views don't support (Web NFC and `navigator.vibrate`). Everything else works. Real NFC would need a native CoreNFC bridge in Swift.

## Customise

- Colors and fonts: variables at the top of `css/styles.css`.
- Copy: `index.html`.
- The prank defaults: `app/index.html`, or the gear icon in the running app.

## Deploy

Static site, no build step. Upload to GitHub Pages, Netlify, Vercel or Cloudflare Pages.

## SEO and sharing

The landing page includes a descriptive title and search description, a
canonical URL, Open Graph/Twitter sharing metadata, a social preview image,
and WebApplication structured data. The standalone simulator is marked
`noindex` so search results focus on the landing page. `robots.txt` and
`sitemap.xml` use the GitHub Pages URL:
https://master01x.github.io/ApplePay-Prank/

If you change the deployment domain, update those URLs in `index.html`,
`robots.txt`, and `sitemap.xml`.

## Disclaimer

For entertainment only. Not affiliated with Apple Pay or any payment provider.
