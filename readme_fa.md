# ⚡ کلوک جی‌اس (CloakJS)

> **ابزار سبک، سریع و بدون وابستگی برای مبهم‌سازی رشته‌های متنی در ورکر‌های کلادفلر و کدهای جاوااسکریپت با الگوریتم XOR چرخشی و Base64.**

[مجوز: MIT](https://www.google.com/search?q=LICENSE)

[🌐 Read Documentation in English](README.md)

---

## 🚀 اجرای آنلاین

بدون نیاز به هیچ‌گونه نصب یا راه‌اندازی، می‌توانید مستقیماً از این ابزار در مرورگر خود استفاده کنید:

👉 **[ورود به صفحهٔ اجرای آنلاین CloakJS](https://mstbat.github.io/CloakJS/)**

---

## 🌟 معرفی پروژه

**کلوک جی‌اس (CloakJS)** یک ابزار سبک و سریع تحت وب است که کدهای حساس شما مانند توکن‌های API، آدرس‌های سرور و پروکسی، هدرهای احراز هویت و متغیرهای کلادفلر ورکر (Cloudflare Workers) را در برابر بازرسی‌های خودکار، ربات‌های اسکنر و کراولرها استتار می‌کند.

این ابزار تمام رشته‌های متنی (String Literals) را استخراج کرده، با یک کلید XOR چرخشی و پایگاه Base64 کدگذاری نموده و یک دیکودر اختصاصی بسیار کم‌حجم (حدود ۱۵ خط) با قابلیت کش هوشمند درون حافظه (`Map`) به ابتدای کد تزریق می‌کند.

تمام محاسبات **۱۰۰٪ سمت مرورگر شما (Client-Side)** انجام می‌شود و هیچ اطلاعات یا کدی به سرورهای خارجی ارسال نخواهد شد.

---

## ✨ ویژگی‌های کلیدی

- 🛡️ **رمزنگاری بر پایه XOR چرخشی و Base64:** مقاومت کامل در برابر اسکنرهای متنی و عبارات باقاعده (Regex).
- ⚡ **دیکودر سبک و بهینه:** استفاده از کش حافظه (`Map`) برای جلوگیری از رمزگشایی چندبارهٔ رشته‌های تکراری و به حداقل رساندن افت پرفورمنس.
- 🧠 **پارس هوشمند جاوااسکریپت:** دست نخورده باقی ماندن مسیرهای `import`/`export`، قالب‌های متنی (Template Literals)، ریجکس‌ها و کلیدهای آبجکت.
- 📁 **مدیریت داینامیک نام فایل‌ها:** تشخیص خودکار نام فایل ورودی و تنظیم نام متناظر برای خروجی (`name.js` → `name.obfuscated.js`).
- ⌨️ **تجربه کاربری مدرن:** پشتیبانی از کشیدن و رها کردن فایل (Drag & Drop)، میانبر کیبورد `Ctrl + Enter` برای اجرای سریع، و کپی/دانلود با یک کلیک.
- 🔒 **حریم خصوصی کامل و بدون نیاز به اینترنت:** طراحی شده به صورت تک‌فایل مستقل بدون نیاز به بک‌اند یا دیتابیس.

---

## 🔍 نمونه عملکرد

### کد ورودی (`source.js`)
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

### کد خروجی مبهم‌شده (`source.obfuscated.js`)
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

## 🛠️ ساختار فایل‌های پروژه

```bash
CloakJS/
├── index.html        # کل رابط کاربری و موتور پردازش کلاینت‌ساید
├── README.md         # مستندات انگلیسی
└── README.fa.md      # مستندات فارسی
```

---

## 📄 لایسنس

این پروژه تحت مجوز **MIT** منتشر شده است.