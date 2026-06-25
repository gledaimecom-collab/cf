---
title: VidLink Proxy
emoji: 🎬
colorFrom: green
colorTo: emerald
sdk: docker
pinned: false
---

<div align="center">
  <h3><b>The Ultimate VidLink.pro Multi-Platform Proxy</b></h3>
  <p>A high-performance proxy that bypasses Cloudflare Geo-blocks (403 errors) to retrieve direct M3U8 streaming links for Movies and TV Shows natively, with zero RAM overhead and full seeking support.</p>
</div>

---

### 🚀 **Features**

- ⚡ **Multi-Platform**: Runs on Node.js Server (VPS), Vercel Serverless, Hugging Face Spaces Docker, or Cloudflare Pages.
- 🛡️ **Bypasses Cloudflare 403s**: Actively circumvents Cloudflare-to-Cloudflare `1020` blocks.
- 🔐 **Native Decryption**: Uses `tweetnacl` to replicate VidLink's `XSalsa20-Poly1305` logic natively in JS (No heavy WASM payloads).
- 🕒 **Adaptive Time-Sync**: Intelligence-based timestamp offset to prevent token expiration.
- 🕵️ **Zero-RAM Streaming Proxy**: Uses Node.js `stream.pipe()` or Web Streams for stealth proxying of `m3u8` playlists and `.ts` chunk segments.
- 🎨 **Range & Seek Support**: Fully passes `Range` headers back and forth, allowing you to seek immediately in your video player.
- 🎨 **Minimalist Documentation**: Built-in aesthetic landing page for easy testing.

---

### ☁️ **Deploy to Cloudflare Pages**

1. Push this repository to GitHub
2. Go to [pages.cloudflare.com](https://pages.cloudflare.com) and connect your repo
3. Cloudflare will auto-detect the `functions/` directory
4. No build command needed - Functions are deployed automatically

Your proxy will be available at `https://{project-name}.pages.dev`

**Note for Cloudflare Pages**: Endpoints are prefixed with `/api`:
- `/api/movie/{tmdb_id}`
- `/api/tv/{tmdb_id}/{season}/{episode}`
- `/api/watch?url={encoded_url}`

---

### 🤗 **Deploy to Hugging Face Spaces**

1. Create a new Space at [huggingface.co/new-space](https://huggingface.co/new-space)
2. Select **Docker** as the SDK
3. Push this repository to the Space (or upload files manually)
4. The Space will automatically build and run on port 7860

Your proxy will be available at `https://{username}-{space-name}.hf.space`

---

### 🌍 **Deploy to Vercel**

If you don't have a VPS, you can instantly deploy the serverless version to Vercel:

```bash
npx vercel deploy
```
Vercel will detect `vercel.json` and deploy `api/index.js` as a serverless function automatically.

---

### 🛠️ **Local Node.js Server**

1. **Install dependencies**
   ```bash
   npm install
   ```

2. **Start the server**
   ```bash
   npm start
   ```

The local proxy will be running at `http://localhost:3000`.

---

### 📖 **Usage**

Once your server is running or deployed, you can hit the following endpoints:

| Endpoint | Description |
| :--- | :--- |
| `GET /movie/{tmdb_id}` | Fetch direct sources for movies, with fully rewritten proxy streams. |
| `GET /tv/{tmdb_id}/{s}/{e}` | Fetch direct sources for episodes. |
| `GET /watch?url={encoded}` | Streaming proxy to circumvent 403 headers and CORS blocks. |

**Cloudflare Pages**: Prefix all endpoints with `/api` (e.g., `/api/movie/123`)

---

### ⚙️ **Technical Breakdown**

This project reverse-engineered the VidLink Pro encryption logic. Unlike traditional solutions that rely on a browser or WASM bridge, this tool:

1. Generates a valid 24-byte nonce.
2. Constructs a binary message containing the `Media ID` and a `64-bit Big-Endian Timestamp`.
3. Encrypts the payload using the production key.
4. Acts as a transparent proxy for `.ts` video chunk retrieval by spoofing correct headers.

---

<div align="center">
  <p><b>Developed by <a href="https://github.com/mdtahseen7">Tahseen</a></b></p>
  <sub>Built with ❤️ for the open-source community.</sub>
</div>
