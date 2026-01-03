npx create-next-app astro-vedic
cd astro-vedic
npm install next-intl tailwindcss @headlessui/react @heroicons/react stripe
npx tailwindcss init -p

// app/[locale]/layout.tsx
import {NextIntlClientProvider} from 'next-intl';
import '../globals.css';
import Nav from '@/components/Nav';
import Footer from '@/components/Footer';

export default async function RootLayout({children, params: {locale}}) {
  const messages = (await import(`../../messages/${locale}.json`)).default;
  return (
    <html lang={locale}>
      <body className="bg-[#F5F2E7] text-[#1A2A40]">
        <NextIntlClientProvider locale={locale} messages={messages}>
          <Nav locale={locale} />
          <main className="mx-auto max-w-6xl px-6 py-10">{children}</main>
          <Footer />
        </NextIntlClientProvider>
      </body>
    </html>
  );
}

// components/Nav.tsx
import Link from 'next/link';
import {useTranslations} from 'next-intl';

npm i @vercel/analytics

export default function Nav({locale}: {locale: string}) {
  const t = useTranslations('Nav');
  const switchTo = locale === 'pt-BR' ? 'en' : locale === 'en' ? 'es' : 'pt-BR';
  return (
    <nav className="flex items-center justify-between px-6 py-4 border-b border-[#C9C9C9] bg-white">
      <Link href={`/${locale}`} className="font-semibold text-[#1A2A40]">Jyotish — Andressa</Link>
      <ul className="flex gap-6">
        <li><Link href={`/${locale}`}>{t('home')}</Link></li>
        <li><Link href={`/${locale}/consultas`}>{t('consultas')}</Link></li>
        <li><Link href={`/${locale}/sobre`}>{t('sobre')}</Link></li>
        <li><Link href={`/${locale}/contato`}>{t('contato')}</Link></li>
        <li><Link href={`/${locale}/checkout`}>Checkout</Link></li>
      </ul>
      <Link href={`/${switchTo}`} className="text-sm underline">{
        switchTo === 'pt-BR' ? 'Português' : switchTo === 'en' ? 'English' : 'Español'
      }</Link>
    </nav>
  );
} 
// components/Footer.tsx
export default function Footer() {
  return (
    <footer className="mt-16 border-t border-[#C9C9C9] bg-white">
      <div className="mx-auto max-w-6xl px-6 py-8 text-sm text-[#1A2A40]">
        <p>© {new Date().getFullYear()} Andressa — Astrologia Védica (Jyotish)</p>
        <p>WhatsApp: (92) 99161-8855 • E-mail: andressaze23@gmail.com</p>
      </div>
    </footer>
  );
} 
// app/[locale]/page.tsx
import {useTranslations} from 'next-intl';
import Link from 'next/link';

export default function Home() {
  const t = useTranslations('Home');
  return (
    <section className="space-y-6 text-center">
      <h1 className="text-4xl font-semibold text-[#1A2A40]">{t('title')}</h1>
      <p className="text-lg text-[#1A2A40]">{t('subtitle')}</p>
      <p className="max-w-3xl mx-auto text-[#1A2A40]">{t('inspire')}</p>
      <Link href="./consultas" className="inline-block bg-[#1A2A40] text-white px-6 py-3 rounded hover:bg-[#D4AF37] hover:text-[#1A2A40] transition">
        {t('cta')}
      </Link>
    </section>
  );
} 
// messages/pt-BR.json (Home + Nav)
{
  "Nav": {
    "home": "Início",
    "consultas": "Consultas",
    "sobre": "Sobre",
    "contato": "Contato"
  },
  "Home": {
    "title": "Astrologia Védica — a ciência da luz aplicada à sua vida",
    "subtitle": "Sou Andressa, astróloga védica. Minha missão é iluminar o caminho da vida, ajudando você a compreender o Karma, o propósito e o destino.",
    "inspire": "Cada mapa védico é como uma estrela única no céu, revelando ciclos, aprendizados e oportunidades que guiam sua jornada. Através da sabedoria ancestral do Jyotish, você pode enxergar com mais clareza os desafios e descobrir caminhos que fortalecem sua essência e alinham sua vida ao propósito maior.",
    "cta": "Solicitar consulta escrita"
  }
}
// messages/en.json (Home + Nav)
{
  "Nav": {
    "home": "Home",
    "consultas": "Sessions",
    "sobre": "About",
    "contato": "Contact"
  },
  "Home": {
    "title": "Vedic Astrology — the science of light applied to your life",
    "subtitle": "I’m Andressa, a Vedic astrologer. My mission is to illuminate the path of life, guiding you to understand Karma, purpose, and destiny.",
    "inspire": "Every Vedic chart is like a unique star in the sky, revealing cycles, lessons, and opportunities that guide your journey. Through the ancient wisdom of Jyotish, you can see challenges with greater clarity and discover paths that strengthen your essence while aligning your life with a higher purpose.",
    "cta": "Request written consultation"
  }
}
// messages/es.json (Home + Nav)
{
  "Nav": {
    "home": "Inicio",
    "consultas": "Consultas",
    "sobre": "Sobre mí",
    "contato": "Contacto"
  },
  "Home": {
    "title": "Astrología Védica — la ciencia de la luz aplicada a tu vida",
    "subtitle": "Soy Andressa, astróloga védica. Mi misión es iluminar el camino de la vida, ayudándote a comprender el Karma, el propósito y el destino.",
    "inspire": "Cada carta védica es como una estrella única en el cielo, revelando ciclos, aprendizajes y oportunidades que guían tu viaje. A través de la sabiduría ancestral del Jyotish, puedes ver con mayor claridad los desafíos y descubrir caminos que fortalecen tu esencia y alinean tu vida con un propósito superior.",
    "cta": "Solicitar consulta escrita"
  }
}
// app/[locale]/consultas/page.tsx
import {useTranslations} from 'next-intl';
import Link from 'next/link';

