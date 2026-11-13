# 🧼 AIMetaScrub: AI Metadata Remover & Viewer

A free, privacy-first web app that shows exactly what hidden data your images carry (**C2PA content credentials, EXIF, XMP, IPTC and AI prompts**) and removes it in one click. Everything runs **in your browser**: nothing is uploaded, and no account is needed.

<!-- Add a screenshot: drag an image into the GitHub editor, then paste the link below.
<img width="1408" alt="AIMetaScrub" src="PASTE_IMAGE_LINK_HERE" />
-->

---

##  Overview

Image files often carry more than pixels. Cameras write GPS coordinates and serial numbers, editors write software and edit history, and AI tools can embed prompts, generator names and signed C2PA records.

AIMetaScrub reads that hidden data, explains every field in plain language, rates how revealing it is, and cuts it out of the file **without re-encoding the image**, so the picture stays exactly the same.

It has three tools in one page:

| Tool | What it does |
|------|--------------|
| **Remove Metadata** | Inspect an image, then strip its metadata and verify the result with a re-scan |
| **View Metadata** | Read-only inspection. Nothing is changed |
| **Edit Metadata** | Write your own description, author, copyright and GPS location into JPG and PNG files |

---

##  Live Demo

Try the live app  [AIMetaScrub on Vercel](https://ai-meta-scrubb.vercel.app/)

Each tool has its own link: `#remove`, `#view` and `#edit` (for example `.../#view`).

---

##  Features

- 🔍 **Full inspector** for C2PA, EXIF, XMP, IPTC, PNG text chunks and AI prompts
- 🏷️ **AI metadata verdict**: a clear "AI metadata found" or "No AI metadata found" banner on every file
- 🛡️ **Privacy score (0–100)** with High / Medium / Low risk tags per field
- 📝 **Plain-language notes** that explain what each field means
- ✂️ **Lossless cleaning**: metadata is cut from the file; pixels are never re-compressed or resized
- ♻️ **Re-scan after cleaning** with a before/after comparison
- 🎛️ **Selective removal**: keep the color profile and photo orientation
- 📦 **Batch processing**: up to 5 images at once, with **Download all (ZIP)**
- 🧪 **Sample scan**: try the inspector with a built-in AI-style image
- ✏️ **Metadata editor** for JPG and PNG
- 🔒 **100% client-side**: no upload, no account, no tracking

---

##  How It Works

1. **Upload** your image (it stays on your device)
2. **Inspect** every field, grouped by type, with risk levels
3. **Remove** the metadata from the file headers
4. **Verify and download**: compare before and after, then save the clean copy

---

##  Tools and Technologies

| Category | Details |
|----------|---------|
| Language | JavaScript (vanilla, single file) |
| Markup and Styling | HTML5, CSS3 (custom properties, CSS animations) |
| Browser APIs | File API, Blob, Canvas, DataView, TextDecoder |
| Hosting | Vercel (static site) |
| Font | Plus Jakarta Sans (Google Fonts, with system fallback) |
| Dependencies | None. No framework and no build step |

---

##  Supported Formats and Metadata

| Format | Metadata read | What cleaning removes |
|--------|---------------|-----------------------|
| **JPG / JPEG** | EXIF, XMP, IPTC, C2PA (JUMBF), comments | EXIF, XMP, IPTC, C2PA, comments and other app segments |
| **PNG** | Text chunks (including AI prompts), eXIf, C2PA (caBX) | All non-essential ancillary chunks |
| **WebP** | EXIF, XMP, C2PA | EXIF, XMP and other metadata chunks |

The color profile is kept by default so colors look the same. For JPG, photo orientation can also be kept so phone photos don't appear rotated.

> HEIC, TIFF, video and PDF are not supported yet. The editor supports JPG and PNG only.

---

##  Privacy Score

The score starts at 100 and loses points for each field found, based on how revealing it is.

| Risk level | Penalty per field | Examples |
|------------|-------------------|----------|
| 🔴 High | −18 | GPS location, camera serial number, artist name, AI prompts |
| 🟠 Medium | −6 | Camera make and model, lens, dates, software, copyright, C2PA generator and signature |
| 🔵 Low | −2 | Everything else, such as orientation |

If AI traces are detected (a generator name, an AI prompt or a C2PA source type), another 10 points are deducted. The score never goes below 0.

It is a simple guide, not a formal security rating. It only looks at metadata.

---

##  Project Structure

```
├── README.md
├── index.html
└── LICENSE
```

The whole app (HTML, CSS and JavaScript) lives in `index.html`.

---

##  Usage

### 1. Clone the Repository
```bash
git clone https://github.com/muqadasejaz/AI-Meta-Scrub
cd AI-Meta-Scrub
```

### 2. Run Locally
It is a single static file, so you can simply open `index.html` in your browser. Or serve it:
```bash
python -m http.server 8000
```
Then open `http://localhost:8000`.

### 3. Use the App
1. Drag and drop up to 5 JPG, PNG or WebP images, or click **Scan a sample image**
2. Open **View metadata** to see every field and the privacy score
3. Click **Remove metadata** (or **Remove all metadata**)
4. Download the clean image, or **Download all (ZIP)**

### 4. Deploy on Vercel
1. Push the repo to GitHub
2. In Vercel, click **Add New → Project** and import the repo
3. Keep the defaults (Framework Preset: **Other**, no build command, no output directory)
4. Click **Deploy**

---

##  Privacy and Security

- Files are read and cleaned inside your browser tab and held only in memory
- Nothing is sent to a server. You can confirm this in your browser's network tab while cleaning
- There are no accounts, no cookies for tracking and no analytics on your files

---

##  Limitations

- Only **metadata** is removed. Invisible pixel-level watermarks (such as SynthID) and visible marks are part of the image and are **not** affected
- C2PA records are displayed, but signatures are **not verified** in the browser
- Removing metadata does not guarantee that a social platform will not label an image as AI-generated. Platforms use other signals too. If your image is realistically AI-generated, follow each platform's disclosure rules
- Keeping photo orientation works for JPG only
- The AI check matches known generator names in metadata fields, so it can include description or keyword fields stored in the file

---

##  Roadmap

- [x] Metadata inspector with privacy score and risk tags
- [x] Lossless removal with before/after verification
- [x] Batch cleaning and ZIP download
- [x] Metadata editor (JPG and PNG)
- [ ] Bento-style features layout and dark mode
- [ ] HEIC and TIFF support
- [ ] Video (MP4/MOV) and PDF support
- [ ] Keep-copyright option for selective removal
- [ ] Exportable scan report
- [ ] Full C2PA signature verification

---

##  References

- [C2PA Specifications](https://c2pa.org/specifications/): Content Credentials standard
- [IPTC Photo Metadata Standard](https://www.iptc.org/standards/photo-metadata/): IPTC and digital source type fields
- [PNG Specification (W3C)](https://www.w3.org/TR/png/): PNG chunk structure
- [WebP RIFF Container](https://developers.google.com/speed/webp/docs/riff_container): WebP file structure
- [Vercel Documentation](https://vercel.com/docs): Static site deployment

---

##  Author

Muqadas Ejaz

BS Computer Science (AI Specialization)

AI/ML Engineer

Kaggle Grand Master

Data Science & Gen AI

📫 Connect with me on [LinkedIn](https://www.linkedin.com/in/muqadasejaz/)

🌐 GitHub: [github.com/muqadasejaz](https://github.com/muqadasejaz)

📬 Kaggle: [Kaggle Profile](https://www.kaggle.com/muqaddasejaz)

---

##  License

This project is open-source and available under the [MIT License](LICENSE).

⭐ If you find this project useful, don't forget to star the repository!
