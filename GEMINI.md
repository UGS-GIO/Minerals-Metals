# Minerals-Metals — PR review guide
Static ArcGIS JS 4.19 map app (index.html + map.js, lightbox2) for UGS/BLM mining & industrial
mineral data. LEGACY per house rules — being retired; do the minimum. Review ONLY the changed lines
(general bug/security/quality assumed). Cite file:line; group nits; prefer minimal, in-style fixes
over refactors — no rewrites on retiring code.

## Match the existing code
- jQuery / ArcGIS-4 era single-file map.js. Match surrounding patterns; don't add frameworks, a
  build step, or rewrite working popup code.

## Security (the priority for a public legacy app)
- NO secrets, API keys, or ArcGIS tokens committed in client-side JS/HTML — these viewers can embed
  map/service keys, so flag any hardcoded credential or `token=`.
- XSS / DOM injection: popups and lightbox captions are built from feature attributes via
  `innerHTML` — any new field rendered from a Feature/API response or a URL query param must be
  escaped; no unescaped `innerHTML`/`document.write` of user/feature/URL data.

## Correctness
- Fail loud on fetch/query errors — don't silently blank the map; handle empty/failed responses.
