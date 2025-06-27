# easy-otp

> **Human‑friendly one‑time passcode generator for Node.js**

[![npm version](https://img.shields.io/npm/v/easy-otp.svg)](https://www.npmjs.com/package/easy-otp)
[![build status](https://github.com/your‑org/easy-otp/actions/workflows/ci.yml/badge.svg)](https://github.com/your‑org/easy-otp/actions)
[![codecov](https://img.shields.io/codecov/c/github/your‑org/easy-otp.svg)](https://app.codecov.io/gh/your‑org/easy-otp)
[![license](https://img.shields.io/npm/l/easy-otp.svg)](LICENSE)

`easy‑otp` produces numeric OTPs that are easy to read, dictate, and re‑type while still offering configurable entropy.  It ships **only** the generator—verifying, expiring, and rate‑limiting codes are left to you.

---

## ✨ Features

* **Pure digits** – no letters or symbols
* **Ambiguity‑free** by default (excludes `0` & `1`)
* **Configurable length** (`4‑12` digits)
* **Secure RNG** (`crypto.randomInt`)
* **Tiny footprint** (< 1 kB min+gz)
* **TypeScript first** – fully typed, ESM & CommonJS
* Convenient **CLI**: `npx easy-otp 8`

---

## 🚀 Quick Start

### Install

```sh
npm i easy-otp
```

> Requires **Node v16 LTS** or later.

### Generate a code (API)

```ts
import { generateOtp } from 'easy-otp';

const code = generateOtp();  // "472638"
```

#### With options

```ts
// 8‑digit code, allow 0 & 1
const code = generateOtp({ length: 8, avoidAmbiguous: false });
```

### Generate a code (CLI)

```sh
npx easy-otp          # 6‑digit default
npx easy-otp 10       # 10‑digit code
```

---

## 🛡️ Security Notes

| Length (digits) | Approx. Entropy\* |
| --------------- | ----------------- |
| 4               | 12 bits           |
| 6 (default)     | 18 bits           |
| 8               | 24 bits           |
| 10              | 30 bits           |
| 12 (max)        | 36 bits           |

\*Entropy assumes 8 possible digits (2‑9) when `avoidAmbiguous: true`.
For stronger guarantees, increase length and **always** rate‑limit and expire codes server‑side.

> **Important:** `easy‑otp` does *not* store or verify codes.  You **must** implement:
>
> 1. Temporary storage (DB, cache, etc.)
> 2. Expiration policy (e.g., 5 min)
> 3. Online brute‑force mitigation (rate‑limiting, CAPTCHA, lock‑outs)

---

## 💻 API

```ts
interface GenerateOtpOptions {
  /** Number of digits (4‑12). Default: 6 */
  length?: number;
  /** Exclude ambiguous digits 0 & 1. Default: true */
  avoidAmbiguous?: boolean;
}

declare function generateOtp(options?: GenerateOtpOptions): string;
```

---

## 🧪 Development

```sh
git clone https://github.com/your‑org/easy-otp
cd easy-otp
pnpm install
pnpm test      # vitest + coverage
```

\### Scripts

| Script           | Purpose                       |
| ---------------- | ----------------------------- |
| `pnpm build`     | Build CJS + ESM bundles       |
| `pnpm lint`      | ESlint + Prettier             |
| `pnpm typecheck` | `tsc --noEmit`                |
| `pnpm release`   | Publish to npm via Changesets |

---

## 🤝 Contributing

Pull requests are welcome!  Please create an issue first if you plan a large change.

1. Fork and clone repo
2. Run `pnpm install`
3. Add tests for your change (100 % coverage is the goal 🚀)
4. Run `pnpm test && pnpm lint`
5. Open a PR

---

## 📜 License

Released under the **MIT License**.  See [`LICENSE`](https://opensource.org/license/mit) for details.
