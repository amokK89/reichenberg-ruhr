# Deployment: Cloudflare Pages

## Erstmalige Einrichtung

### 1. GitHub-Repo erstellen
- Repository-Name: `reichenberg-ruhr`
- Sichtbarkeit: Private (Domain-Code muss nicht öffentlich sein)
- Dieses Verzeichnis pushen

### 2. Cloudflare Pages verknüpfen
1. Cloudflare Dashboard → Pages → "Create a project"
2. "Connect to Git" → GitHub-Repo `reichenberg-ruhr` auswählen
3. Build-Einstellungen:
   - **Build command:** `npm run build`
   - **Build output directory:** `dist`
   - **Node.js version:** 18 (oder 20)
4. "Save and Deploy"

### 3. Domain konfigurieren
In Cloudflare DNS für `reichenberg.ruhr`:
- Alten XING-Redirect-Record löschen
- Neuen CNAME-Record anlegen:
  - Name: `@` (oder `reichenberg.ruhr`)
  - Target: `reichenberg-ruhr.pages.dev`
  - Proxy: **An** (oranges Wolken-Icon)

HTTPS wird automatisch von Cloudflare bereitgestellt.

### 4. E-Mail-Routing (optional)
Cloudflare Dashboard → Email Routing → `dennis@reichenberg.ruhr` → Weiterleitung an Dennis' Postfach.

---

## Laufende Updates

```bash
git add .
git commit -m "Update: [Beschreibung der Änderung]"
git push
```

Cloudflare Pages deployt automatisch nach jedem Push auf `main`.

---

## Google Search Console

1. https://search.google.com/search-console → "Property hinzufügen"
2. Domain-Property: `reichenberg.ruhr`
3. TXT-Verifikationsrecord in Cloudflare DNS eintragen
4. Nach Verifikation: Sitemap einreichen → `https://reichenberg.ruhr/sitemap-index.xml`

---

## Inhalte aktualisieren (Checkliste vor Go-Live)

- [ ] `src/components/Hero.astro` — `hasProfileImage` auf `true` setzen, sobald `public/profile.jpg` vorhanden
- [ ] `src/components/TechStack.astro` — Platzhalter-Stack durch Dennis' echten Stack ersetzen
- [ ] `src/pages/index.astro` — `og:image` Meta-Tag mit Profilbild-URL befüllen
- [ ] `public/profile.jpg` — Profilbild (Dennis liefert Foto) einpflegen
