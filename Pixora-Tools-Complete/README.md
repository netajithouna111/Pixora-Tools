# Pixora Tools — Complete MVP package

## What is included
- Responsive dark/light homepage and brand identity
- Search and category filtering across 30 listed tool entries
- Browser-side image upload and preview (25 MB file limit)
- Working browser tools: image compression, resizing, center crop, rotate, flip, grayscale, blur, text watermark, brightness/contrast, PNG/JPEG/WEBP conversion, social/platform canvas presets, favicon canvas
- Basic image metadata shown on upload
- AI background removal using Transformers.js + Xenova/MODNet in the browser
- AI 2× super-resolution and AI-assisted photo enhancement using UpscalerJS (model output plus local tonal finishing)
- About, Privacy, Terms and Contact pages (contact email is a placeholder)
- `robots.txt`, `sitemap.xml`, Cloudflare `_headers`
- No build step; static HTML/CSS/JS

## Important feature status
Still not active: AI face restoration/colorization, QR code generation, PDF export and pixel sampling. The three AI tools included here do not require a paid API key. They download open model/runtime files from third-party CDNs and model hosts on first use. A large download, modern browser and sufficient device memory are required. Model licensing and commercial-use terms must be checked before monetizing the site. The UI identifies unavailable features rather than pretending to process them.

## Local preview
Run:
```bash
python -m http.server 8000
```
Open http://localhost:8000.

## Cloudflare Pages deployment
1. Upload this folder to a GitHub repository.
2. Cloudflare Dashboard → Workers & Pages → Create → Pages → Connect to Git.
3. Choose the repository.
4. Framework preset: None.
5. Build command: leave empty.
6. Build output directory: `/` (repository root).
7. Deploy.

## Before public launch
- Replace `YOUR-DOMAIN.example` in `index.html`, `robots.txt`, and `sitemap.xml` with your actual HTTPS domain.
- Add a real monitored support email to `contact.html`.
- Check legal/privacy text for your actual hosting, analytics and any third-party integrations.
- Add a cookie/consent mechanism if required by your chosen analytics/advertising setup and applicable law.
- Test all tools on current desktop and mobile browsers, including large files and unsupported image formats.
- Set up Google Search Console and submit `/sitemap.xml` after the domain is live.
- Do not add AdSense until the site has substantial useful content, working tools, and complete policy pages.
- Confirm country-specific passport photo specifications from official authorities; the preset is only a canvas size.

## Technical notes
This is a static MVP, not a full SaaS backend. Image operations run on the user's device via Canvas. No accounts, server-side uploads, database, AI API, payments or analytics are configured. Never put API secrets in browser JavaScript.


## AI tools — important setup notes
- Background removal uses `@huggingface/transformers` with `Xenova/modnet`; inference runs in the browser. The model is downloaded from Hugging Face on first use.
- AI Image Upscaler uses the UpscalerJS browser runtime and its default super-resolution model. AI Photo Enhancer uses the same super-resolution pass followed by a light local contrast finish; it is not face restoration.
- TensorFlow.js, UpscalerJS and the default model are loaded from jsDelivr. Keep the page served over HTTPS (Cloudflare Pages provides HTTPS) or localhost.
- These features are free to run without a Pixora API key, but model downloads consume visitor data and device CPU/GPU/RAM. Performance varies; older phones may run slowly or run out of memory. Start with small images.
- Third-party script/model hosts receive normal network requests. Image pixels are processed locally by these browser workflows; do not claim that no third-party network requests occur.
- Review the current licenses of each runtime and exact model artifact before commercial use. “Free to use” does not automatically mean unrestricted commercial redistribution.
- If a CDN or model host is unavailable, the AI tool will show an error; the ordinary Canvas tools continue to work.
