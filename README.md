# Alfa Gems World — e-commerce storefront starter

A responsive storefront prototype for Alfa Gems World with gemstone categories, product search/filter/sort, product detail dialogs, cart, WhatsApp order enquiry, and a browser-local product manager with CSV import/export.

## Important limitations

This is a **front-end starter**, not a production-ready transactional e-commerce backend. The demo product manager uses `localStorage`, so changes only persist in the current browser/device. There is no secure administrator authentication, shared database, live stock reservation, customer order database, payment processing, payment verification, or courier integration. The checkout button creates a WhatsApp enquiry; it does **not** confirm an order or collect payment.

Do not enter real customer personal information into a public demo. Do not claim an order is paid until a payment gateway verifies it server-side.

## Run locally

Open `index.html` in a browser, or serve this folder with any static web server. No build step is required.

## Publish free on GitHub Pages

1. Create/sign in to a GitHub account.
2. Create a public repository named `alfagemsworld` (or another available name).
3. Upload all files from this folder to the repository root.
4. In repository **Settings → Pages**, choose deployment from the `main` branch and `/ (root)`.
5. Wait for the deployment URL shown in Pages settings. A typical URL format is `https://YOUR-USERNAME.github.io/alfagemsworld/`; the exact username and URL depend on your account and repository.
6. Test the website on a phone and desktop.

GitHub Pages is static hosting only. The local demo admin is visible to visitors and is not secure. Remove/disable it before public launch, or replace it with authenticated server-side administration.

## Product catalogue

- Use **Admin demo** to add/edit/delete products in this browser only.
- Use **Export products CSV** to save a copy.
- Import a CSV with columns: `id,name,category,sku,price,weight,description,stock,featured,image,certified`.
- Image URL must be a public HTTPS image URL. For a production store, use managed object storage and validate uploads.

Sample product entries are illustrative placeholders. Verify actual prices, stock, weights, units (per piece vs per carat), origin, treatments, and certificates before making listings public.

## Recommended production architecture

- Static storefront: GitHub Pages, Netlify, or another provider whose current terms fit your use.
- Database/authentication: Supabase or another managed database with Row Level Security and server-side authorization.
- Server-side payment functions: a trusted serverless backend or payment gateway integration.
- Payment gateway: apply for a merchant account and follow current gateway documentation. Keep secret keys only in server-side secrets.
- Order creation: server validates current product prices and stock, writes a pending order, then creates a gateway payment order.
- Payment confirmation: verify signed gateway webhook and payment/order IDs server-side; only then mark paid.
- Admin: authenticated users only, with database policies restricting product/order management to authorized staff.
- Customer data: minimize collection, protect access, define retention, and publish accurate policies.

## Production payment flow checklist

1. Create a merchant account with a supported gateway and complete any required verification.
2. Add public gateway key to frontend only if the provider explicitly documents it as public; store secret keys in server-side environment secrets.
3. Server reads product IDs and quantities from the cart and fetches prices from the database. Never trust browser-supplied totals.
4. Server creates a pending order and gateway payment order.
5. Browser opens the provider checkout.
6. Server verifies payment signature / webhook authenticity and checks the captured/paid status using the provider's documented process.
7. Update order payment status idempotently and notify customer.
8. Test successful, failed, cancelled, duplicate-webhook, refund, and out-of-stock cases in sandbox before production.

Never request or store a customer's UPI PIN. A screenshot or return-to-site redirect alone is not proof of payment.

## Before launch

- Replace sample products and prices with verified stock data.
- Add actual product photographs and accurate product details.
- Add secure database and admin login.
- Integrate server-side payment verification.
- Finalize shipping, refund, cancellation, privacy and terms policies.
- Test mobile checkout, accessibility, SEO, links, error cases, and backups.
