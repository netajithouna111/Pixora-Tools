# Pixora Tools architecture

## Current MVP
Static frontend hosted via Cloudflare Pages. HTML provides crawlable content; CSS handles responsive UI; vanilla JS implements tool discovery and browser-side image processing.

## Processing flow
User file → browser File input → Image decode → Canvas transformation → Blob export → local download.
No upload endpoint is present for the working image tools.

## Future production architecture
- Frontend: Next.js/static generation for unique SEO tool landing pages.
- Edge/API: Cloudflare Workers for controlled third-party API calls and rate limits.
- AI: optional provider integration, with explicit disclosure before image upload.
- Storage: no persistent image storage by default; if needed, temporary object storage with strict expiry and deletion.
- Database: D1 only for accounts/preferences/metadata if justified.
- Monitoring: uptime, error monitoring, Search Console and privacy-conscious analytics.

## Security checklist
- Keep third-party API keys server-side.
- Validate MIME and file signatures where possible.
- Enforce upload size, pixel dimension and request limits.
- Use HTTPS, security headers, dependency updates and rate limits.
- Never log image contents or sensitive filenames.
- Disclose any third-party data processing.
- Test SVG and animated formats carefully before enabling them.


## Browser AI layer
AI tools are lazy-loaded at run time. Background removal imports Transformers.js and the Xenova/MODNet model. Super-resolution and AI-assisted enhancement use the UpscalerJS browser runtime with TensorFlow.js. No Pixora backend, account, API key or server-side image upload is used. Model weights are fetched from third-party hosts and cached according to browser/CDN behavior.
