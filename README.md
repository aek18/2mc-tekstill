# 2MC Studio · Premium T-Shirt Shop

Avrupa standartlarında, **canlı mockup** özellikli online tişört mağazası.
`frontend-developer.md` spesifikasyonuna göre kuruldu.

## Stack

- Next.js 15 (App Router, RSC varsayılan)
- TypeScript strict
- TailwindCSS + shadcn-style primitives + Radix UI
- Zustand (cart, customizer state)
- Tanstack Query (provider hazır)
- next-themes (dark mode)
- Framer Motion + lucide-react

## Çalıştırma

```bash
cd tshirt-shop
npm install
npm run dev
```

`http://localhost:3000`

```bash
npm run typecheck    # tsc --noEmit
npm run build
npm run start
```

## Sayfalar

| Route | Dosya | Açıklama |
| --- | --- | --- |
| `/` | `src/app/page.tsx` | Hero + öne çıkanlar + value-props |
| `/products` | `src/app/products/page.tsx` | Tüm ürünler grid |
| `/products/[slug]` | `src/app/products/[slug]/page.tsx` | Ürün detayı + canlı customizer |
| `/customize` | `src/app/customize/page.tsx` | Boş tasarım stüdyosu |
| `/cart` | `src/app/cart/page.tsx` | KDV ayrıştırılmış sepet özeti |

## Canlı Mockup

Çekirdek bileşen: `src/components/customizer/tshirt-mockup.tsx`

- SVG ile çizilmiş tişört (önyüz/arkayüz farklı yaka eğrileri)
- `colorHex` propu ile renk anlık değişiyor
- `design.text` üzerinde **drag-to-position** (pointer events, baskı alanına clamp)
- Yazı tipi (display/sans/serif), font boyutu, rotasyon, metin rengi
- Baskı alanı (kesikli kılavuz) `showPrintArea` ile açılır
- Fabric noise filtresi (`feTurbulence`) ile kumaş dokusu

State: `src/stores/customizer.ts` (Zustand). UI: `customizer-panel.tsx`.

## Avrupa Standardı Notlar

- Fiyatlar **EUR**, KDV **dahil** (`Intl.NumberFormat('de-DE')`)
- Sepet özetinde KDV ayrıştırması (`vatBreakdown`)
- 14 gün iade, SSL ödeme, GDPR uyumlu cookie banner
- i18n hazır (`src/lib/i18n.ts`) — TR doldurulmuş, EN/DE/FR genişletilebilir
- GOTS / OEKO-TEX / GRS / Fair Wear sertifikaları PDP'de
- Üretim yeri (Country of Origin) PDP'de görünür

## Mimari Kurallar (frontend-developer.md uyumu)

- Server Component varsayılan; `use client` sadece interaktivitede (customizer, cart, theme, cookie)
- `any` yok, prop tipleri açık
- Erişilebilirlik: `radiogroup` rolleri, `aria-checked`, focus ring, `aria-busy`/`aria-live`
- Mobile-first responsive (`sm:`, `md:`, `lg:`)
- Hardcoded string yerine `t(key)`
- `loading.tsx`, `error.tsx`, `not-found.tsx` mevcut

## Genişletme Önerileri

- Server Action ile gerçek checkout (Stripe entegrasyonu — `payment-integrator.md`)
- Supabase ile ürün/sipariş datası (`supabase-specialist.md`)
- next-intl ile gerçek çoklu dil (`localization-expert.md`)
- Görsel upload (logo) — Konva/fabric.js ile zengin canvas editörü
- 3D tişört (react-three-fiber) — premium tier
