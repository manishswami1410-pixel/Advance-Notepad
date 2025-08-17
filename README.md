{
  "name": "Advanced Notepad",
  "short_name": "Notepad",
  "start_url": ".",
  "display": "standalone",
  "background_color": "#0f172a",
  "theme_color": "#0f172a",
  "icons": [
    {
      "src": "/icons/icon-192.png",
      "sizes": "192x192",
      "type": "image/png"
    },
    {
      "src": "/icons/icon-512.png",
      "sizes": "512x512",
      "type": "image/png"
    }
  ]
self.addEventListener("install", (event) => {
  event.waitUntil(
    caches.open("notepad-cache").then((cache) => {
      return cache.addAll([
        "/",
        "/index.html",
        "/manifest.json",
        "/icons/icon-192.png",
        "/icons/icon-512.png",
      ]);
    })
  );
});

self.addEventListener("fetch", (event) => {
  event.respondWith(
    caches.match(event.request).then((response) => {
      return response || fetch(event.request);
    })
  );
});
if ("serviceWorker" in navigator) {
  window.addEventListener("load", () => {
    navigator.serviceWorker
      .register("/sw.js")
      .then(() => console.log("Service Worker Registered"));
  });
}
<meta name="theme-color" content="#0f172a" />
<!-- Android Chrome theme -->
<meta name="theme-color" content="#0f172a" />

<!-- iOS Safari -->
<meta name="apple-mobile-web-app-capable" content="yes" />
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />

<!-- Windows Edge -->
<meta name="msapplication-navbutton-color" content="#0f172a" />
<!-- General viewport -->
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1" />
<link rel="icon" href="/icons/favicon-32.png" sizes="32x32" type="image/png" />
<link rel="icon" href="/icons/favicon-192.png" sizes="192x192" type="image/png" />
<link rel="apple-touch-icon" href="/icons/apple-icon-180.png" />
<link rel="manifest" href="/manifest.json" />
public/
│── index.html
│── manifest.json
│── browserconfig.xml
│── icons/
│     ├── favicon-32.png
│     ├── favicon-192.png
│     ├── icon-192.png
│     ├── icon-512.png
│     ├── apple-icon-180.png
│     └── maskable-icon.png
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Advanced Notepad</title>

    <!-- Viewport -->
    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1" />

    <!-- Theme Colors -->
    <meta name="theme-color" content="#0f172a" />
    <meta name="apple-mobile-web-app-capable" content="yes" />
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
    <meta name="apple-mobile-web-app-title" content="Advanced Notepad" />
    <meta name="msapplication-TileColor" content="#0f172a" />
    <meta name="msapplication-config" content="/browserconfig.xml" />

    <!-- Icons -->
    <link rel="icon" href="/icons/favicon-32.png" sizes="32x32" type="image/png" />
    <link rel="icon" href="/icons/favicon-192.png" sizes="192x192" type="image/png" />
    <link rel="apple-touch-icon" href="/icons/apple-icon-180.png" />

    <!-- Manifest -->
    <link rel="manifest" href="/manifest.json" />
  </head>
  <body>
    <div id="root"></div>
  </body>
</html>
{
  "name": "Advanced Notepad",
  "short_name": "Notepad",
  "start_url": ".",
  "display": "standalone",
  "background_color": "#0f172a",
  "theme_color": "#0f172a",
  "icons": [
    {
      "src": "/icons/icon-192.png",
      "sizes": "192x192",
      "type": "image/png"
    },
    {
      "src": "/icons/icon-512.png",
      "sizes": "512x512",
      "type": "image/png"
    },
    {
      "src": "/icons/maskable-icon.png",
      "sizes": "512x512",
      "type": "image/png",
      "purpose": "maskable"
    }
  ]
}
<?xml version="1.0" encoding="utf-8"?>
<browserconfig>
  <msapplication>
    <tile>
      <square150x150logo src="/icons/icon-192.png"/>
      <TileColor>#0f172a</TileColor>
    </tile>
  </msapplication>
</browserconfig>
npm install --save-dev pwa-asset-generator
project-root/
│── public/
│    ├── index.html
│    ├── manifest.json
│    └── icons/   (auto-generated icons यहाँ आएंगे)
│── logo.png       (master logo, 1024x1024 recommended)
│── generate-icons.js
// generate-icons.js
import { generateImages, generateFavicon } from 'pwa-asset-generator';
import fs from 'fs';

const masterLogo = 'logo.png';
const outputDir = './public/icons';
const manifestPath = './public/manifest.json';

(async () => {
  try {
    console.log('🚀 Generating PWA icons...');

    // Generate all splash screens + icons
    await generateImages(masterLogo, outputDir, {
      background: '#0f172a',
      splashOnly: false,
      manifest: manifestPath,
      pathOverride: '/icons/',
      log: true,
    });

    // Generate favicon.ico
    await generateFavicon(masterLogo, outputDir);

    console.log('✅ All icons & manifest updated successfully!');
  } catch (err) {
    console.error('❌ Error generating icons:', err);
  }
})();
"scripts": {
  "generate:icons": "node generate-icons.js"
}
npm run generate:icons
