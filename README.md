# Kawanzaa Store — متجر React حديث مع RTL

واجهة متجر عربية حديثة مبنية بـ React 18 وTypeScript وTailwind وshadcn UI. تدعم RTL بالكامل، وتتضمن عربة تسوق، سداد تجريبي، صفحة طلبات، إعدادات، وتحسينات تجربة مستخدم مثل شريط إعلان، روابط مستودع سريعة، وحارس بصري لإخفاء خطوط العرض الشاذة.

- الإطار: React 18 + TypeScript
- البناء: esbuild
- التوجيه: react-router مع HashRouter (مناسب لكل الاستضافات الثابتة)
- الأنماط: Tailwind CSS + shadcn UI
- الأيقونات: lucide-react
- الحالة: Zustand
- التنبيهات: sonner

---

## المزايا الرئيسية

- RTL كامل وتجربة عربية افتراضية.
- عربة تسوق مع شاشة سداد تجريبية (Checkout Dialog).
- قائمة منتجات وبطاقات منتج جذابة.
- صفحة الطلبات (Orders) مع حالة فارغة أنيقة.
- صفحة الإعدادات (Settings) لتخصيصات أساسية.
- شريط إعلان علوي قابل للتخصيص.
- روابط سريعة إلى المستودع (RepoQuickLinks).
- اختصار عائم لصفحة مساعد GitHub.
- حارس بصري VisualGuard لإخفاء خطوط عمودية سوداء تظهر أحيانًا بسبب إضافات أو CSS خارجي:
  - تفعيل/تعطيل عبر Alt+Shift+V
  - يعمل تلقائيًا ويعرض تنبيهًا عند الإخفاء.

---

## نظرة تقنية سريعة

- نقطة الدخول: `src/main.tsx`
- الراوتر الرئيسي: `src/App.tsx`
- صفحات:
  - `src/pages/Home.tsx` — الصفحة الرئيسية (غير فارغة)
  - `src/pages/Orders.tsx` — الطلبات
  - `src/pages/Settings.tsx` — الإعدادات
  - `src/pages/GitHubWizard.tsx` — مساعد إعداد GitHub (اختياري)
- مكونات UI رئيسية:
  - `src/components/Navbar.tsx` — شريط علوي متجاوب
  - `src/components/AnnouncementBar.tsx` — شريط إعلان
  - `src/components/ProductList.tsx` + `src/components/ProductCard.tsx`
  - `src/components/CartSheet.tsx` — سلة جانبية
  - `src/components/checkout/CheckoutDialog.tsx`
  - `src/components/Hero.tsx` + `src/components/HeroProductRibbon.tsx`
  - `src/components/RepoQuickLinks.tsx` ، `src/components/FloatingShortcut.tsx`
  - `src/components/VisualGuard.tsx`
- الحالة:
  - `src/stores/cart.ts`, `src/stores/orders.ts`, `src/stores/settings.ts`, `src/stores/ui.ts`, `src/stores/auth.ts`
- البيانات/الأنواع:
  - `src/data/products.ts`, `src/types/product.ts`, `src/types/order.ts`

ملاحظة: عند استخدام زر shadcn UI مع `variant="outline"` يجب إضافة `bg-transparent` في `className` للحفاظ على الشكل البصري المتسق.

---

## المتطلبات

- Node.js 18 أو أحدث
- npm 9+ (أو pnpm/yarn إن رغبت)

---

## التشغيل محليًا

1) تثبيت الاعتمادات:
```bash
npm install
```

2) تشغيل بيئة التطوير:
```bash
npm run dev
```
- سيبدأ سيرفر التطوير عبر esbuild.
- الراوتر يستخدم `HashRouter` لذلك الروابط تعمل مباشرة بدون إعدادات إعادة توجيه.

3) بناء النسخة الإنتاجية:
```bash
npm run build
```
- ينتج مجلد `dist/` (قابل للرفع على أي استضافة ملفات ثابتة).

---

## النشر (Hosting)

نظرًا لاستخدام `HashRouter`، يمكن نشر الموقع كملفات ثابتة بدون أي إعادة كتابة لمسارات.

خيارات سريعة:
- Netlify Drop: اسحب مجلد `dist` إلى https://app.netlify.com/drop
- Cloudflare Pages: أنشئ مشروعًا واختر "Upload assets" ثم ارفع محتويات `dist`.
- Vercel / Netlify / Cloudflare Pages (من Git): 
  - أمر البناء: `npm run build`
  - دليل الإخراج: `dist`

روابط نظيفة بدون `#`؟
- إن رغبت بالتحول إلى `BrowserRouter` لاحقًا، أضف قواعد إعادة كتابة:
  - Netlify: ملف `_redirects` يحتوي على: `/*  /index.html  200`
  - Vercel/Cloudflare: تفعيل SPA fallback لـ `index.html`

---

## اختصارات ولوائح UX

- VisualGuard:
  - تفعيل/تعطيل: Alt + Shift + V
  - يعالج تلقائيًا “الخط العمودي الأسود” الضيق الذي قد يظهر بفعل CSS خارجي.
- التنبيهات: sonner تعمل باتجاه RTL افتراضيًا من الجذر في `App.tsx`.

---

## بنية المجلدات

```
src/
  components/
    announcement/
    checkout/
    filters/
    ...
  data/
  pages/
  stores/
  types/
  App.tsx
  main.tsx
  shadcn.css
```

---

## نمط الكود والتصميم

- TypeScript مع تعليقات JSDoc موجزة للمكوّنات والدوال والواجهات.
- Tailwind مع shadcn UI:
  - لتخصيص ألوان/موضوع، استخدم متغيرات CSS ضمن إعدادات Tailwind إن لزم.
- الأيقونات: `lucide-react`.

---

## استكشاف الأخطاء

- مشكلة “Build failed … Unexpected ')' in regular expression”:
  - تم معالجة parsing لألوان rgba في `VisualGuard.tsx` بطريقة لا تستخدم تعبيرات نمطية قد يرفضها esbuild.
- ظهور خط عمودي أسود:
  - استخدم Alt+Shift+V لتفعيل/تعطيل VisualGuard.
  - إن استمر الظهور في عناصر محددة، عدّل المصدر في CSS/المكوّن مباشرة.

---

## المساهمة

- يرجى قراءة `CONTRIBUTING.md` قبل إرسال PRs.
- اتبع نمط التعليقات JSDoc وأسلوب كتابة TypeScript المستعمل في المشروع.
- تأكد أن الصفحة الرئيسية ليست فارغة وأن الأزرار outline في shadcn تحتوي `bg-transparent`.

---

## الأمن والإبلاغ

- راجع `SECURITY.md` لسياسات الإبلاغ عن الثغرات.

---

## الترخيص

- راجع ملف `LICENSE` في الجذر لمعرفة الرخصة المطبقة.

---

## خارطة طريق (اقتراحات)

- دعم i18n متعدد اللغات عبر i18next (موجود في الاعتمادات).
- تحسينات أداء: تقسيم كود (Code Splitting) وترحيل صور ذكية.
- دعم روابط نظيفة عبر BrowserRouter وإضافة Rewrites للمنصة المفضلة.
- تحسينات إمكانية الوصول (ARIA) واختبارات E2E.

إن احتجت إعدادات نشر مفصلة لمنصة محددة (Vercel، Netlify، Cloudflare Pages)، أخبرنا وسنزودك بالخطوات الدقيقة.
