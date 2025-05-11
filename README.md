# تعليمات النشر للموقع

## متطلبات النشر

1. قاعدة بيانات PostgreSQL
2. بيئة تشغيل Python 3.9+

## المتغيرات البيئية المطلوبة:

```
# إعدادات قاعدة البيانات
DATABASE_URL=postgresql://username:password@hostname:port/database_name
PGDATABASE=database_name
PGHOST=hostname
PGPORT=port
PGUSER=username
PGPASSWORD=password

# سر الجلسة (مطلوب)
SESSION_SECRET=your_secure_random_string

# إعدادات تيليجرام (اختياري)
TELEGRAM_BOT_TOKEN=your_telegram_bot_token
TELEGRAM_CHAT_ID=your_telegram_chat_id
```

## خطوات النشر على Render:

1. قم بإنشاء قاعدة بيانات PostgreSQL جديدة على Render.
2. قم بإنشاء خدمة Web Service جديدة مع الإعدادات التالية:
   - Runtime: Python 3
   - Build Command: `pip install -r requirements.txt`
   - Start Command: `gunicorn --bind 0.0.0.0:$PORT main:app`
3. قم بإضافة المتغيرات البيئية المذكورة أعلاه في إعدادات Environment.
4. رفع الملفات إما عن طريق GitHub أو تحميل الملفات مباشرة.

## إنشاء مستخدم مسؤول:

يتضمن الموقع آليتين لإنشاء مستخدم مسؤول:

1. **طريقة تلقائية**: سيتم إنشاء مستخدم مسؤول افتراضي تلقائيًا عند تشغيل التطبيق لأول مرة.
   - اسم المستخدم: `admin`
   - كلمة المرور: `admin123`

2. **طريقة يدوية**: إذا واجهت مشكلة في الوصول إلى لوحة التحكم، يمكنك تنفيذ ملف إنشاء المسؤول عبر Shell:
   ```
   python create_admin_for_render.py
   ```
   أو
   ```
   python create_admin_direct.py admin admin@example.com admin123
   ```

## إصلاح مشكلة الوصول إلى لوحة الإحصائيات:

إذا واجهت مشكلة في الوصول إلى لوحة الإحصائيات (يتم اعتبارك كزائر وليس كمسؤول)،
استخدم إحدى الطرق التالية:

1. تأكد من تسجيل الدخول بحساب المسؤول (`admin`).
2. قم بتنفيذ ملف `create_admin_for_render.py` لإنشاء مستخدم مسؤول.
3. قم بإعادة تشغيل التطبيق بعد إنشاء المستخدم المسؤول.

## ملاحظات هامة:

1. قم بتغيير كلمة مرور المسؤول الافتراضية فور تسجيل الدخول الأول.
2. مجلدات التحميل ستكون فارغة عند البداية وستمتلئ عند رفع الملفات.
3. الموقع محسن للغة العربية بشكل افتراضي.

تم إعداد حزمة النشر هذه بتاريخ: 2025-05-11 13:41:16
