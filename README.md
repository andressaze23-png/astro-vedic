
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







