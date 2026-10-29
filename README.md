# mubina-oila-shajara
@@ -0,0 +1,60 @@
# Oila shajarasi — mustaqil sayt

Cloudflare Pages (bepul) + D1 bazasi. Kod va haftalik zaxira shu GitHub repozitoriyda saqlanadi.

- Ko'rish: havolani olgan har kim ko'radi (kirishsiz). Tirik insonlarning tug'ilgan kun va oyi yashiriladi — faqat yili ko'rinadi.
- Tahrirlash: faqat egasi, sahifadagi «Kirish» tugmasi orqali parol bilan.
- Qidiruv tizimlari saytni indekslamaydi (noindex).

## Bir martalik sozlash (taxminan 10 daqiqa)

### 1. Cloudflare hisobi
[dash.cloudflare.com/sign-up](https://dash.cloudflare.com/sign-up) — bepul ro'yxatdan o'ting (bank kartasi shart emas).

### 2. D1 bazasini yaratish
Cloudflare panelida: Storage & databases → D1 SQL database → Create → nomi: shajara → Create.
(Jadvallar va hozirgi 40 kishilik ma'lumot sayt birinchi ochilganda avtomatik yoziladi.)

### 3. Saytni GitHub'dan ulash
Workers & Pages → Create → Pages → Import an existing Git repository → GitHub'ni ulang → shajara repozitoriyini tanlang.

- Project name: shajara (manzil shajara.pages.dev bo'ladi; band bo'lsa boshqa nom tanlang)
- Framework preset: None
- Build command: *(bo'sh qoldiring)*
- Build output directory: public

Save and Deploy ni bosing.

### 4. Baza va parolni ulash
Loyiha → Settings:

- Bindings → Add → D1 database: Variable name DB, database shajara → Save.
- Variables and Secrets → Add: Type Secret, name ADMIN_PASSWORD, value — o'zingizning kuchli parolingiz → Save.
- (Ixtiyoriy, zaxira uchun) yana bitta Secret: BACKUP_TOKEN — kamida 16 belgili tasodifiy matn.

So'ng Deployments → oxirgi deploy → ⋯ → Retry deployment (sozlamalar kuchga kirishi uchun).

### 5. Tekshirish
https://shajara.pages.dev ni oching → shajara ko'rinadi → Kirish → parol → endi tahrirlay olasiz.

### 6. Haftalik avtomatik zaxira (ixtiyoriy, tavsiya etiladi)
GitHub → shu repozitoriy → Settings → Secrets and variables → Actions → New repository secret:

- SITE_URL = https://shajara.pages.dev
- BACKUP_TOKEN = Cloudflare'dagi bilan aynan bir xil

Har yakshanba backup/shajara-zaxira.json yangilanadi. Darhol sinash: Actions → Haftalik zaxira → Run workflow.

## Zaxiradan tiklash
Saytda Eksport → Zaxira nusxa → Fayldan tiklash → backup/shajara-zaxira.json (suratlar bilan birga tiklanadi).

## O'z domeningiz (ixtiyoriy, pullik)
Masalan qochqorovlar.uz sotib olsangiz: loyiha → Custom domains → Set up a domain.

## Dasturchi uchun
- src/shajara.html — asosiy sahifa (claude.ai versiyasi bilan bir xil).
- python3 build.py → public/index.html yasaydi (server adapteri va kirish tugmasini qo'shadi).
- public/sj-adapter.js — sahifani /api ga ulaydi.
- functions/api/[[path]].js — API (D1), functions/_blob/[id].js — suratlar.
- lib/seed.js — boshlang'ich ma'lumot (faqat baza bo'sh bo'lganda bir marta yoziladi).
- Mahalliy sinov: npm i && npm run dev → http://localhost:8788 (parol: sinov123).