export default function Consultas() {
  const t = useTranslations('Consultas');
  return (
    <section className="space-y-6">
      <h1 className="text-3xl font-semibold">{t('title')}</h1>
      <div className="border rounded p-6 bg-white space-y-3">
        <h2 className="text-xl font-medium">{t('written.title')}</h2>
        <p>{t('written.desc')}</p>
        <p className="font-semibold">{t('price')}</p>
        <Link href="../checkout" className="inline-block bg-[#1A2A40] text-white px-6 py-3 rounded hover:bg-[#D4AF37] hover:text-[#1A2A40] transition">
          {t('cta')}
        </Link>
      </div>
    </section>
  );
}
// messages/pt-BR.json (Consultas)
{
  "Consultas": {
    "title": "Consultas védicas",
    "written": {
      "title": "Consulta Escrita",
      "desc": "Você envia seus dados de nascimento (data, hora e local). Eu realizo a análise completa do mapa védico e envio um relatório detalhado por e-mail.",
      "delivery": "Prazo de entrega: até 3 dias úteis."
    },
    "price": "Valor: R$50,00",
    "cta": "Ir para checkout"
  }
}
// messages/en.json (Consultas)
{
  "Consultas": {
    "title": "Vedic sessions",
    "written": {
      "title": "Written Consultation",
      "desc": "You provide your birth details (date, time, place). I prepare a full Vedic chart analysis and deliver a detailed report by email.",
      "delivery": "Delivery time: up to 3 business days."
    },
    "price": "Price: $10 USD (approx.)",
    "cta": "Go to checkout"
  }
} 
// messages/es.json (Consultas)
{
  "Consultas": {
    "title": "Consultas védicas",
    "written": {
      "title": "Consulta Escrita",
      "desc": "Envías tus datos de nacimiento (fecha, hora y lugar). Realizo el análisis completo de la carta védica y envío un informe detallado por correo electrónico.",
      "delivery": "Plazo de entrega: hasta 3 días hábiles."
    },
    "price": "Precio: 10 USD (aprox.)",
    "cta": "Ir al checkout"
  }
}
// app/[locale]/checkout/page.tsx
import {useTranslations} from 'next-intl';

