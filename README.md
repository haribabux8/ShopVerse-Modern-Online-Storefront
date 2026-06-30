# 🛍️ ShopVerse — Modern Online Storefront

**ShopVerse** is a polished, fully responsive e-commerce storefront built with pure HTML, CSS, and vanilla JavaScript — no frameworks, no build step, no backend lock-in. It demonstrates how far modern front-end engineering can go on its own: a complete shopping experience covering product discovery, filtering, a persistent cart, wishlist, checkout flow, and a clean account area, all packaged behind a refined design system with light/dark themes.

The project was crafted as a portfolio-grade reference for clean front-end architecture: semantic markup, a token-driven design system, modular JS, and graceful client-side state management via `localStorage`. It looks production-ready out of the box and is trivially deployable to any static host — GitHub Pages, Netlify, Vercel, Cloudflare Pages, or an S3 bucket.

Whether you are a recruiter reviewing UI craft, a developer studying vanilla-JS architecture, or a contributor looking for a clean base to extend into a full backend-powered store, ShopVerse is structured to be readable, hackable, and easy to grow.

---

## 📖 Overview

**Purpose** — Provide a beautiful, fully working storefront experience without forcing a heavy framework or backend dependency. Ideal for prototypes, landing pages, internal demos, and learning projects.

**Business Value**
- Zero-cost hosting and instant time-to-market (static deployment).
- Drop-in front-end shell that can later be wired to any commerce backend (Shopify, Medusa, Strapi, custom Node/Express, Firebase).
- Conversion-focused UI patterns (hero, social proof, urgency, frictionless cart) inspired by leading DTC brands.

**User Benefits**
- Fast page loads, no framework runtime tax.
- Persistent cart and wishlist across visits.
- Accessible, keyboard-friendly navigation with light and dark themes.
- Mobile-first responsive layout that feels native on phones and tablets.

**Main Functionality**
- Catalog browsing with categories, search, sort, and filtering.
- Product detail pages with specs, ratings, gallery, and "add to cart".
- Full cart with quantity controls, subtotal, shipping, and tax preview.
- Multi-step checkout with form validation and order summary.
- Lightweight client-side auth UI (login / register screens).

---

## ✨ Features

### 🛒 Core Features
- ✅ Home page with hero, categories, featured and best-seller carousels
- ✅ Product listing with category filters, price range, sort, and live search
- ✅ Rich product detail page (gallery, rating, reviews count, specs table)
- ✅ Persistent shopping cart powered by `localStorage`
- ✅ Multi-step checkout (shipping → payment → review)
- ✅ Wishlist with one-click toggle
- ✅ Toast notifications for cart, wishlist, and form actions

### 👤 User Features
- ✅ Login and registration UI
- ✅ Newsletter subscription form
- ✅ Theme switcher (light / dark)
- ✅ Recently viewed products
- ✅ Quantity stepper and inline price recalculation
- ✅ Empty-state designs for cart, wishlist, and search

### 🛠️ Admin-Ready Hooks *(extension-ready)*
- ⬜ Product CRUD endpoints (placeholder structure in `js/products.js`)
- ⬜ Order management dashboard
- ⬜ Coupon and discount engine

### 🚀 Advanced Features
- ✅ Token-based design system (CSS custom properties)
- ✅ Reusable component patterns (cards, chips, badges, modals)
- ✅ Skeleton loaders and page-transition spinner
- ✅ SVG-based placeholder image generator (no broken images, ever)
- ✅ Fully responsive grid (mobile, tablet, desktop, wide)
- ✅ Smooth scroll, fade-in animations, and micro-interactions

### 🔒 Security Features *(client-side scope)*
- ✅ Input validation on all forms (email, required, length)
- ✅ Safe HTML rendering for user-provided strings
- ✅ No third-party trackers or external scripts beyond Google Fonts
- ✅ Ready to harden with CSP headers at the hosting layer

---

