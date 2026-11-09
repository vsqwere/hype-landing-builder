---
name: "hype-landing-builder"
description: "Use when a client brief, ТЗ or client website arrives and a high-end animated landing page is needed: checks the brief for sanity first, picks one bold brand idea that is never boring in any style, builds from a ready motion kit with Impeccable and unslop-ui rules baked in, gates on both detectors plus QA, packages for Netlify. Built to spend few credits."
---

# Hype Landing Builder v4

Мета: лендинг рівня сильної студії, який не виглядає ні зробленим AI, ні нудним, у якому б стилі його не робили. І все це за мінімум кредитів.

Три опори:
1. **ТЗ перевірене** до першого рядка коду (розділ 0).
2. **Жодного AI-прийому.** Правила Impeccable і unslop-ui вбудовані сюди (розділ 2), а обидва детектори є воротами в кінці (розділ 4).
3. **Не нудно в будь-якому стилі.** Контракт сміливості (розділ 2) однаковий для мінімалізму, корпоративу, грайливого чи люкс-стилю. Змінюється лише те, чим його виконано.

Спілкуйся українською, тексти сайту пиши мовою аудиторії клієнта.

## Бюджет кредитів (читати першим)

Кредити зʼїдають довгі читання, переписування файлів, перегляд картинок, генерація і зайві кола. Тому:

- Сайт клієнта відкривай одним WebFetch, максимум ще одна сторінка заради фото. Референси не обходь.
- Одне коло питань. Брендові ідеї даються текстом у тому самому колі, без макетів-картинок.
- Субагентів не запускай. Плагін Impeccable не встановлюй і його команди-скіли не викликай: його правила вже в цьому файлі, з нього береш лише детектор `npx -y impeccable detect --json`. Сканер unslop-ui тягнеш одним `git clone` (розділ 4), репозиторій не читаєш.
- Готовий код (рух, базові стилі, QA, заголовки Netlify) лежить у цьому файлі нижче. **Не передруковуй його**, а витягни скриптом із розділу 3.
- Кожен файл пиши один раз за планом. Правки роби точково через Edit, весь файл ніколи не переписуй.
- Код тримай компактним: `styles.css` з токенами бренду, усі секції в `sections.jsx`, спільні компоненти вже є у `fx.jsx`.
- Скріншоти робить QA-скрипт: лише видима частина екрана, JPEG. Очима переглядай максимум 6 кадрів за весь проєкт.
- Вивід команд обрізай (`| tail -20`). Не читай `node_modules`, лок-файли й довгі логи.
- Фото генеруй лише для дірок: один batch-виклик, до 6 кадрів.
- Фінальний звіт: 6–8 рядків.

## 0. Перевірка ТЗ на адекватність

Перш ніж питати чи будувати, прочитай ТЗ (бриф, листування, сайт клієнта) і пройди сім перевірок. Думай як арт-директор, який не хоче зірвати дедлайн і репутацію.

1. **Ціль і дія.** Зрозуміло, що продається, кому, і що відвідувач має зробити (заявка, дзвінок, покупка, запис)? Якщо дій кілька, яка головна?
2. **Суперечності.** Вимоги, що виключають одна одну: «мінімалізм» і «все на першому екрані»; «преміум» і «знижки на кожному блоці»; «як Apple» і «20 секцій тексту»; аудиторія 60+ і дрібний сірий текст на чорному.
3. **Чого бракує.** Без чого сайт не збереш чесно: контакти, назва, реальні факти й цифри, фото, ціни, юридичні дані. Окремо: чого бракує, але можна закрити припущенням.
4. **Що поза межами скіла.** Це односторінковий лендинг на Vite + React під Netlify. Бекенд, авторизація, оплата, кошик, CMS, кабінет, багатосторінковість з роутингом, мультимовність з перемикачем: скажи прямо, що з цього зробиш як UI-заглушку, а що потребує окремої розробки.
5. **Ризикове або нечесне.** Вигадані відгуки, кейси, цифри чи логотипи клієнтів; копія чужого сайту чи бренду; згенеровані «наша команда» або «до/після»; медичні, фінансові чи юридичні обіцянки без підстав; чужі шрифти чи фото без ліцензії. Цю частину не робиш і пропонуєш чесну заміну (реальні дані, позначений плейсхолдер, сток з ліцензією).
6. **Нереалістичне.** Обсяг проти строку, «зроби як [студія] за годину», метрики, яких сайт не може гарантувати (конверсія ×3, топ-1 у Google). Чесно скажи, що реально.
7. **Відповідність аудиторії.** Чи пасує бажаний стиль тим, хто купує? Якщо ні, скажи чому одним реченням і запропонуй, як зберегти бажане відчуття без шкоди.

Вердикт пиши користувачу коротко, до 8 рядків, з пунктами лише там, де є проблема:
- **Можна будувати**: проблем немає.
- **Можна з припущеннями**: перелічи припущення, які візьмеш, якщо ніхто не заперечить.
- **Стоп**: є суперечність, нечесна вимога або критична дірка. Питання по них ідуть у коло питань розділу 1, і до відповіді код не пишеш.

Запиши вердикт першими рядками `docs/brand.md`.

## 1. Бриф → одне коло питань

