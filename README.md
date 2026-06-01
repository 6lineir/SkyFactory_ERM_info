<p align="center">
  <img src="https://github.com/6lineir/SkyFactory_ERM_info/blob/main/Screens_ERM/logo.png?raw=true" alt="SkyTex Logo" width="80">
</p>

<h1 align="center">SkyTex ERP · پلتفرم هوشمند مدیریت تولید و انبارداری</h1>

<p align="center">
  <strong>راهکار یکپارچه جامع برای صنایع نساجی</strong><br />
  مدیریت تولید، انبار، خروج کالا و کنترل کیفیت در یک پلتفرم مدرن
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.13-blue?logo=python" />
  <img src="https://img.shields.io/badge/Django-6.0-darkgreen?logo=django" />
  <img src="https://img.shields.io/badge/Next.js-15-black?logo=next.js" />
  <img src="https://img.shields.io/badge/TypeScript-5.0-blue?logo=typescript" />
  <img src="https://img.shields.io/badge/Docker-Ready-2496ED?logo=docker" />
  <img src="https://img.shields.io/badge/License-MIT-green" />
</p>

---

## 📖 درباره پروژه

**SkyTex ERP** یک سیستم برنامه‌ریزی منابع سازمانی (ERP) تخصصی برای **کارخانه‌های بافندگی و نساجی** است. این پلتفرم با هدف دیجیتالی کردن فرآیندهای کلیدی از جمله:

- ثبت و پیگیری سری‌های تولید
- مدیریت دقیق انبار نخ، پارچه و کش
- کنترل کیفیت طاقه‌ها (QC)
- صدور حواله خروج و مدیریت مشتریان
- گزارش‌گیری و ثبت رویدادها

طراحی شده است. معماری مدرن مبتنی بر **Next.js** در فرانت‌اند و **Django REST Framework** در بک‌اند، مقیاس‌پذیری، امنیت و تجربه کاربری روان را تضمین می‌کند.

---

## ✨ ویژگی‌های کلیدی

| ماژول                    | قابلیت‌ها                                                                              |
| ------------------------ | -------------------------------------------------------------------------------------- |
| 👥 **مدیریت کاربران**    | احراز هویت JWT، نقش‌های `Admin`، `ProductionManager`، `WarehouseKeeper`، `Guest`       |
| 🏭 **تولید**             | تعریف سری تولید، تخصیص ماشین‌آلات و بافنده‌ها، ثبت وزن و ابعاد، محاسبه وزن نهایی       |
| 📦 **انبارداری پیشرفته** | انبارهای چندگانه، ردیابی طاقه با شماره سریال، رزرو خودکار نخ، انتقال بین انبارها       |
| ✅ **کنترل کیفیت**       | امکان تأیید QC و ثبت یادداشت برای هر طاقه، بروزرسانی گروهی                             |
| 🚚 **فروش و حواله**      | مدیریت مشتریان، ایجاد حواله خروج، تغییر خودکار وضعیت طاقه به `shipped`                 |
| 📄 **رسید ورودی**        | ثبت تأمین‌کننده، بارنامه، فاکتور و افزایش موجودی                                       |
| 🖨️ **سفارشات چاپ**       | وضعیت‌های `design_pending`، `printing`، `completed`، ثبت جزئیات طرح و متراژ            |
| 🎨 **تنظیمات پلتفرم**    | شخصی‌سازی نام سایت، حالت تعمیر و نگهداری، **تم رنگی پویا** (روشن/تاریک با رنگ‌های HSL) |
| 📜 **لاگ حسابرسی**       | ثبت تمام فعالیت‌های کاربران به همراه زمان و جزئیات                                     |

---

## 🧰 تکنولوژی‌های به کار رفته

### بک‌اند (Backend)

- **Django 6.0** + **Django REST Framework**
- احراز هویت: `djangorestframework-simplejwt`
- تبدیل خودکار camelCase/snake_case با `djangorestframework-camel-case`
- مستندات API: `drf-spectacular` (Swagger UI)
- فیلترگذاری: `django-filter`
- فایل‌های استاتیک: `Whitenoise`

### فرانت‌اند (Frontend)

