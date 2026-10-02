DORAEMON POCKET VAULT (PWA)

DEPLOY
  Drag this folder into vercel.com/new (or run `vercel` in it). No build step.
  GitHub Pages works too, but GitHub Pages cannot send the headers in
  vercel.json, so make sure manifest.webmanifest is served as
  application/manifest+json or Chrome will only offer a shortcut.

INSTALL AS AN APP (NOT A SHORTCUT)
  1. Open the deployed https:// URL in Chrome (Edge or Samsung Internet also work).
  2. Tap the gold "INSTALL APP" button at the bottom of the page, or use the
     browser menu > "Install app".
  3. Confirm. The icon opens with no browser address bar, splash screen, and
     your own window.

  Choose "Install app", never "Add to Home screen". "Add to Home screen" creates a
  shortcut that still opens inside the browser.

  iOS Safari never shows an install button. Tap the INSTALL APP bar in the app
  for the Share > Add to Home Screen steps. That still launches standalone.

REQUIRED FOR INSTALL TO WORK
  - Must be served over HTTPS. A plain http:// LAN address (like
    http://192.168.1.5:3000) can only ever create a shortcut. Use a tunnel or
    deploy.
  - Must be the deployed origin, not a local file. Opening index.html by
    double-clicking (file://) will not install.
  - localhost is treated as secure, so http://localhost:3000 does work locally.

WHAT WAS CHANGED FOR INSTALL
  manifest.webmanifest  added id, display_override, orientation, lang, dir,
                        categories, launch_handler, and an explicit
                        "purpose":"any" on the standard icons. Chrome requires a
                        parseable manifest before it offers a real install.
  vercel.json           forces Content-Type: application/manifest+json on the
                        manifest, text/javascript on sw.js, and
                        Service-Worker-Allowed: /.
  sw.js                 cache bumped to dpv-v2 and now precaches
                        icon-maskable-512.png so the installed icon works
                        offline.
  index.html            added mobile-web-app-capable,
                        apple-mobile-web-app-status-bar-style, a
                        beforeinstallprompt handler with a gold "INSTALL APP"
                        button, an appinstalled confirmation, a manual
                        "HOW TO INSTALL" sheet for iOS, and display-mode
                        detection so the bar hides once installed.

NOTE ON THE MASKABLE ICON
  icon-512.png and icon-maskable-512.png are currently identical, so the
  maskable one has no safe-zone padding and Android may clip the artwork on
  adaptive-icon masks. Regenerate icon-maskable-512.png with the logo scaled to
  about 60 percent on a solid #0096e0 background to fix it.