З брифу або сайту витягни: що продається, головна дія, аудиторія, які є фото, контакти.

Далі один AskUserQuestion, до 4 питань. Питання зі «Стоп» з розділу 0 ідуть першими, решта за потребою:

1. **Брендова ідея.** Три варіанти, і всі три мають бути сміливими. У label назва світу (2–3 слова), у description до 25 слів: фірмовий прийом, палітра, шрифтова пара, головна сцена. Ідеї будуй з предметів, місць, матеріалів і ритуалів зі світу аудиторії клієнта, а не зі слів «мінімалізм», «сучасно» чи «яскраво». Перший варіант твій рекомендований. Якщо клієнт назвав стиль (мінімалізм, корпоратив, люкс), усі три ідеї в цьому стилі, але з різними прийомами.
2. **Фото:** з сайту клієнта / сток плюс генерація дірок / клієнт надішле.
3. **Головна дія**, якщо з брифу вона незрозуміла.
4. **Референс**, якщо клієнт не дав жодного: один сайт чи бренд, чий рівень і настрій подобається. Один реальний референс важить більше за всі правила.

Якщо відповіді немає, бери рекомендовані варіанти й припущення з розділу 0. Обране запиши в `docs/brand.md`, до 20 рядків: вердикт ТЗ, ідея, прийом, палітра в hex з поясненням, звідки кожен колір, шрифти з причиною вибору, фото-напрям, головна сцена, 3 приклади заголовків, контракт сміливості (розділ 2) одним рядком на пункт.

## 2. Дизайн: сміливо, без AI-прийомів

### 2.1 Контракт сміливості (для будь-якого стилю)

Нудний сайт виникає не через стиль, а через відсутність рішень. Мінімалізм теж може бути сміливим, якщо рішення радикальні. Кожен сайт виконує всі шість пунктів, а стиль лише визначає, чим:

1. **Фірмовий прийом.** Одна річ зі світу клієнта, яка повторюється на 4+ секціях і належить лише цьому бренду: форма з логотипу, матеріал, предмет, жест, спосіб кадрування. Тест: заміни логотип на конкурента. Якщо сайт досі пасує, прийому немає, переробляй.
2. **Одна авторська сцена.** Один момент руху, який розповідає ідею (як частини лого Pecode розлітаються в етапи роботи), а не набір однакових появ. Пін і scrub через ScrollTrigger. Решта сторінки майже статична.
3. **Контраст масштабу.** На кожному другому екрані є щось екстремальне за розміром: заголовок на всю ширину, фото на весь екран, одна цифра на пів екрана, або навпаки, крихітний обʼєкт у великій порожнечі.
4. **Хоча б одна секція, залита кольором бренду**, а не лише акцент на кнопках. Плюс одна темна або контрастна секція для ритму.
5. **Вихід за сітку.** Мінімум три місця, де елемент перекриває межу іншого: фото заходить на сусідню секцію, заголовок лягає на фото, картка наїжджає на кадр.
6. **Ритм секцій.** Сусідні секції відрізняються щільністю і композицією: широке фото → щільний список → велика цитата → мозаїка. Жодних двох однакових сіток підряд.

Що означає «сміливо» в різних стилях (приклади, не шаблон):
- **Мінімалізм:** багато повітря, але одна гігантська типографічна або фото-подія на екран, точний рух, жорстка сітка.
- **Корпоратив або B2B:** реальні фото людей і процесу на весь екран, кольорові поля бренду, конкретні цифри й імена замість іконок.
- **Люкс:** повільний ритм, великі кадри матеріалу крупним планом, мало слів, одна дорога сцена.
- **Грайливий:** насичені поля кольору, асиметрія, фірмова форма як персонаж, але без емодзі й мультяшного стоку.
- **Технічний:** справжні дані, схеми, інтерфейси продукту, щільність як перевага; моно лише для коду й чисел.

### 2.2 Сітка, типографіка, фото (базові значення, ідея може їх зсунути)

**Сітка і простір**
- 12 колонок. Поля сторінки `clamp(20px,4vw,64px)`, проміжок між колонками `clamp(12px,1.5vw,24px)`.
- Асиметрія свідома: наприклад, текст на 5 колонках з відступом у 1, фото на 7.
- Вертикальний відступ секцій `clamp(96px,14vw,220px)`. Шкала відступів кратна 8, одна на весь сайт.
- Тонкі лінії 1px (колір тексту на 15%) ділять секції й рядки списків.

**Типографіка**
- h1: `clamp(56px,10vw,168px)`, line-height 0.94, tracking не тісніше −0.04em.
- h2: `clamp(40px,6vw,96px)`.
- Основний текст 18–20px, ширина рядка до 60–75ch.
- Мета-текст (категорії, роки, підписи) 15–16px, менше не можна.
- Шрифт обирай з причиною, записаною в `docs/brand.md`. Пара з дисплейного й текстового зазвичай сильніша за один шрифт.
- Джерела: Fontshare, Pangram Pangram, Google Fonts поза чорним списком нижче. Формат woff2 локально, дисплейний через preload, fallback з `size-adjust`, щоб заміна шрифту не зсувала верстку.