## 🧰 Tech Stack

### Frontend
- HTML5 (semantic, accessible)
- CSS3 with custom properties, Grid & Flexbox
- Vanilla JavaScript (ES6+ modules-style organisation)
- Google Fonts — Inter
- Inline SVG iconography

### Backend
- _Not included._ ShopVerse is intentionally backend-agnostic. Recommended integrations:
  - Node.js + Express (REST)
  - Firebase / Supabase
  - Headless commerce (Shopify Storefront API, Medusa, Saleor)

### Database
- _Not included._ Suggested options when adding a backend:
  - PostgreSQL (relational)
  - MongoDB (document)
  - Firestore (realtime)

### DevOps & Deployment
- GitHub Pages, Netlify, Vercel, Cloudflare Pages, or any static host
- GitHub Actions (ready for CI lint/format/preview deploy)

### Development Tools
- Visual Studio Code
- Live Server / `npx serve`
- Git & GitHub
- Chrome DevTools (Lighthouse, Responsive mode)
- Prettier (formatting)

---

## 🏗️ Architecture

ShopVerse follows a **classic multi-page static architecture** with shared JavaScript modules that handle global state (cart, wishlist, theme) and per-page rendering logic.

```text
┌──────────────────────────────────────────────────────────────┐
│                          Browser                             │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐ ┌──────────┐ │
│  │ index.html │  │products.html│  │ cart.html │ │checkout..│ │
│  └─────┬──────┘  └──────┬─────┘  └─────┬──────┘ └────┬─────┘ │
│        │ shared CSS + shared JS modules               │      │
│        ▼                                              ▼      │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │   js/products.js   →  catalog & seed data               │ │
│  │   js/app.js        →  header, footer, theme, toasts     │ │
│  │   js/cart.js       →  cart + wishlist (localStorage)    │ │
│  │   js/checkout.js   →  multi-step checkout form          │ │
│  └─────────────────────────────────────────────────────────┘ │
│                          │                                   │
│                          ▼                                   │
│                  ┌───────────────┐                           │
│                  │ localStorage  │  (cart, wishlist, theme)  │
│                  └───────────────┘                           │
└──────────────────────────────────────────────────────────────┘
```

**Application Flow** — User lands on `index.html` → browses categories → clicks a product → lands on `product.html` → adds to cart (state persisted in `localStorage`) → opens `cart.html` → proceeds to `checkout.html`.

**Client–Server Communication** — Currently fully client-side. Plug points are exposed in `js/cart.js` (`syncCart()`) and `js/checkout.js` (`submitOrder()`) so a fetch call to a real API can be added in a single function.

**Data Relationships** — Products belong to categories. Cart items reference product IDs. Wishlist items reference product IDs. Orders (future) reference cart items + user.

---

## 📁 Project Structure

```text
shopverse/
│
├── index.html              # Home page (hero, categories, featured, testimonials)
├── products.html           # Catalog grid with filters & search
├── product.html            # Single product detail page
├── cart.html               # Shopping cart
├── checkout.html           # Multi-step checkout
├── login.html              # Login & registration screens
│
├── css/
│   ├── style.css           # Design system + components
│   └── responsive.css      # Breakpoints & mobile tweaks
│
├── js/
│   ├── app.js              # Header/footer, theme, toasts, global UI
│   ├── products.js         # Categories + product seed data
│   ├── cart.js             # Cart & wishlist state (localStorage)
│   └── checkout.js         # Checkout flow logic
│
├── screenshot/             # Marketing & README screenshots
│   ├── img1.jpeg
│   ├── img2.jpeg
│   ├── img3.jpeg
│   ├── img4.jpeg
│   └── img5.jpeg
│
├── docs/
│   └── screenshots/        # README screenshot assets
│
└── README.md
```

| Folder | Purpose |
|--------|---------|
| `css/` | Design system, components, and responsive rules |
| `js/`  | Modular vanilla-JS scripts shared across pages |
| `screenshot/` | Source imagery for marketing previews |
| `docs/` | Documentation assets used in this README |

