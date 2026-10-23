# MFS Fachkonferenz – Landingpage

Statische Seite, gehostet auf Vercel, ausgeliefert unter
https://www.management-forum.de/fachkonferenz-bau-und-betrieb-von-senioren-und-pflegeeinrichtungen/

## Struktur
- `fachkonferenz-bau-und-betrieb-von-senioren-und-pflegeeinrichtungen/index.html` – die Seite
- `…/support.js` – Laufzeit (nicht bearbeiten)
- `…/assets/` – Bilder, Video, Logos, Porträts
- `vercel.json` – Weiterleitung, Caching, Header

## Deployment
1. Inhalt dieses Ordners in ein GitHub-Repo pushen.
2. In Vercel: New Project → Repo importieren → Framework „Other“, kein Build-Command, Output-Directory leer.
3. Test: https://<projekt>.vercel.app/fachkonferenz-bau-und-betrieb-von-senioren-und-pflegeeinrichtungen/
4. IT von management-forum.de richtet Reverse Proxy ein:

nginx:
```
location /fachkonferenz-bau-und-betrieb-von-senioren-und-pflegeeinrichtungen/ {
  proxy_pass https://<projekt>.vercel.app/fachkonferenz-bau-und-betrieb-von-senioren-und-pflegeeinrichtungen/;
  proxy_set_header Host <projekt>.vercel.app;
  proxy_ssl_server_name on;
}
```

Apache:
```
SSLProxyEngine On
ProxyPass        /fachkonferenz-bau-und-betrieb-von-senioren-und-pflegeeinrichtungen/ https://<projekt>.vercel.app/fachkonferenz-bau-und-betrieb-von-senioren-und-pflegeeinrichtungen/
ProxyPassReverse /fachkonferenz-bau-und-betrieb-von-senioren-und-pflegeeinrichtungen/ https://<projekt>.vercel.app/fachkonferenz-bau-und-betrieb-von-senioren-und-pflegeeinrichtungen/
```

## Tracking
- Google Tag Manager **GTM-M6NMLGH** wird im `<head>` geladen. Vorher setzt die Seite Consent Mode v2 (alles „denied“) und `dataLayer.push({ lp_id: 'LP_Senioren' })`.
- GA4 **G-ZF9DT30DB7** wird zusätzlich direkt per gtag geladen, erst nach Zustimmung im Cookie-Banner (localStorage-Schlüssel `mfs-consent`). Das Banner sendet dabei `gtag('consent','update', …)`.
- Alle Ereignisse heißen `lp_sen_…` (CTAs je Platzierung, PDF, Telefon/E-Mail, Programm-Tab, Scroll 25/50/75/90 %, Verweildauer 30 s/60 s/2 min). Details: `LP_Senioren_GTM_Tracking-Plan.xlsx`, Container: `GTM_LP_Senioren_Import.json` (nicht Teil dieses Repos).

## Sprungmarken (Google-Ads-Sitelinks)
#themen · #besichtigungen · #fuer-wen · #programm · #referentinnen · #preise / #teilnahme · #rueckblick-2025 · #anmeldung

## Assets
Bilder als WebP in Anzeigegröße, Hero-Video 1280×720 ohne Ton (`b1_hero-neu-720.mp4`), Social-Vorschau `og-image.jpg` (1200×630). Geänderte Dateien bekommen neue Namen, weil `assets/` 30 Tage gecacht wird.
