
mkdir astro-vedic && cd astro-vedic


git init


├─ app/
│  ├─ [locale]/
│  │  ├─ layout.tsx
│  │  ├─ page.tsx
│  │  ├─ consultas/page.tsx
│  │  ├─ sobre/page.tsx
│  │  ├─ contato/page.tsx
│  │  └─ checkout/page.tsx
│  └─ globals.css
├─ components/
│  ├─ Nav.tsx
│  ├─ Footer.tsx
│  └─ Card.tsx
├─ messages/
│  ├─ pt-BR.json
│  ├─ en.json
│  └─ es.json
├─ lib/
│  └─ payments.ts
├─ public/
│  └─ logo.svg
├─ tailwind.config.js
├─ package.json
└─ README.md
 {
  "name": "astro-vedic",
  "version": "1.0.0",
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start"
 
}
 module.exports = {
  content: ['./app/**/*.{ts,tsx}', './components/**/*.{ts,tsx}'],
  theme: {
    extend: {}
  },
  plugins: []
};
 @tailwind base;
@tailwind components;
@tailwind utilities;

:root {
  --gold: #D4AF37;
  --deep-blue: #1A2A40;
  --beige: #F5F2E7;
  --soft-gray: #C9C9C9;
  --soft-pink: #E8C6C6;
}
npm install next react react-dom

body {
  background: var(--beige);
  color: var(--deep-blue);
}
 {
  "Home": {
    "title": "Astrologia Védica — a ciência da luz aplicada à sua vida",
    "subtitle": "Sou Andressa, astróloga védica. Minha missão é iluminar o caminho da vida, ajudando você a compreender o Karma, o propósito e o destino.",
    "inspire": "Cada mapa védico é como uma estrela única no céu, revelando ciclos, aprendizados e oportunidades que guiam sua jornada.",
    "cta": "Solicitar consulta escrita"
  }
}
 {
  "Home": {
    "title": "Vedic Astrology — the science of light applied to your life",
    "subtitle": "I’m Andressa, a Vedic astrologer. My mission is to illuminate the path of life, guiding you to understand Karma, purpose, and destiny.",
    "inspire": "Every Vedic chart is like a unique star in the sky, revealing cycles, lessons, and opportunities that guide your journey.",
    "cta": "Request written consultation"
  }
}
 {
  "Home": {
    "title": "Astrología Védica — la ciencia de la luz aplicada a tu vida",
    "subtitle": "Soy Andressa, astróloga védica. Mi misión es iluminar el camino de la vida, ayudándote a comprender el Karma, el propósito y el destino.",
    "inspire": "Cada carta védica es como una estrella única en el cielo, revelando ciclos, aprendizajes y oportunidades que guían tu viaje.",
    "cta": "Solicitar consulta escrita"
  }
}
)


git add .
git commit -m "Primeira versão do site Jyotish"

git remote add origin https://github.com/andressaze23-png/vedic-astro.git

git push -u origin main

