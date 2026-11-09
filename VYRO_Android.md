# VYRO Android

نسخة MVP عربية من شبكة VYRO الاجتماعية، مبنية بـ Kotlin وJetpack Compose وMaterial 3. تم الحفاظ على الهوية البصرية الداكنة وإضافة تدفق دخول/تسجيل، جلسة محلية، إنشاء منشورات، إعجاب، تعليقات، ملف شخصي، تنقل عربي RTL-friendly، وشاشات واضحة للميزات القادمة.

## التشغيل

1. افتح مجلد `VYRO-Android` في Android Studio حديث يدعم AGP 8.7 وKotlin 2.0.
2. شغّل `./gradlew assembleDebug` بعد إضافة Gradle Wrapper من Android Studio، أو شغّل `gradle assembleDebug` إذا كان Gradle مثبتًا.
3. ثبّت `app/build/outputs/apk/debug/app-debug.apk` على جهاز Android 6 أو أحدث.

## ما تم تنفيذه واختباره من ناحية الكود

- شاشة تسجيل الدخول وإنشاء الحساب مع تحقق أساسي من البريد وكلمة المرور.
- حفظ جلسة المستخدم محليًا عبر SharedPreferences وتسجيل الخروج.
- خلاصة منشورات تفاعلية محلية: إنشاء منشور، إعجاب/إلغاء إعجاب، وإضافة تعليق.
- ملف شخصي أولي وإحصاءات وتنقل عربي بخمس تبويبات.
- واجهة Shorts وRooms وMessages مع توضيح صريح لما يحتاج خدمة خادم حقيقية.
- مخطط Supabase أولي في `supabase/migrations/001_initial_schema.sql` يتضمن profiles/posts/likes/comments وRLS.
- GitHub Actions باستخدام Java 17 واسم artifact هو `VYRO-Android-APK`.

## غير منفذ بعد

البيانات البعيدة، Supabase Auth/Storage/Realtime، رفع الصور والفيديو، FCM، الرسائل الفورية، مؤشرات الكتابة وحالة القراءة، معالجة الفيديو، والرومات الصوتية الحية. هذه الميزات تتطلب إعداد مشروع Supabase، مفاتيح عميلة آمنة عبر BuildConfig/Secrets، ومزود صوت حقيقي مثل LiveKit أو Agora. لا تضع `service_role` أو كلمات مرور قاعدة البيانات داخل التطبيق.

## إعداد Supabase المقترح

نفّذ ملف SQL في Supabase SQL Editor، ثم أضف طبقة Repository تستخدم Supabase Auth وPostgREST وStorage. يجب إبقاء `anon` key فقط في تطبيق Android مع تفعيل RLS، ووضع مفاتيح الخادم في Edge Functions أو بيئة CI.

## ملاحظة مهمة

هذه الحزمة MVP قابلة للبناء والتوسعة وليست ادعاءً بأن الخدمات السحابية أو البث الحي تعمل دون إعداد خارجي. اختبارات قبول الحسابين والمزامنة بين الأجهزة تحتاج مشروع Supabase وبيانات اعتماد فعلية غير مرفقة.
