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
Google Analytics 4 (G-ZF9DT30DB7) lädt erst nach Zustimmung im Cookie-Banner (localStorage-Schlüssel `mfs-consent`).
