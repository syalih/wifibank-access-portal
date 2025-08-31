# WifiBank AuthFlow

A banking‑grade **Tailwind CSS** login experience for modern web apps. Includes **dark mode**, **RTL/i18n (English/Arabic)**, **virtual keyboard (numeric & full)**, **WebAuthn/Passkeys demo**, **OTP modal**, **session‑timeout banner**, **password strength meter**, and more. Built as a clean, standalone HTML + JS page you can drop into any app or wire to your backend.

---

## ✨ Features

* 🌗 **Dark Mode** toggle (persisted in `localStorage`)
* 🌍 **I18n + RTL**: English / Arabic switch with `dir=ltr/rtl`
* 🔐 **Customer ID + Password/PIN** inputs with **Caps Lock** warning
* ⌨️ **Virtual Keyboard** (toggle):

  * **123** numeric keypad (shuffled layout for each open)
  * **ABC** full QWERTY keyboard with **Shift**, **Space**, **Backspace**, **Clear**
* 🧠 **Password strength meter** (live)
* 👁 **Show/Hide password**
* 🪪 **WebAuthn / Passkeys** demo button (device support check)
* 📲 **OTP (2FA) modal** with 6 inputs, resend timer, keyboard navigation
* ⏳ **Session‑timeout banner** with countdown & "Stay signed in"
* ✅ Client‑side validation + accessible labels and live regions
* 🧭 Mobile‑first, responsive Tailwind layout

> ⚠️ **Security note**: This is a **demo UI**. Replace mock logic with real server endpoints before production.

---

## 🧱 Tech Stack

* **Tailwind CSS** via CDN (or CLI)
* **Vanilla JavaScript** (no framework required)
* **Semantic HTML5**

---

## 📁 Project Structure

```
.
├── index.html     # WifiBank login page (Tailwind + JS)
└── README.md      # You are here
```

---

## 🚀 Quick Start

1. **Clone**

```bash
git clone https://github.com/your-org/wifibank-authflow.git
cd wifibank-authflow
```

2. **Open** (no build needed)

```bash
# macOS\ nopen index.html
# Windows
start index.html
```

Or serve locally (recommended for CORS‑safe testing):

```bash
npx serve .
# or
python -m http.server 5173
```

3. **Try it**

* Toggle **Dark/Light**
* Switch **English ↔ العربية** (notice RTL)
* Open **Virtual Keyboard** (⌨️), switch **123/ABC**, try **Shuffle**
* Hit **Use Face/Touch ID (WebAuthn)** to see capability check
* Submit to trigger **OTP modal** and **session‑timeout** demo

---

## 🔌 Hooking to Your Backend

Replace demo handlers with real endpoints:

### 1) Sign‑in

```js
// POST /api/auth/login (example)
fetch('/api/auth/login', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json', 'X-CSRF-Token': token },
  credentials: 'include',
  body: JSON.stringify({ customerId, password })
});
```

**Recommendations**

* Use **HTTPS** only; set **Secure**, **HttpOnly**, **SameSite** cookies
* Implement **CSRF** protection & **rate limiting**
* Log **device fingerprint** + IP, apply risk‑based challenges

### 2) OTP / 2FA

* `/api/auth/otp/send` → send code (SMS/Email/TOTP)
* `/api/auth/otp/verify` → verify 6‑digit code, issue session

### 3) Passkeys (WebAuthn)

* Use a server lib (e.g., **@simplewebauthn/server**) to create and verify challenges
* Front‑end: `navigator.credentials.create()` and `navigator.credentials.get()`
* Store public key credentials per user; bind to device + origin

---

## 🧩 Tailwind: CDN → CLI (optional)

For production, prefer a **compiled Tailwind build** to tree‑shake unused classes.

```bash
npm i -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

`tailwind.config.js`

```js
module.exports = {
  content: ['index.html', 'src/**/*.{js,ts,html}'],
  darkMode: 'class',
  theme: { extend: {} },
  plugins: [],
};
```

Build:

```bash
npx tailwindcss -i ./src/input.css -o ./public/styles.css --minify
```

Update `index.html` to reference your compiled CSS.

---

## 🔒 Security Checklist (Before Production)

* [ ] Enforce **HTTPS** & HSTS
* [ ] **CSP** headers (script‑src, frame‑ancestors, upgrade‑insecure‑requests)
* [ ] **CSRF** tokens for state‑changing requests
* [ ] **Brute‑force** protections (lockout/backoff, captcha where needed)
* [ ] **Password policy** + breach checks (HIBP API)
* [ ] **WebAuthn** (passkeys) for phishing‑resistant MFA
* [ ] **Audit logging** + anomaly detection
* [ ] **Accessibility** pass (tab order, labels, contrast)

---

## 📸 Screenshots (placeholders)

* Light mode – Login form
* Dark mode – Virtual Keyboard (ABC)
* OTP modal

> Add your screenshots to `/docs` and link them here.

---

## 🗺 Roadmap

* [ ] Full registration & reset password flows
* [ ] Real WebAuthn registration/login
* [ ] reCAPTCHA / hCaptcha integration
* [ ] Device management (trusted devices)
* [ ] Remember‑me with rotating refresh tokens

---

## 🤝 Contributing

PRs are welcome! Please open an issue first for discussion.

---

## 📄 License

MIT © 2025 WifiBank / Your Organization