**Фото**
- Від 10 медіа на сторінці. Hero на всю ширину або на 8+ колонок.
- Пропорції лише з набору 4:5, 3:2, 16:9, 1:1. Одна кольорова обробка для всіх кадрів.
- Одна мова зйомки на весь сайт: світло, крупність, точка зору, обробка.
- Порядок джерел: реальні фото клієнта, потім сток з перевіреною ліцензією, потім генерація атмосфери, деталей і матеріалів. Ніколи не генеруй команду, клієнтів або «до/після».
- Справжній продукт (скрін, дані, обʼєкт) краще за абстрактні ілюстрації. Без 3D-блобів і стокових ілюстрацій у стилі undraw.

### 2.3 Чорний список: жодного AI-прийому

Тут зведені правила Impeccable (craft floor) і unslop-ui (аналіз 3,2 млн дописів Reddit про те, що люди називають AI-слопом). Правило: прийом зі списку можна взяти, лише якщо це записане бренд-рішення клієнта в `docs/brand.md` (і тоді в коді коментар `unslop-ignore`). «Мені так здалося гарно» рішенням не є.

**Дефолти, які видають AI**
- «Смаковий дефолт» 2026: кремовий або бежевий фон + serif у заголовках (Instrument Serif, Fraunces, Playfair, Cormorant, DM Serif) + шавлієвий чи лісовий зелений. Будь-які два з трьох уже сигнал.
- AI-фіолетовий (violet, indigo) як основний колір; градієнт фіолетовий → синій.
- Градієнтний текст. Акцент дає вага чи розмір.
- Темна тема з неоновим світінням, якого ніхто не просив; кольоровий ореол без зсуву замість тіні.
- Нетюнінгований shadcn/Tailwind: стоковий slate, `rounded-lg` усюди, стандартні тіні.
- Шрифти на автопілоті: Inter, Geist, Roboto, DM Sans, Plus Jakarta, Outfit, Space Grotesk, Syne, Instrument Sans, системний шрифт як дисплейний.
- Газетні лінійки + italic serif + дрібні моно-лейбли; необорутал з жорсткими тінями `4px 4px 0` поза справжнім брутал-світом.

**Каркаси сторінки**
- Центрований hero з величезним заголовком і двома кнопками, а під ним три однакові картки «іконка + заголовок + текст».
- Однакові картки як основа сторінки; картки в картках.
- Шаблон «hero-метрики»: велика цифра, маленький підпис, ряд статистик.
- Лейбл чи kicker над заголовком. Це заборона без винятків.
- Нумерація секцій 01/02/03, якщо порядок нічого не означає.
- Все по центру з безкінечними порожнечами.

**Поверхні й деталі**
- Емодзі чи юнікод-символи замість іконок. Іконки малюються: одна бібліотека або власні SVG, одна товщина лінії.
- Скло й blur як декор; кольоровий `border-left` товщий за 1px на картках і списках.
- Моно-шрифт як «технічний» костюм, а не для коду й чисел.
- Однаковий радіус на всьому і пігулки всюди. Радіус: маленька свідома шкала.
- Геометричні маски (коло, полігон), що імітують контур людини чи предмета на фото.
- Курсив будь-де, крім цитати, яку дав клієнт.
- Текст менше 15px, капс в основному тексті.

**Рух**
- Однакова поява (fade-up) на кожній секції, `hover:scale-105` на кожній картці, скролджекінг усієї сторінки.
- Рух без змісту. Він або пояснює зв'язок, або веде погляд, або його немає.
- Bounce, elastic, анімації довші за 1,4 с на інтерфейсі.

**Тексти (unslop-ai-text)**
- Довге тире (—) у текстах сайту: заміни комою, крапкою або дужками.
- Конструкція «це не просто X, це Y» і «не X, а Y» як прийом.
- Трійки за звичкою («швидко, якісно, надійно»), однаковий ритм речень.
- Хайп-слова: unlock, unleash, elevate, seamless, game-changer, revolutionary, supercharge, effortlessly, «Your X, reimagined», «у сучасному швидкому світі», «трансформуйте», «революційний», «безшовний».
- Порожні фрази, що звучать гладко й нічого не кажуть. Кожне речення має факт, предмет або дію.
- Жирний лейбл з двокрапкою на початку кожного пункту; емодзі як буліти.
- Підсумки «отже», «підсумовуючи»; повтор однієї думки в кількох секціях.

**Чого НЕ ганяти** (дані показують, що це не сигнал AI): bento-сітка, mesh/aurora фон, темна тема сама по собі, Tailwind і shadcn з власною темою.

### 2.4 Обовʼязкова якість у будь-якому стилі

- **Контраст:** текст і плейсхолдери ≥ 4.5:1, великий текст ≥ 3:1. На кольоровому фоні вторинний текст тонуй від цього кольору, не сірим.
- **Глибина:** тіні мають зсув і мʼяке розмиття.
- **Стани:** hover, focus-visible, active, disabled, loading, error, empty у кожного клікабельного елемента й форми.
- **Поверхні браузера:** `::selection`, caret, скролбар, кільце фокуса, відступ підкреслення, табличні цифри в даних, усе в палітрі бренду.
- **Хедер:** не заважає читати (ховається при скролі вниз через `useHideHeader` або лишається компактним); мобільне меню на весь екран, з `aria-expanded` і закриттям по Esc.
- **Футер як подія:** великий CTA на всю ширину, контакти, адреса.
- **Факти:** лише справжні, з джерелом у `docs/brand.md`.
- **Копірайт:** мова самого продукту; кнопки називають дію; помилки кажуть, що сталося і як виправити.