export default function Checkout() {
  const t = useTranslations('Checkout');
  return (
    <section className="space-y-6">
      <h1 className="text-3xl font-semibold">{t('title')}</h1>
      <form className="grid gap-4 bg-white p-6 rounded border">
        <label className="grid gap-1">
          <span>{t('name')}</span>
          <input className="border rounded px-3 py-2" required />
        </label>
        <label className="grid gap-1">
          <span>{t('email')}</span>
          <input type="email" className="border rounded px-3 py-2" required />
        </label>
        <label className="grid gap-1">
          <span>{t('birth')}</span>
          <textarea className="border rounded px-3 py-2" placeholder={t('birthPlaceholder')} required />
        </label>
        <div>
          <span className="font-semibold">{t('methodsTitle')}</span>
          <ul className="list-disc ml-6">
            <li>Stripe (Cartão de Crédito/Débito)</li>
            <li>PayPal</li>
            <li>Pix (Brasil)</li>
          </ul>
        </div>
        <button className="bg-[#1A2A40] text-white px-6 py-3 rounded hover:bg-[#D4AF37] hover:text-[#1A2A40] transition">
          {t('pay')}
        </button>
        <p className="text-sm text-[#1A2A40]">{t('refund')}</p>
      </form>
    </section>
  );
}
// messages/pt-BR.json (Checkout)
{
  "Checkout": {
    "title": "Checkout",
    "name": "Nome completo",
    "email": "E-mail",
    "birth": "Dados de nascimento",
    "birthPlaceholder": "Data, hora e local de nascimento",
    "methodsTitle": "Formas de pagamento",
    "pay": "Pagar R$50,00",
    "refund": "Política de reembolso: cancelamentos antes da análise têm reembolso integral; após o início da análise, reembolso de 50%; após o envio do relatório, não há reembolso."
  }
}
// messages/en.json (Checkout)
{
  "Checkout": {
    "title": "Checkout",
    "name": "Full name",
    "email": "Email",
    "birth": "Birth details",
    "birthPlaceholder": "Date, time, and place of birth",
    "methodsTitle": "Payment methods",
    "pay": "Pay $10 USD",
    "refund": "Refund policy: cancellations before analysis receive a full refund; after analysis starts, 50% refund; after report delivery, no refund."
  }
}
// messages/es.json (Checkout)
{
  "Checkout": {
    "title": "Checkout",
    "name": "Nombre completo",
    "email": "Correo electrónico",
    "birth": "Datos de nacimiento",
    "birthPlaceholder": "Fecha, hora y lugar de nacimiento",
    "methodsTitle": "Métodos de pago",
    "pay": "Pagar 10 USD",
    "refund": "Política de reembolso: cancelaciones antes del análisis reciben reembolso total; después de iniciar el análisis, 50% de reembolso; después del envío del informe, no hay reembolso."
  }
}
// app/[locale]/sobre/page.tsx
import {useTranslations} from 'next-intl';

export default function Sobre() {
  const t = useTranslations('Sobre');
  return (
    <section className="space-y-4">
      <h1 className="text-3xl font-semibold">{t('title')}</h1>
      <p>{t('bio')}</p>
      <p>{t('ethics')}</p>
    </section>
  );
}
// messages/pt-BR.json (Sobre + Contato)
{
  "Sobre": {
    "title": "Sobre Andressa",
    "bio": "Astróloga védica, iluminar o caminho da vida, ajudando a entender o Karma, propósito e destino.",
    "ethics": "Sem fatalismo. Leituras com ética, clareza e recomendações práticas (upayas)."
  },
  "Contato": {
    "title": "Contato",
    "whatsapp": "WhatsApp / Telefone: (92) 99161-8855",
    "email": "E-mail: andressaze23@gmail.com",
    "form": "Envie seus dados de nascimento e mensagem pelo formulário."
  }
}
// app/[locale]/contato/page.tsx
import {useTranslations} from 'next-intl';

export default function Contato() {
  const t = useTranslations('Contato');
  return (
    <section className="space-y-6">
      <h1 className="text-3xl font-semibold">{t('title')}</h1>
      <p>{t('whatsapp')}</p>
      <p>{t('email')}</p>
      <form className="grid gap-4 bg-white p-6 rounded border">
        <input className="border rounded px-3 py-2" placeholder="Nome" required />
        <textarea className="border rounded px-3 py-2" placeholder="Dados de nascimento (data, hora, local)" required />
        <textarea className="border rounded px-3 py-2" placeholder="Mensagem" required />
        <button className="bg-[#1A2A40] text-white px-6 py-3 rounded hover:bg-[#D4AF37] hover:text-[#1A2A40] transition">
          Enviar
        </button>
      </form>
    </section>
  );
}
// tailwind.config.js
module.exports = {
  content: ['./app/**/*.{ts,tsx}', './components/**/*.{ts,tsx}'],
  theme: { extend: {} },
  plugins: []
};
/* app/globals.css */
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

body { background: var(--beige); color: var(--deep-blue); }
// lib/payments.ts (exemplo de placeholder)
export const STRIPE_CHECKOUT_URL = 'https://buy.stripe.com/SEU_LINK';
export const PAYPAL_CHECKOUT_URL = 'https://www.paypal.com/SEU_LINK';
export const PIX_INFO = 'Envie o comprovante do Pix para andressaze23@gmail.com';







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
  "version": "1.0.0"
 
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

git add . && git commit -m "fix: add next dependency" && git push

// app/[locale]/checkout/page.tsx
import {useTranslations} from 'next-intl';
import Link from 'next/link';
import {PAYPAL_LINK, PIX_INFO} from '@/lib/payments';

