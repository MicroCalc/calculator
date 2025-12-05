# MicroCalc - Free Online Calculator Hub

MicroCalc is a comprehensive online calculator hub featuring 40+ calculators for finance, health, math, dates, and more. Built with Next.js 14, TypeScript, and Tailwind CSS for a fast, SEO-optimized, and beautiful user experience.

![MicroCalc](./public/og-image.png)

## ✨ Features

- **40+ Calculators** - Finance, health, math, dates, converters, and more
- **10 Fully Implemented** - Mortgage, Loan, Auto Loan, BMI, Age, Date, Salary (BD), Fuel Cost, Compound Interest, Scientific
- **SEO Optimized** - Server-side rendering, JSON-LD schemas, sitemap, meta tags
- **Dark Mode** - System-aware theme with manual toggle
- **Mobile First** - Responsive design that works on all devices
- **Embed Widgets** - Free iframe widgets for external sites
- **No Database** - JSON-based calculator specs for easy customization
- **TypeScript** - Fully typed codebase
- **Tested** - Unit tests for all implemented calculators

## 🚀 Quick Start

### Prerequisites

- Node.js 18.0.0 or higher
- npm, yarn, or pnpm

### Installation

```bash
# Clone the repository
git clone https://github.com/your-username/microcalc.git
cd microcalc

# Install dependencies
npm install
# or
pnpm install
# or
yarn install

# Start development server
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) to see the app.

### Build for Production

```bash
npm run build
npm run start
```

## 📁 Project Structure

```
microcalc/
├── app/                    # Next.js App Router pages
│   ├── page.tsx           # Homepage
│   ├── calculators/       # Calculator pages
│   │   └── [slug]/        # Dynamic calculator routes
│   ├── category/          # Category pages
│   │   └── [slug]/
│   ├── embed/             # Embeddable widget pages
│   │   └── [slug]/
│   ├── api/               # API routes
│   │   └── preview/       # Calculator preview API
│   ├── privacy/           # Legal pages
│   ├── terms/
│   └── tools/
│       └── embed-directory/
├── components/            # React components
│   ├── calculator/        # Calculator-specific components
│   ├── layout/            # Header, Footer
│   ├── providers/         # Context providers
│   ├── search/            # Search modal
│   ├── seo/               # JSON-LD components
│   └── ads/               # Ad placeholder
├── data/
│   └── calculators/       # Calculator JSON specs (40+ files)
├── lib/                   # Utilities
│   ├── calculators.ts     # Calculator loading functions
│   ├── constants.ts       # Categories, config
│   └── formulas.ts        # Calculator logic (10 implemented)
├── locales/               # i18n translations
│   ├── en.json
│   └── bn.json
├── types/                 # TypeScript types
├── __tests__/             # Unit tests
└── public/                # Static assets
```

## 🔧 Configuration

### Environment Variables

Create a `.env.local` file:

```env
# Site URL (required for SEO)
NEXT_PUBLIC_SITE_URL=https://microcalc.app
NEXT_PUBLIC_SITE_NAME=MicroCalc

# Google Analytics 4 (optional)
NEXT_PUBLIC_GA4_MEASUREMENT_ID=G-XXXXXXXXXX

# Google AdSense (optional)
NEXT_PUBLIC_ADSENSE_PUBLISHER_ID=ca-pub-XXXXXXXXXXXXXXXX

# Google Search Console (optional)
NEXT_PUBLIC_GOOGLE_SITE_VERIFICATION=your-verification-code
```

### Google Analytics Setup

1. Create a GA4 property at [analytics.google.com](https://analytics.google.com)
2. Get your Measurement ID (G-XXXXXXXXXX)
3. Add to `.env.local`
4. Rebuild the app

### Google AdSense Setup

1. Apply at [google.com/adsense](https://www.google.com/adsense)
2. Get approved and create ad units
3. Add Publisher ID to `.env.local`
4. Update `AdPlaceholder.tsx` with actual AdSense code

### Google Search Console

1. Go to [search.google.com/search-console](https://search.google.com/search-console)
2. Add your property
3. Choose HTML tag verification
4. Add the content value to `NEXT_PUBLIC_GOOGLE_SITE_VERIFICATION`
5. Submit your sitemap: `https://yoursite.com/sitemap.xml`

## 🧮 Adding New Calculators

### 1. Create Calculator Spec

Create a new JSON file in `data/calculators/`:

```json
{
  "slug": "my-calculator",
  "title": "My Calculator",
  "category": "math",
  "description": "Short description",
  "introduction": "Longer intro (100-200 words)",
  "inputs": [
    {
      "id": "value1",
      "label": "First Value",
      "type": "number",
      "defaultValue": 100,
      "validation": { "required": true, "min": 0 }
    }
  ],
  "outputs": [
    {
      "id": "result",
      "label": "Result",
      "format": "number",
      "highlight": true
    }
  ],
  "formula": {
    "description": "Formula explanation",
    "formula": "Result = Value1 * 2"
  },
  "formulaId": "myCalculator",
  "faq": [
    {
      "question": "How does this work?",
      "answer": "It doubles your input."
    }
  ],
  "seo": {
    "title": "My Calculator - SEO Title",
    "description": "SEO meta description"
  },
  "isImplemented": false
}
```

### 2. Add to Calculator Registry

Update `lib/calculators.ts` to import the new spec.

### 3. Implement Formula (Optional)

Add logic to `lib/formulas.ts`:

```typescript
export function calculateMyCalculator(inputs: Record<string, number | string>): CalculatorResult {
  const value1 = Number(inputs.value1) || 0
  return {
    success: true,
    outputs: {
      result: value1 * 2,
    },
  }
}

// Add to FORMULA_REGISTRY
export const FORMULA_REGISTRY = {
  // ... existing formulas
  myCalculator: calculateMyCalculator,
}
```

Set `isImplemented: true` in the spec.

## 🌍 Localization

The app is prepared for i18n with translation files in `/locales`.

### Adding a New Language

1. Copy `locales/en.json` to `locales/[lang].json`
2. Translate all strings
3. Update components to use the translations

For full i18n with URL prefixes, consider adding `next-intl` or `next-i18next`.

## 🧪 Testing

```bash
# Run tests
npm run test

# Run tests with coverage
npm run test:coverage

# Run tests once (CI)
npm run test:run
```

## 🚀 Deployment

### Deploy to Vercel

1. Push your code to GitHub
2. Import the repository at [vercel.com/new](https://vercel.com/new)
3. Add environment variables
4. Deploy!

Or use the Vercel CLI:

```bash
npm i -g vercel
vercel
```

### Manual Deployment

```bash
npm run build
# Deploy the `.next` folder to your hosting
```

## 📊 Future Enhancements

### Database Integration

To add PostgreSQL:

1. Install Prisma: `npm install prisma @prisma/client`
2. Initialize: `npx prisma init`
3. Define schema for calculator usage analytics
4. Migrate: `npx prisma migrate dev`

### User Accounts

Consider adding:
- NextAuth.js for authentication
- Save calculation history
- Custom calculator preferences
- Premium features

### Additional Features

- [ ] Calculation history (localStorage)
- [ ] Compare multiple scenarios
- [ ] Export to Excel/PDF
- [ ] API for third-party integrations
- [ ] More calculator implementations

## 📄 License

MIT License - feel free to use for personal or commercial projects.

## 🤝 Contributing

Contributions welcome! Please:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## 📧 Contact

For questions, suggestions, or partnership inquiries, please open an issue or contact us through the website.

---

Built with ❤️ using Next.js, TypeScript, and Tailwind CSS