**Секції** (обери 8–10, сусідні мають відрізнятися)
- Hero: велика подія (типографіка, фото або відео) і одна робоча дія. Якщо головна дія заявка, поле чи кнопка є вже на першому екрані.
- Маніфест: великий абзац на 2–3 рядки з акцентом кольором і фото збоку.
- Послуги чи продукти рядками з превʼю.
- Роботи чи кейси горизонтальною галереєю або великими кадрами.
- Процес: фото sticky ліворуч змінюються, кроки праворуч.
- Фото-мозаїка на сітці з різними пропорціями.
- Факти з фото.
- Відгук з портретом (лише справжній).
- FAQ акордеоном з лініями.
- Фінальний CTA і футер-подія.

## 3. Проєкт і кіт

```sh
npm create vite@latest site -- --template react && cd site
npm i gsap @gsap/react lenis && npm i -D playwright
```

Якщо браузер для Playwright ще не встановлений: `npx playwright install chromium`.

Витягни кіт із цього SKILL.md, не передруковуючи його. `SKILL_MD` — шлях до цього файлу в теці скіла:

```sh
python3 - "$SKILL_MD" <<'EOF'
import re,sys,os
s=open(sys.argv[1]).read()
for p,c in re.findall(r"```\w*\n(?://|/\*|#) file: (\S+)[^\n]*\n(.*?)```",s,re.S):
    os.makedirs(os.path.dirname(p) or '.',exist_ok=True); open(p,'w').write(c); print(p)
EOF
```

Отримаєш `src/fx.jsx`, `src/base.css`, `tests/qa.mjs` і `public/_headers`. Якщо теку скіла не знайшов, перепиши ці блоки вручну один раз.

Далі пишеш лише своє:
- `styles.css`: змінні `--bg`, `--ink`, `--accent`, `--r-btn`, `@font-face` з `docs/brand.md`, стилі секцій;
- `sections.jsx`;
- `App.jsx`;
- фото в `public/img` (WebP, до 2000px по довшій стороні).

У `main.jsx` імпортуй `base.css`, потім `styles.css`. В `App` виклич `useEffect(() => { const l = initScroll(); return () => l?.destroy(); }, [])`.

**Правила руху** (кіт їх уже виконує, не ламай):
- Одна авторська сцена з контракту сміливості пишеться окремо в `sections.jsx` через `gsap.matchMedia()` з cleanup; на мобайлі й при reduced motion її замінює статичний стан, де весь вміст видно.
- `Lines` лише для h1 і максимум двох ключових h2. `Media` з `reveal` лише для 2–3 ключових кадрів; решта фото без появи, тільки з внутрішнім паралаксом.
- Інструменти кіту (`HoverList`, `HScroll`, `Magnetic`) бери ті, що служать ідеї, а не всі одразу (ховання хедера чи компактний хедер обовʼязкові, див. 2.4). Два сайти поспіль з однаковим набором уже шаблон.
- Анімуються лише transform, opacity і clip-path.
- Easing `expo.out` для появи, без bounce.
- Пін лише через ScrollTrigger.
- Лише `svh`/`dvh`, ніколи `100vh`.
- Медіа з `aspect-ratio`, щоб не було зсувів.
- При reduced motion рух вимикається, вміст видно одразу.
- Не додавай інших reveal-ефектів на секції. Однакова поява на кожному блоці це AI-прийом.

```jsx
// file: src/fx.jsx
import { useRef } from 'react';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
import { SplitText } from 'gsap/SplitText';
import { useGSAP } from '@gsap/react';
import Lenis from 'lenis';
gsap.registerPlugin(ScrollTrigger, SplitText, useGSAP);
export const reduced = () => matchMedia('(prefers-reduced-motion: reduce)').matches;
const fine = () => matchMedia('(pointer: fine)').matches;

// Плавний скрол на одному тікері з ScrollTrigger
export function initScroll() {
  document.fonts.ready.then(() => ScrollTrigger.refresh());
  addEventListener('load', () => ScrollTrigger.refresh());
  if (reduced()) return null;
  const lenis = new Lenis({ autoRaf: false, lerp: 0.09, anchors: true });
  lenis.on('scroll', ScrollTrigger.update);
  gsap.ticker.add((t) => lenis.raf(t * 1000));
  gsap.ticker.lagSmoothing(0);
  return lenis;
}

// Хедер ховається при скролі вниз
export function useHideHeader(ref) {
  useGSAP(() => {
    ScrollTrigger.create({ start: 0, end: 'max', onUpdate: (s) =>
      ref.current?.classList.toggle('is-hidden', s.direction === 1 && s.scroll() > 160) });
  });
}

// Заголовок, що зʼявляється по рядках; intro = анімація при завантаженні
export function Lines({ as: Tag = 'h2', intro = false, className = '', children }) {
  const ref = useRef(null);
  useGSAP(() => {
    if (reduced()) return;
    SplitText.create(ref.current, { type: 'lines', mask: 'lines', autoSplit: true,
      onSplit: (s) => gsap.from(s.lines, { yPercent: 105, duration: 1.1, stagger: 0.08, ease: 'expo.out',
        delay: intro ? 0.15 : 0,
        scrollTrigger: intro ? undefined : { trigger: ref.current, start: 'top 88%', once: true } }) });
  }, { scope: ref });
  return <Tag ref={ref} className={className}>{children}</Tag>;
}

// Фото або відео в масці: паралакс усередині; reveal кліпом лише з reveal (2–3 ключові кадри)
export function Media({ src, alt = '', ratio = '4/5', video = false, poster, intro = false, reveal = false, className = '' }) {
  const ref = useRef(null);
  useGSAP(() => {
    if (reduced()) return;
    const el = ref.current, inner = el.firstElementChild;
    if (intro) gsap.from(inner, { scale: 1.15, duration: 1.4, ease: 'expo.out' });
    else if (reveal) gsap.fromTo(el, { clipPath: 'inset(100% 0% 0% 0%)' }, { clipPath: 'inset(0% 0% 0% 0%)', duration: 1.2, ease: 'expo.out',
      scrollTrigger: { trigger: el, start: 'top 90%', once: true } });
    gsap.fromTo(inner, { yPercent: -7 }, { yPercent: 7, ease: 'none',
      scrollTrigger: { trigger: el, start: 'top bottom', end: 'bottom top', scrub: true } });
  }, { scope: ref });
  return (
    <figure ref={ref} className={`media ${className}`} style={{ aspectRatio: ratio }}>
      {video
        ? <video src={src} poster={poster} muted playsInline loop autoPlay={!reduced()} />
        : <img src={src} alt={alt} loading={intro ? 'eager' : 'lazy'} fetchPriority={intro ? 'high' : 'auto'} decoding="async" />}
    </figure>
  );
}

// Магнітна обгортка для головного CTA (лише миша)
export function Magnetic({ children, strength = 0.3 }) {
  const ref = useRef(null);
  useGSAP(() => {
    if (!fine() || reduced()) return;
    const el = ref.current;
    const x = gsap.quickTo(el, 'x', { duration: 0.5, ease: 'power3' });
    const y = gsap.quickTo(el, 'y', { duration: 0.5, ease: 'power3' });
    const move = (e) => { const r = el.getBoundingClientRect();
      x((e.clientX - r.left - r.width / 2) * strength); y((e.clientY - r.top - r.height / 2) * strength); };
    const leave = () => { x(0); y(0); };
    el.addEventListener('pointermove', move); el.addEventListener('pointerleave', leave);
    return () => { el.removeEventListener('pointermove', move); el.removeEventListener('pointerleave', leave); };
  }, { scope: ref });
  return <span ref={ref} className="magnetic">{children}</span>;
}

// Рядки з лініями і превʼю-фото за курсором. items: [{ title, meta, img, href }]
export function HoverList({ items }) {
  const wrap = useRef(null), prev = useRef(null);
  const { contextSafe } = useGSAP(() => {
    gsap.set(prev.current, { xPercent: -50, yPercent: -50 });
    if (!fine() || reduced()) return;
    const x = gsap.quickTo(prev.current, 'x', { duration: 0.6, ease: 'power3' });
    const y = gsap.quickTo(prev.current, 'y', { duration: 0.6, ease: 'power3' });
    const move = (e) => { const r = wrap.current.getBoundingClientRect(); x(e.clientX - r.left); y(e.clientY - r.top); };
    wrap.current.addEventListener('pointermove', move);
    return () => wrap.current?.removeEventListener('pointermove', move);
  }, { scope: wrap });
  const show = contextSafe((src) => { if (!fine()) return; prev.current.querySelector('img').src = src;
    gsap.to(prev.current, { autoAlpha: 1, scale: 1, duration: 0.35, ease: 'power3.out' }); });
  const hide = contextSafe(() => gsap.to(prev.current, { autoAlpha: 0, scale: 0.9, duration: 0.25 }));
  return (
    <div ref={wrap} className="hlist" onPointerLeave={hide}>
      {items.map((it) => (
        <a key={it.title} href={it.href || '#contact'} className="hlist__row" onPointerEnter={() => show(it.img)}>
          <span className="hlist__t">{it.title}</span><span className="meta">{it.meta}</span>
          <img className="hlist__thumb" src={it.img} alt="" loading="lazy" />
        </a>
      ))}
      <div ref={prev} className="hlist__prev" aria-hidden="true"><img src={items[0]?.img} alt="" /></div>
    </div>
  );
}

// Горизонтальна галерея: пін на десктопі, свайп на мобайлі
export function HScroll({ children, id }) {
  const ref = useRef(null);
  useGSAP(() => {
    const mm = gsap.matchMedia();
    mm.add('(min-width: 900px) and (prefers-reduced-motion: no-preference)', () => {
      const track = ref.current.querySelector('.hs__track');
      const dist = () => Math.max(0, track.scrollWidth - innerWidth);
      gsap.to(track, { x: () => -dist(), ease: 'none',
        scrollTrigger: { trigger: ref.current, start: 'top top', end: () => '+=' + dist(), scrub: 0.6,
          pin: true, pinType: 'transform', anticipatePin: 1, invalidateOnRefresh: true } });
    });
  }, { scope: ref });
  return <section ref={ref} id={id} className="hs"><div className="hs__track">{children}</div></section>;
}
```

```css
/* file: src/base.css — каркас; кольори й шрифти перевизнач у styles.css з docs/brand.md */
:root{--bg:#fff;--ink:#111;--accent:#0047ff;--display:system-ui;--text:system-ui;
  --m:clamp(20px,4vw,64px);--g:clamp(12px,1.5vw,24px);--sec:clamp(96px,14vw,220px);--ease:cubic-bezier(.16,1,.3,1);
  --line:color-mix(in srgb,currentColor 15%,transparent);--r-btn:6px}
*,*::before,*::after{box-sizing:border-box}
html.lenis,html.lenis body{height:auto}.lenis.lenis-smooth{scroll-behavior:auto!important}
body{margin:0;background:var(--bg);color:var(--ink);font:400 clamp(18px,1.25vw,20px)/1.5 var(--text);-webkit-font-smoothing:antialiased;overflow-x:clip}
img,video{display:block;max-width:100%}
::selection{background:var(--accent);color:var(--bg)}
:focus-visible{outline:2px solid var(--accent);outline-offset:3px}
.wrap{padding-inline:var(--m)}
.grid{display:grid;grid-template-columns:repeat(12,minmax(0,1fr));column-gap:var(--g)}
.sec{padding-block:var(--sec)}
.rule{border-top:1px solid var(--line)}
h1,h2,h3{font-family:var(--display);font-weight:500;margin:0;text-wrap:balance}
h1{font-size:clamp(56px,10vw,168px);line-height:.94;letter-spacing:-.03em}
h2{font-size:clamp(40px,6vw,96px);line-height:1;letter-spacing:-.025em}
h3{font-size:clamp(24px,2.2vw,36px);line-height:1.1;letter-spacing:-.01em}
p{margin:0;max-width:60ch;text-wrap:pretty}
.meta{font-size:15px;line-height:1.4;opacity:.75}
.media{position:relative;overflow:hidden;margin:0;background:color-mix(in srgb,var(--ink) 8%,var(--bg))}
.media>img,.media>video{position:absolute;left:0;top:-8%;width:100%;height:116%;object-fit:cover}
.link{color:inherit;text-decoration:none;background:linear-gradient(currentColor,currentColor) 100% 100%/0 1px no-repeat;transition:background-size .6s var(--ease)}
.link:hover{background-size:100% 1px;background-position:0 100%}
.btn{position:relative;display:inline-flex;align-items:center;gap:.6em;padding:1.1em 1.8em;border:1px solid currentColor;border-radius:var(--r-btn);color:inherit;text-decoration:none;font:500 17px/1 var(--text);overflow:hidden;isolation:isolate;transition:color .5s var(--ease)}
.btn::before{content:'';position:absolute;inset:0;background:var(--ink);transform:translateY(101%);transition:transform .5s var(--ease);z-index:-1}
.btn:hover{color:var(--bg)}.btn:hover::before{transform:none}
.magnetic{display:inline-block}
.header{position:fixed;inset:0 0 auto;z-index:50;display:flex;justify-content:space-between;align-items:center;padding:20px var(--m);color:#fff;mix-blend-mode:difference;transition:transform .6s var(--ease)}
.header.is-hidden{transform:translateY(-100%)}
.hlist{position:relative}
.hlist__row{display:grid;grid-template-columns:1fr auto;align-items:baseline;gap:var(--g);padding:28px 0;border-top:1px solid var(--line);color:inherit;text-decoration:none;transition:padding .6s var(--ease)}
.hlist__row:last-of-type{border-bottom:1px solid var(--line)}
.hlist__row:hover{padding-left:24px}
.hlist__t{font:500 clamp(28px,4vw,64px)/1 var(--display);letter-spacing:-.02em}
.hlist__thumb{display:none}
.hlist__prev{position:absolute;left:0;top:0;width:min(26vw,360px);aspect-ratio:4/5;pointer-events:none;visibility:hidden;opacity:0;overflow:hidden;z-index:5}
.hlist__prev img{width:100%;height:100%;object-fit:cover}
@media (pointer:coarse){.hlist__thumb{display:block;grid-column:1/-1;width:100%;aspect-ratio:3/2;object-fit:cover}.hlist__prev{display:none}}
.hs{overflow:hidden}
.hs__track{display:flex;gap:var(--g);padding-inline:var(--m);width:max-content}
.hs__track>*{flex:none;width:clamp(280px,36vw,600px)}
@media (max-width:899px){.hs__track{width:auto;overflow-x:auto;scroll-snap-type:x mandatory}.hs__track>*{width:80vw;scroll-snap-align:start}}
@media (prefers-reduced-motion:reduce){.hs__track{width:auto;overflow-x:auto}*,*::before,*::after{transition-duration:.01ms!important;animation-duration:.01ms!important}}
```

```js
// file: tests/qa.mjs — node tests/qa.mjs (BASE_URL=... за потреби); друкує лише проблеми
import { chromium } from 'playwright';
import { mkdirSync } from 'node:fs';
mkdirSync('qa', { recursive: true });
const BASE = process.env.BASE_URL || 'http://127.0.0.1:4173/';
const b = await chromium.launch(); const res = {}; const errors = [];
for (const w of [390, 768, 1440]) {
  const p = await b.newPage({ viewport: { width: w, height: w < 800 ? 844 : 900 } });
  p.on('pageerror', (e) => errors.push(e.message)); p.on('console', (m) => m.type() === 'error' && errors.push(m.text()));
  await p.addInitScript(() => { window.__f = []; let l = performance.now();
    const t = (n) => { window.__f.push(n - l); l = n; requestAnimationFrame(t); }; requestAnimationFrame(t);
    window.__cls = 0; new PerformanceObserver((x) => x.getEntries().forEach((e) => { if (!e.hadRecentInput) window.__cls += e.value; }))
      .observe({ type: 'layout-shift', buffered: true }); });
  await p.goto(BASE, { waitUntil: 'networkidle' }); await p.waitForTimeout(1600);
  const H = await p.evaluate(() => document.documentElement.scrollHeight);
  const marks = w === 768 ? [] : [0, 0.33, 0.66].map((f) => Math.floor(H * f)); let i = 0;
  for (let y = 0; y < H; y += 150) {
    if (marks.length && y >= marks[0]) { marks.shift(); await p.waitForTimeout(700);
      await p.screenshot({ path: `qa/${w}-${i++}.jpg`, type: 'jpeg', quality: 60 }); }
    await p.mouse.wheel(0, 150); await p.waitForTimeout(35);
  }
  await p.waitForTimeout(1000);
  res[w] = await p.evaluate(() => {
    const vis = (el) => { const s = getComputedStyle(el); return s.display !== 'none' && s.visibility !== 'hidden' && el.getClientRects().length && !el.closest('[aria-hidden="true"]'); };
    const txt = [...document.querySelectorAll('body *')].filter((el) => vis(el) && [...el.childNodes].some((n) => n.nodeType === 3 && n.textContent.trim()));
    const cut = (el) => el.textContent.trim().slice(0, 30); const f = window.__f.slice(30);
    const inView = (el) => { const r = el.getBoundingClientRect(); return r.width > 40 && r.height > 20 && r.top >= 0 && r.bottom <= innerHeight; };
    return {
      overflow: document.documentElement.scrollWidth > innerWidth,
      italic: txt.filter((el) => getComputedStyle(el).fontStyle !== 'normal' && !el.closest('blockquote')).map(cut).slice(0, 4),
      tiny: txt.filter((el) => parseFloat(getComputedStyle(el).fontSize) < 15).map(cut).slice(0, 4),
      caps: txt.filter((el) => getComputedStyle(el).textTransform === 'uppercase' && parseFloat(getComputedStyle(el).fontSize) < 24).map(cut).slice(0, 4),
      dash: txt.filter((el) => el.textContent.includes('—')).map(cut).slice(0, 4),
      gradText: txt.filter((el) => getComputedStyle(el).backgroundClip === 'text' || getComputedStyle(el).webkitBackgroundClip === 'text').map(cut).slice(0, 4),
      media: [...document.querySelectorAll('img,video,canvas')].filter((m) => vis(m) && m.getBoundingClientRect().width > 160).length,
      bare: [...document.querySelectorAll('main section')].filter((s) => !s.querySelector('img,video,canvas')).map((s) => s.id || s.className).slice(0, 4),
      broken: [...document.images].filter((im) => im.complete && im.getAttribute('src') && !im.naturalWidth).map((im) => im.src.split('/').pop()),
      hidden: [...document.querySelectorAll('main *')].filter((el) => vis(el) && inView(el) && (+getComputedStyle(el).opacity < 0.05 || getComputedStyle(el).clipPath.includes('100%'))).length,
      jank: +(f.filter((d) => d > 50).length / Math.max(f.length, 1)).toFixed(3),
      cls: +window.__cls.toFixed(3),
    };
  });
  await p.close();
}
await b.close();
const fail = [];
for (const [w, r] of Object.entries(res)) {
  if (r.overflow) fail.push(`${w}: горизонтальний скрол`);
  if (r.italic.length) fail.push(`${w}: курсив ${r.italic.join(' | ')}`);
  if (r.tiny.length) fail.push(`${w}: текст <15px ${r.tiny.join(' | ')}`);
  if (r.caps.length) fail.push(`${w}: капс-лейбли ${r.caps.join(' | ')}`);
  if (r.dash.length) fail.push(`${w}: довге тире в текстах ${r.dash.join(' | ')}`);
  if (r.gradText.length) fail.push(`${w}: градієнтний текст ${r.gradText.join(' | ')}`);
  if (r.broken.length) fail.push(`${w}: биті фото ${r.broken.join(', ')}`);
  if (r.hidden) fail.push(`${w}: ${r.hidden} блоків приховані після скролу`);
  if (r.cls > 0.05) fail.push(`${w}: CLS ${r.cls}`);
  if (r.jank > 0.05) fail.push(`${w}: ривки ${r.jank}`);
}
if (res[1440].media < 10) fail.push(`лише ${res[1440].media} медіа (треба 10+)`);
if (res[1440].bare.length > 1) fail.push(`секції без медіа: ${res[1440].bare.join(', ')}`);
if (errors.length) fail.push(`помилки консолі: ${[...new Set(errors)].slice(0, 3).join(' | ')}`);
console.log(fail.length ? 'FAIL\n' + fail.join('\n') : `QA OK · медіа ${res[1440].media} · CLS ${res[1440].cls} · ривки ${res[1440].jank}`);
process.exitCode = fail.length ? 1 : 0;
```

```
# file: public/_headers
/assets/*
  Cache-Control: public, max-age=31536000, immutable
/*
  X-Frame-Options: DENY
  X-Content-Type-Options: nosniff
  Referrer-Policy: strict-origin-when-cross-origin
  Permissions-Policy: camera=(), microphone=(), geolocation=()
```

## 4. Ворота: один прохід плюс одне коло правок

1. Збери і запусти: `npm run build && (npx vite preview --port 4173 --strictPort &)`.
2. **Impeccable**, по коду і по рендеру:
   `npx -y impeccable detect --json src/ | head -c 3000`
   `npx -y impeccable detect --json http://127.0.0.1:4173/ | head -c 3000`
   Мета: 0 знахідок, крім бренд-рішень, записаних у `docs/brand.md`.
3. **unslop-ui** (MIT, Carter Johnson), сканер тягнеш один раз:
   `[ -d /tmp/unslop ] || GIT_LFS_SKIP_SMUDGE=1 git clone -q --depth 1 https://github.com/JCarterJohnson/vibecoded-design-tells /tmp/unslop`
   `python3 /tmp/unslop/skill/scripts/devibe_scan.py src | tail -20`
   Мета: high 0, medium лише з `unslop-ignore` і записаною причиною. Якщо клон не вдався, пройди розділ 2.3 очима й напиши у звіті, що сканер не запускався.
4. **QA:** `node tests/qa.mjs`. Скрипт друкує лише проблеми: overflow, курсив, текст < 15px, капс-лейбли, довге тире, градієнтний текст, биті фото, приховані блоки, CLS, ривки, мало медіа, секції без медіа.
5. **Очима, 6 кадрів** `qa/390-*.jpg` і `qa/1440-*.jpg`. Три питання:
   - **AI-тест:** чи є на кадрах хоч один прийом з розділу 2.3, якого детектори не бачать (каркас «hero + 3 картки», однакові секції, все по центру, рух на кожному блоці)?
   - **Тест нудьги:** чи виконано всі шість пунктів контракту сміливості? Заміни подумки логотип на конкурента: сайт досі пасує? Що запамʼятається через 3 секунди?
   - **Тест ТЗ:** кожна вимога з брифу знаходиться за секунди, головна дія видна на першому екрані.
   Перевір і клавіатуру: Tab має пройти меню, CTA і форму, фокус має бути видно.
6. Виправ точково через Edit, перезапусти білд, обидва детектори і QA. На цьому зупинись: те, що лишилось, піде у звіт. Тест не послаблюй, правило не вимикай, щоб пройти.
7. Цифри headless-браузера це димовий тест, а не замір реального телефона. У звіті напиши, що на пристрої не перевірено.

## 5. Netlify і звіт

- Netlify Forms: прихована статична форма з `data-netlify="true"`. Видима форма шле POST, «Дякуємо» показується лише після успішної відповіді. Тестових заявок на реальні форми клієнта не надсилай. Якщо форма лише UI, так і напиши на сторінці й у README.
- Для концепту додай у `_headers` `X-Robots-Tag: noindex, nofollow`. Для SPA з роутами потрібен `public/_redirects` з рядком `/* /index.html 200`.
- Скрипт збірки: `"build:netlify": "vite build && cd dist && rm -f ../site-netlify.zip && zip -qr -X ../site-netlify.zip ."` (`index.html` має лежати в корені архіву).
- Деплой: Netlify → Add new site → Deploy manually → перетягнути zip.
- README до 30 рядків:
  - запуск;
  - вердикт ТЗ і взяті припущення;
  - ідея бренду і як виконано контракт сміливості;
  - звідки фото (реальні / сток з ліцензією й автором / згенеровані, так і позначити);
  - результати воріт: Impeccable (код і рендер), unslop-ui (high/medium), QA;
  - що не перевірено;
  - контент, який має підтвердити клієнт.
- Звіт користувачу, 6–8 рядків:
  - вердикт ТЗ одним рядком;
  - ідея і фірмовий прийом;
  - секції;
  - фото і звідки;
  - ворота: Impeccable, unslop-ui, QA;
  - що лишилось.

  Zip надсилай через SendUserFile.

## Завжди

- Не вигадуй цифри, відгуки, логотипи й контакти. Згенеровані фото не видавай за реальні.
- Не копіюй код, фото й тексти референсів.
- Шрифти й фото у фінальній збірці лише локальні.
- Не пиши «перевірено», якщо перевірку не запускав.
- Не замінюй один дефолт іншим: виправлення фіолетового не «зелений, бо гарно», а колір бренду або записане рішення.

Джерела правил: Impeccable (impeccable.style, Apache-2.0) і unslop-ui / vibecoded-design-tells (github.com/JCarterJohnson/vibecoded-design-tells, MIT, Carter Johnson). Правила переказані своїми словами, код сканера тягнеться з репозиторію під його ліцензією.