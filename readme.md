# ⚡ CloakJS

> **Lightweight, zero-dependency JavaScript & Cloudflare Worker string obfuscator with rotating XOR encryption and Base64 encoding.**

[Run Online](https://www.google.com/search?q=https://mstbat.github.io/CloakJS/)
[](https://github.com/MSTbat/CloakJS)
[License: MIT](https://www.google.com/search?q=LICENSE)
[](https://github.com/MSTbat/CloakJS)

[📖 مطالعه مستندات به زبان فارسی (Persian Documentation)]()

---

## 🚀 Run Online

Use CloakJS directly in your browser without any installation:

👉 **[Launch CloakJS Online App](https://mstbat.github.io/CloakJS/)**

---

## 🌟 Overview

**CloakJS** protects sensitive API tokens, proxy endpoints, headers, secrets, and URLs inside Cloudflare Workers and client-side JavaScript. It extracts string literals, encodes them using rotating XOR bitwise encryption, packages them into an indexed table, and injects a tiny (~15 lines), zero-dependency, `Map`-cached decoder.

Everything runs **100% in your browser**—no code or sensitive credentials are ever transmitted to an external server.

---

## ✨ Features

- 🛡️ **Rotating XOR & Base64 Bitmasking:** Encrypts strings against static regex scanners, bot crawlers, and inspection scripts.
- ⚡ **Minimal Runtime Overhead:** Self-contained decoder with a high-performance in-memory `Map` cache to avoid repeated string decoding.
- 🧠 **Smart Code Parsing:** Intelligently preserves `import`/`export` paths, template literals, regex expressions, and object keys (`key: value`).
- 📁 **Dynamic File Renaming:** Automatically recognizes files on upload or drag-and-drop (`name.js` → `name.obfuscated.js`).
- ⌨️ **UX Workflows:** Supports drag-and-drop, `Ctrl + Enter` shortcut execution, one-click clipboard copy, and file download.
- 🔒 **Privacy-First & Offline:** Runs entirely client-side using Vanilla JS & Tailwind CSS; zero external dependencies.

---

## 🔍 How It Works

### Input (`source.js`)
```javascript
export default {
  async fetch(request, env) {
    const secretEndpoint = "https://api.internal.network/v1/auth";
    const bearerToken = "Bearer secret_live_key_98234710";
    return fetch(secretEndpoint, {
      headers: { "Authorization": bearerToken }
    });
  }
};
```

### Output (`source.obfuscated.js`)
```javascript
// @ts-nocheck
const _0x_key = 79;
const _0x_tbl = ["v9HXzGsJBgYJAwYbbhkDaxobBx8fZb/R18w=","HxwCFBIVAh4=","Ij05Ezs4JjAuIzYQKi8="];
const _0x_cache = new Map();
function func_dec(idx) {
  if (_0x_cache.has(idx)) return _0x_cache.get(idx);
  const raw = atob(_0x_tbl[idx]);
  let out = "";
  for (let i = 0; i < raw.length; i++) {
    out += String.fromCharCode(raw.charCodeAt(i) ^ (_0x_key ^ (i % 11)));
  }
  try { out = decodeURIComponent(escape(out)); } catch (_) {}
  _0x_cache.set(idx, out);
  return out;
}

export default {
  async fetch(request, env) {
    const secretEndpoint = func_dec(0);
    const bearerToken = func_dec(1);
    return fetch(secretEndpoint, {
      headers: { [func_dec(2)]: bearerToken }
    });
  }
};
```

---

## 🛠️ Project Structure

```bash
CloakJS/
├── index.html        # Complete standalone web app (GitHub Pages entry)
├── README.md         # English documentation
└── README.fa.md      # Persian documentation
```

---

## 📄 License

Distributed under the **MIT License**.