export default function Checkout() {
  const t = useTranslations('Checkout');
  return (
    <section className="space-y-6">
      <h1 className="text-3xl font-semibold">{t('title')}</h1>
      <form className="grid gap-4 bg-white p-6 rounded border">
        <label className="grid gap-1">
          <span>{t('name')}</span>
          <input className="border rounded px-3 py-2" required />
        </label>
        <label className="grid gap-1">
          <span>{t('email')}</span>
          <input type="email" className="border rounded px-3 py-2" required />
        </label>
        <label className="grid gap-1">
          <span>{t('birth')}</span>
          <textarea className="border rounded px-3 py-2" placeholder={t('birthPlaceholder')} required />
        </label>

        <div className="space-y-2">
          <span className="font-semibold">{t('methodsTitle')}</span>
          <div className="grid md:grid-cols-2 gap-3">
            <Link href={PAYPAL_LINK} className="text-center bg-[#1A2A40] text-white px-6 py-3 rounded hover:bg-[#D4AF37] hover:text-[#1A2A40] transition">
              {t('payPaypal')}
            </Link>
            <button type="button" className="text-center bg-white border border-[#1A2A40] text-[#1A2A40] px-6 py-3 rounded hover:border-[#D4AF37] transition"
              onClick={() => alert(PIX_INFO)}>
              {t('payPix')}
            </button>
          </div>
          <p className="text-sm text-[#1A2A40]">{t('pixNote')}</p>
        </div>

        <p className="text-sm text-[#1A2A40]">{t('refund')}</p>
      </form>
    </section>
  );
}
// lib/payments.ts
export const PAYPAL_LINK = 'https://www.paypal.com/paypalme/andressaze23'; // opção 1: PayPal.Me
// Se preferir botão padrão, use: https://www.paypal.com/donate/?business=andressaze23%40gmail.com&no_recurring=0&currency_code=BRL
export const PIX_INFO = 'Faça um Pix para a chave 92991618855 e envie o comprovante para andressaze23@gmail.com';

// messages/pt-BR.json (Checkout)
{
  "Checkout": {
    "title": "Checkout",
    "name": "Nome completo",
    "email": "E-mail",
    "birth": "Dados de nascimento",
    "birthPlaceholder": "Data, hora e local de nascimento",
    "methodsTitle": "Formas de pagamento",
    "payPaypal": "Pagar com PayPal",
    "payPix": "Pagar com Pix",
    "pixNote": "Após o Pix, envie o comprovante para andressaze23@gmail.com. Você receberá confirmação por e-mail.",
    "refund": "Política de reembolso: cancelamentos antes da análise têm reembolso integral; após o início da análise, reembolso de 50%; após o envio do relatório, não há reembolso."
  }
}
// messages/en.json (Checkout)
{
  "Checkout": {
    "title": "Checkout",
    "name": "Full name",
    "email": "Email",
    "birth": "Birth details",
    "birthPlaceholder": "Date, time, and place of birth",
    "methodsTitle": "Payment methods",
    "payPaypal": "Pay with PayPal",
    "payPix": "Pay with Pix",
    "pixNote": "After Pix payment, send the receipt to andressaze23@gmail.com. You’ll receive confirmation by email.",
    "refund": "Refund policy: cancellations before analysis receive a full refund; after analysis starts, 50% refund; after report delivery, no refund."
  }
}
// messages/es.json (Checkout)
{
  "Checkout": {
    "title": "Checkout",
    "name": "Nombre completo",
    "email": "Correo electrónico",
    "birth": "Datos de nacimiento",
    "birthPlaceholder": "Fecha, hora y lugar de nacimiento",
    "methodsTitle": "Métodos de pago",
    "payPaypal": "Pagar con PayPal",
    "payPix": "Pagar con Pix",
    "pixNote": "Después del pago por Pix, envía el comprobante a andressaze23@gmail.com. Recibirás confirmación por correo.",
    "refund": "Política de reembolso: cancelaciones antes del análisis reciben reembolso total; después de iniciar el análisis, 50% de reembolso; después del envío del informe, no hay reembolso."
  }
}

import { Analytics } from "@vercel/analytics/next"

vercel --prod
vercel env pull

npm install @vercel/edge-config

import { NextResponse } from 'next/server';
import { get } from '@vercel/edge-config';

export const config = { matcher: '/welcome' };

export async function middleware() {
  const greeting = await get('greeting');
  // NextResponse.json requires at least Next v13.1 or
  // enabling experimental.allowMiddlewareResponseBody in next.config.js
  return NextResponse.json(greeting);
} 
{
  "greeting": "hello world"
}

{
  "name": "astro-vedic",
  "version": "1.0.0",
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start"
  },
  "dependencies": {
    "next": "14.0.0",
    "react": "18.2.0",
    "react-dom": "18.2.0",
    "next-intl": "^3.0.0",
    "tailwindcss": "^3.3.0"
  }
}
npm install next react react-dom
yarn add next react react-dom






