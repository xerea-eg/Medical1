# نظام إدارة العيادة — Firebase Auth + Firestore Rules

المشروع: `medical-system-af4d9`

## خطوات التشغيل (مرة واحدة)

1. **Firebase Console → Build → Authentication → Sign-in method**
   فعّل **Email/Password**.

2. **Firestore Database**
   أنشئ قاعدة البيانات لو مش موجودة (Production mode).

3. **Firestore → Rules**
   انسخ محتوى `firestore.rules` والصقه ثم اضغط **Publish**.

4. **إنشاء أول مدير** (لازم يدوي، لأن القواعد بتمنع أي حد غير مفعّل):
   - Authentication → Users → **Add user**
     - Email: `admin@medical.xeriag.com`
     - Password: كلمة مرور قوية (6 أحرف على الأقل)
   - انسخ الـ **User UID** بتاع المستخدم ده.
   - Firestore → **Start collection** باسم `users` → Document ID = الـ UID اللي نسخته، والحقول:
     - `username` (string): `admin`
     - `name` (string): `المدير`
     - `role` (string): `admin`
     - `perms` (array): فاضية
     - `docId` (string): فاضية

5. ارفع `index.html` و`CNAME` و`logo.png.png` على الاستضافة (GitHub Pages) وادخل بـ `admin` وكلمة المرور.

## ملاحظات

- اسم المستخدم في التطبيق بيتحوّل داخلياً لإيميل: `اسم_المستخدم@medical.xeriag.com` (مش بيتبعت عليه إيميلات). أسماء المستخدمين: حروف إنجليزية وأرقام و `. _ -` فقط.
- المستخدمون الجدد بيتضافوا من شاشة الإعدادات، وكلمة المرور 6 أحرف على الأقل.
- **تغيير كلمة المرور:** كل مستخدم يغيّر كلمته بنفسه من زر 🔑. المدير مش قادر يغيّر كلمة مرور غيره من المتصفح (ده يحتاج Admin SDK). لو مستخدم نسي: احذف حسابه من Authentication في الـ Console وأضفه من جديد من التطبيق.
- **حذف مستخدم** من التطبيق بيقفل وصوله فوراً (بيمسح وثيقته)، لكن حساب Auth بيفضل موجود. لو أضفت نفس الاسم تاني بنفس كلمة المرور القديمة هيتربط تلقائياً.
- بيانات Firestore الجديدة فاضية؛ مفيش نقل من مشروع `xeria-eg`.
- رابط `APPS_URL` (رفع الملفات عبر Google Apps Script) لسه على حالته القديمة في الكود وبعيد عن Firebase؛ راجعه لو ده حساب Google مختلف.