---

## ⚙️ Installation

### Prerequisites
- A modern browser (Chrome, Edge, Firefox, Safari)
- _Optional:_ Node.js ≥ 18 (only if you want to run a local dev server)
- Git

### 1. Clone the Repository
```bash
git clone https://github.com/haribabux7/shopverse.git
cd shopverse
```

### 2. Install Dependencies
No build step is required. If you want a local dev server with live reload:
```bash
npm install -g serve
```

### 3. Configure Environment Variables
None required for the static build. If you wire in a backend, see the [Environment Variables](#-environment-variables) section.

### 4. Start the Development Server
```bash
# Option A: any static server
serve .

# Option B: Python built-in server
python -m http.server 5173

# Option C: VS Code Live Server extension → "Open with Live Server"
```

Then open `http://localhost:5173` (or whatever port your server prints).

---

## 🔐 Environment Variables

ShopVerse is static by default, but the following `.env` template is provided for future backend integrations:

```env
PORT=5173
DATABASE_URL=postgres://user:password@localhost:5432/shopverse
MONGO_URI=mongodb://localhost:27017/shopverse
JWT_SECRET=replace-with-a-long-random-string
API_KEY=your-third-party-api-key
EMAIL_HOST=smtp.mailtrap.io
EMAIL_USER=your-smtp-user
EMAIL_PASSWORD=your-smtp-password
```

| Variable | Purpose |
|----------|---------|
| `PORT` | Port the API server listens on |
| `DATABASE_URL` | Postgres connection string |
| `MONGO_URI` | MongoDB connection string (alternative) |
| `JWT_SECRET` | Secret used to sign authentication tokens |
| `API_KEY` | Third-party service credentials (payments, search, etc.) |
| `EMAIL_HOST` / `EMAIL_USER` / `EMAIL_PASSWORD` | Transactional email (orders, password reset) |

---

## 🧭 Usage

**Typical user workflow**
1. Visitor lands on the **home page**, scrolls through categories and featured items.
2. They open **Products**, refine by category, price, or search.
3. They open a **product detail page**, review specs, and add to cart or wishlist.
4. They open the **cart**, adjust quantities, and proceed to **checkout**.
5. They fill in shipping and payment details, review the order, and place it.

**Example scenarios**
- *Gift shopping:* use the wishlist to shortlist items and share the page.
- *Repeat purchase:* cart state is preserved, so returning users see the same cart.
- *Mobile commute browsing:* sticky CTAs and large tap targets make one-handed use comfortable.

**Best practices for extending**
- Keep design tokens in `css/style.css` — never hardcode colors in components.
- Co-locate page-specific logic in inline `<script>` blocks only when it's tiny; otherwise add a new `js/<page>.js`.
- All persistent state goes through helpers in `js/cart.js` to avoid stale `localStorage` reads.

---

## 🔌 API Documentation

ShopVerse currently ships without a backend, but the following REST contract is the recommended shape when one is added:

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET`  | `/api/products` | List all products (supports `?category=`, `?q=`, `?sort=`) |
| `GET`  | `/api/products/:id` | Fetch a single product by ID |
| `POST` | `/api/cart` | Create or sync a cart for the current user |
| `PUT`  | `/api/cart/:itemId` | Update quantity for a cart line |
| `DELETE` | `/api/cart/:itemId` | Remove a line from the cart |
| `POST` | `/api/orders` | Place an order (checkout) |
| `POST` | `/api/auth/login` | Authenticate a user |
| `POST` | `/api/auth/register` | Create a new account |

**Example request**
```bash
curl -X POST https://api.shopverse.dev/api/orders \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <token>" \
  -d '{"items":[{"id":1,"qty":2}],"shipping":{"city":"Bengaluru"}}'
```

**Example response**
```json
{
  "orderId": "ord_01H8X",
  "status": "confirmed",
  "total": 419.98,
  "currency": "USD"
}
```

---

## 🗃️ Database Schema

Suggested relational schema:

```text
users        (id, name, email, password_hash, created_at)
products     (id, name, category, price, old_price, rating, reviews, description, specs, image)
categories   (id, name, icon, description)
carts        (id, user_id, created_at)
cart_items   (id, cart_id, product_id, quantity)
orders       (id, user_id, status, total, shipping_json, payment_json, created_at)
order_items  (id, order_id, product_id, quantity, unit_price)
wishlists    (id, user_id, product_id)
```

**Relationships**
- `users 1—N orders`
- `orders 1—N order_items`
- `products 1—N order_items`
- `users 1—1 carts`, `carts 1—N cart_items`

---

## 🧪 Testing

### Unit Testing
```bash
npm test
```
Suggested tool: **Vitest** or **Jest** for pure helpers in `js/cart.js`.

### Integration Testing
Use **Playwright** or **Cypress** to drive the static site:
```bash
npx playwright test
```

### End-to-End Testing
Cover the critical flow: *browse → add to cart → checkout → confirmation*.

### Tools
- Vitest / Jest (unit)
- Playwright / Cypress (E2E)
- Lighthouse CI (performance budgets)

---

## 🚀 Performance Optimizations

- **Caching** — long-cache headers for `css/` and `js/` (set at host level).
- **Lazy loading** — `loading="lazy"` on non-critical images.
- **Pagination** — product grid is virtualisation-ready.
- **Query optimization** — filters operate on in-memory arrays in O(n).
- **Code splitting** — per-page scripts only load what each page needs.
- **Compression** — works with Brotli/Gzip at the CDN edge.
- **Inline SVG placeholders** — zero image network calls for previews.

---

## 🛡️ Security Features

- 🔐 **Authentication** — UI scaffolding ready; pluggable to JWT/OAuth providers.
- 🧱 **Authorization** — role-based routes ready to layer in.
- 🔑 **Password Encryption** — recommended: bcrypt or Argon2 server-side.
- 🪪 **JWT Security** — short-lived access tokens + refresh tokens.
- ✅ **Input Validation** — HTML5 + JS validation on every form.
- 🚦 **Rate Limiting** — recommended at API gateway / reverse proxy.
- 🛡️ **CSRF Protection** — use SameSite cookies + CSRF token middleware.
- 📦 **Secure API Practices** — HTTPS-only, CSP, no inline secrets.

---

## ☁️ Deployment

Because ShopVerse is static, deployment is one drag-and-drop away.

### Vercel
```bash
npx vercel
```
### Netlify
```bash
npx netlify deploy --prod
```
### Render / Railway
Create a new **Static Site** service and point it at the repo root. Build command: *(empty)*. Publish directory: `.`.

### AWS S3 + CloudFront
1. Create an S3 bucket and enable static website hosting.
2. Upload the repo contents.
3. Front the bucket with CloudFront for HTTPS + caching.

### Azure Static Web Apps
Use the Azure Static Web Apps GitHub Action template; no build step required.

### CI/CD (GitHub Actions overview)
```yaml
name: Deploy
on: { push: { branches: [main] } }
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: nwtgck/actions-netlify@v3
        with: { publish-dir: '.', production-deploy: true }
        env:
          NETLIFY_AUTH_TOKEN: ${{ secrets.NETLIFY_AUTH_TOKEN }}
          NETLIFY_SITE_ID: ${{ secrets.NETLIFY_SITE_ID }}
```

---

## 🧩 Challenges & Solutions

- **Keeping state in sync across pages** — multi-page apps lose in-memory state between navigations. Solved by centralising cart and wishlist reads/writes through a tiny module in `js/cart.js` that always re-hydrates from `localStorage`.
- **Avoiding broken product imagery** — instead of relying on external image hosts, the catalog uses an inline SVG generator (`ph()`) that produces branded placeholders at runtime — zero network requests, zero broken images.
- **Maintaining design consistency without a framework** — adopted a CSS custom-properties design system (`--color-*`, `--radius-*`, `--shadow-*`) so theme changes (including dark mode) are a one-line swap.
- **Responsive layout without a UI kit** — built a small grid + utility layer in `responsive.css` covering 4 breakpoints, validated on real devices via Chrome's responsive mode.
- **Keeping checkout forms friendly** — combined native HTML5 validation with JS-level UX (inline errors, disabled submit, toast confirmations) so users get fast feedback without heavy form libraries.

---

## 🔮 Future Improvements

1. Real backend with Node.js + Express + PostgreSQL.
2. Stripe / Razorpay checkout integration.
3. User accounts with order history.
4. Admin dashboard for product, order, and inventory CRUD.
5. Full-text product search powered by MeiliSearch or Algolia.
6. Internationalisation (i18n) with multi-currency support.
7. Progressive Web App (offline mode, installable).
8. AI-powered product recommendations.
9. Reviews & ratings with media uploads.
10. Coupon engine, gift cards, and loyalty points.
11. Email notifications for orders and shipping updates.
12. Accessibility audit pass to WCAG 2.2 AA.
13. Lighthouse performance budget enforced in CI.
14. Headless CMS integration for marketing pages.
15. End-to-end Playwright test suite in CI.

---

## 🤝 Contributing

Contributions are warmly welcomed.

1. **Fork** the repository.
2. **Create a feature branch**
   ```bash
   git checkout -b feat/your-feature
   ```
3. **Commit your changes** using conventional commits
   ```bash
   git commit -m "feat: add product quick view"
   ```
4. **Push the branch**
   ```bash
   git push origin feat/your-feature
   ```
5. **Open a Pull Request** describing the change, screenshots, and any trade-offs.

**Coding standards**
- 2-space indentation, semicolons, single quotes in JS.
- Keep functions small and named.
- No inline styles — extend the design system instead.
- Run Prettier before pushing.

---

## ❓ FAQ

**Q: Do I need Node.js to run this?**
No. Any static file server (or even opening `index.html` directly) works.

**Q: Where is product data stored?**
In `js/products.js` as a seed array. Swap it for a `fetch()` call to your API when ready.

**Q: How is the cart persisted?**
Via `localStorage`, keyed by `shopverse:cart` and `shopverse:wishlist`.

**Q: Can I use this commercially?**
Yes — it's MIT licensed.

**Q: Does it support dark mode?**
Yes, toggle from the header. Preference is remembered across visits.

**Q: How do I add a new page?**
Create `your-page.html`, link it in the header/footer in `js/app.js`, and add a per-page script under `js/` if needed.

---

## 📄 License

This project is licensed under the **MIT License** — you are free to use, modify, and distribute it with attribution.

```
MIT License © 2025 Hari Babu C H
```

---

## 👤 Author

**HARI BABU C H**

Frontend Developer | Data Analyst | Chennai, India

- 🌐 Portfolio: [https://www.haribabu.me](https://www.haribabu.me)
- 💼 LinkedIn: [https://www.linkedin.com/in/haribabux8](https://www.linkedin.com/in/haribabux8)
- 🐙 GitHub: [https://github.com/haribabux8](https://github.com/haribabux8)
- 📧 Email: [haribabuc458@gmail.com](mailto:haribabuc458@gmail.com)

---

## 🙏 Acknowledgements

- **Open Source Libraries** — Google Fonts (Inter), the broader MDN Web Docs community.
- **Contributors** — Everyone who reports issues, suggests features, or stars the repo.
- **Learning Resources** — MDN Web Docs, CSS-Tricks, web.dev, Smashing Magazine.
- **Inspiration** — Apple, Nike, Allbirds, Linear, and other brands that set the bar for digital craft.

---