- **Next.js 15** (App Router) + **TypeScript**
- استایل: Tailwind CSS
- انتخاب تاریخ: `react-multi-date-picker`
- ارتباط با API: `fetch` با `api-client` سفارشی

### زیرساخت

- **Docker** + **Docker Compose** (برای اجرای آسان)
- دیتابیس: **SQLite** (توسعه) / **PostgreSQL** (تولید)
- Proxy معکوس: قابل استفاده با Nginx

---

## 🔄 معماری داده و جریان اطلاعات

لایه دسترسی به داده (Data Service) تمام تعاملات با سرور را مدیریت می‌کند. هر کامپوننت React با فراخوانی توابعی مانند `getProductionSeries()` درخواست خود را ارسال می‌کند:
کامپوننت React
↓ فراخوانی
getProductionSeries() (از data-service)
↓ استفاده از
apiRequest('/production/production-series/', 'GET')
↓ ارسال درخواست به
بک‌اند Django (http://localhost:8000)
↓ بازگشت JSON (تبدیل خودکار camelCase)
بازگشت داده به کامپوننت

text

توابع آماده برای **دریافت، ایجاد، بروزرسانی و حذف** اطلاعات مربوط به:

- انبارها، ماشین‌آلات، بافنده‌ها
- طاقه‌های پارچه، نخ‌ها، کش‌ها
- سری‌های تولید، حواله‌های خروج، رسیدهای ورودی
- مشتریان، سفارشات چاپ، لاگ‌های حسابرسی و تنظیمات پلتفرم

به طور کامل پیاده‌سازی شده‌اند.

---
## 📸 نمایشی از محیط پلتفرم

<p align="center">
  <em>تصاویر زیر نمای کلی از ماژول‌های مختلف سیستم اسکای‌تکس را نشان می‌دهد.</em>
</p>

<div style="display: grid; grid-template-columns: repeat(auto-fill, minmax(320px, 1fr)); gap: 16px; direction: ltr;">
  <img src="https://github.com/6lineir/SkyFactory_ERM_info/blob/main/Screens_ERM/01.png?raw=true" alt="Dashboard" style="width: 100%; border-radius: 12px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
  <img src="https://github.com/6lineir/SkyFactory_ERM_info/blob/main/Screens_ERM/02.png?raw=true" alt="Production Series" style="width: 100%; border-radius: 12px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
  <img src="https://github.com/6lineir/SkyFactory_ERM_info/blob/main/Screens_ERM/03.png?raw=true" alt="Fabric Rolls" style="width: 100%; border-radius: 12px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
  <img src="https://github.com/6lineir/SkyFactory_ERM_info/blob/main/Screens_ERM/04.png?raw=true" alt="Yarn Inventory" style="width: 100%; border-radius: 12px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
  <img src="https://github.com/6lineir/SkyFactory_ERM_info/blob/main/Screens_ERM/05.png?raw=true" alt="Outbound Shipment" style="width: 100%; border-radius: 12px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
  <img src="https://github.com/6lineir/SkyFactory_ERM_info/blob/main/Screens_ERM/06.png?raw=true" alt="Customer Management" style="width: 100%; border-radius: 12px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
  <img src="https://github.com/6lineir/SkyFactory_ERM_info/blob/main/Screens_ERM/07.png?raw=true" alt="Print Orders" style="width: 100%; border-radius: 12px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
  <img src="https://github.com/6lineir/SkyFactory_ERM_info/blob/main/Screens_ERM/08.png?raw=true" alt="Warehouses" style="width: 100%; border-radius: 12px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
  <img src="https://github.com/6lineir/SkyFactory_ERM_info/blob/main/Screens_ERM/09.png?raw=true" alt="Machines" style="width: 100%; border-radius: 12px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
  <img src="https://github.com/6lineir/SkyFactory_ERM_info/blob/main/Screens_ERM/10.png?raw=true" alt="Weavers" style="width: 100%; border-radius: 12px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
  <img src="https://github.com/6lineir/SkyFactory_ERM_info/blob/main/Screens_ERM/11.png?raw=true" alt="QC Check" style="width: 100%; border-radius: 12px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
  <img src="https://github.com/6lineir/SkyFactory_ERM_info/blob/main/Screens_ERM/12.png?raw=true" alt="Platform Settings" style="width: 100%; border-radius: 12px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
  <img src="https://github.com/6lineir/SkyFactory_ERM_info/blob/main/Screens_ERM/13.png?raw=true" alt="Audit Logs" style="width: 100%; border-radius: 12px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
  <img src="https://github.com/6lineir/SkyFactory_ERM_info/blob/main/Screens_ERM/14.png?raw=true" alt="Inbound Delivery" style="width: 100%; border-radius: 12px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
  <img src="https://github.com/6lineir/SkyFactory_ERM_info/blob/main/Screens_ERM/15.png?raw=true" alt="Reports" style="width: 100%; border-radius: 12px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
  <img src="https://github.com/6lineir/SkyFactory_ERM_info/blob/main/Screens_ERM/16.png?raw=true" alt="Login Page" style="width: 100%; border-radius: 12px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
</div>

---

---

---

## 🚀 نصب و اجرا

### روش ۱: اجرا با Docker (توصیه شده برای تولید)

bash

# 1. کلون مخزن

git clone https://github.com/yourusername/skytex-erp.git
cd skytex-erp

# 2. ساخت و اجرای کانتینرها

docker-compose up --build -d

# 3. اعمال migration‌ها

docker exec -it skytex-backend-1 python manage.py migrate

# 4. ایجاد کاربر ادمین (اختیاری)

docker exec -it skytex-backend-1 python manage.py createsuperuser
اکنون فرانت‌اند در http://localhost:3000 و بک‌اند در http://localhost:8000 در دسترس است.

روش ۲: اجرای محلی (برای توسعه)
پیش‌نیازها: Python 3.13+، Node.js 22+، npm

بک‌اند (Django)
bash
cd app-back-django
python -m venv venv
source venv/bin/activate # یا venv\Scripts\activate در ویندوز
pip install -r requirements.txt
python manage.py migrate
python manage.py runserver
فرانت‌اند (Next.js)
bash
cd client
npm install
cp .env.example .env.local # تنظیم NEXT_PUBLIC_API_URL
npm run dev
📂 ساختار پروژه

```text
skytex-erp/
├── app-back-django/          # بک‌اند جنگو
│   ├── core/                 # ابزارهای عمومی، middleware
│   ├── users/                # مدل کاربر سفارشی
│   ├── inventory/            # انبار (نخ، طاقه، کش)
│   ├── production/           # تولید (سری، ماشین، بافنده)
│   ├── sales/                # فروش (مشتری، حواله، سفارش چاپ)
│   └── requirements.txt
├── client/                   # فرانت‌اند Next.js
│   ├── app/                  # صفحات، API routes
│   ├── components/           # کامپوننت‌های React
│   └── package.json
├── docker-compose.yml
├── Dockerfile.backend
├── Dockerfile.frontend
└── README.md
```

📡 مستندات API
پس از اجرای بک‌اند، مستندات تعاملی Swagger در آدرس زیر قابل دسترسی است:

```text
http://localhost:8000/api/schema/swagger-ui/
```

برای تست APIها می‌توانید توکن JWT را از طریق api/token/ دریافت کنید.

🤝 مشارکت در توسعه
ما از مشارکت شما استقبال می‌کنیم!
لطفاً مراحل زیر را دنبال کنید:

مخزن را Fork کنید.

یک branch جدید ایجاد کنید: git checkout -b feature/awesome-feature

تغییرات خود را commit کنید: git commit -m 'Add awesome feature'

Push به branch: git push origin feature/awesome-feature

یک Pull Request باز کنید.

📄 مجوز
این پروژه تحت مجوز MIT منتشر شده است. برای جزئیات بیشتر فایل LICENSE را مشاهده کنید.

<p align="center"> ساخته شده با ❤️ برای صنعت نساجی ایران<br /> <a href="https://github.com/6lineir/SkyFactory_ERM">GitHub</a> · <a href="https://yourdemo.com">مشاهده دمو</a> · <a href="tel:989966099982">تماس با ما</a> </p>
