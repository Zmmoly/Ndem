# نديم - تطبيق تسميع القرآن الكريم

## نظرة عامة
نديم هو تطبيق أندرويد مصمم لمساعدة المسلمين في تسميع وحفظ القرآن الكريم. التطبيق مبني باستخدام Kotlin و Jetpack Compose و Firebase.

## المميزات
- 🔐 نظام تسجيل الدخول والتسجيل آمن
- 📖 واجهة مستخدم إسلامية أنيقة
- 🎤 تسجيل التسميع الصوتي
- 📊 تتبع التقدم والإحصائيات
- 👤 إدارة الملف الشخصي
- 🌙 تصميم متجاوب

## التقنيات المستخدمة
- **لغة البرمجة**: Kotlin
- **واجهة المستخدم**: Jetpack Compose
- **قاعدة البيانات**: Firebase Firestore
- **المصادقة**: Firebase Authentication
- **التخزين**: Firebase Storage (للملفات الصوتية)
- **البنية**: MVVM Architecture

## البنية
```
awab.quran.ar/
├── MainActivity.kt
├── NadeemApplication.kt
├── ui/
│   ├── theme/
│   │   ├── Color.kt
│   │   ├── Theme.kt
│   │   └── Type.kt
│   ├── navigation/
│   │   └── Navigation.kt
│   └── screens/
│       ├── splash/
│       │   └── SplashScreen.kt
│       ├── auth/
│       │   ├── LoginScreen.kt
│       │   ├── RegisterScreen.kt
│       │   └── ForgotPasswordScreen.kt
│       ├── home/
│       │   └── HomeScreen.kt
│       ├── recitation/
│       │   └── RecitationScreen.kt
│       └── profile/
│           └── ProfileScreen.kt
```

## إعداد Firebase

### الخطوة 1: إنشاء مشروع Firebase
1. اذهب إلى [Firebase Console](https://console.firebase.google.com/)
2. انقر على "Add project"
3. أدخل اسم المشروع "Nadeem"
4. اتبع التعليمات لإنشاء المشروع

### الخطوة 2: إضافة تطبيق Android
1. في صفحة المشروع، انقر على أيقونة Android
2. أدخل اسم الحزمة: `awab.quran.ar`
3. قم بتنزيل ملف `google-services.json`
4. ضع الملف في مجلد `app/`

### الخطوة 3: تفعيل الخدمات
1. **Authentication**:
   - اذهب إلى Authentication > Sign-in method
   - فعّل Email/Password
   
2. **Firestore Database**:
   - اذهب إلى Firestore Database
   - انقر على "Create database"
   - اختر وضع Test mode للبداية
   - اختر الموقع الأقرب لك

3. **Storage**:
   - اذهب إلى Storage
   - انقر على "Get started"
   - اتبع التعليمات

### الخطوة 4: قواعد Firestore
```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // قاعدة المستخدمين
    match /users/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
    
    // قاعدة التسميعات
    match /recitations/{recitationId} {
      allow read, write: if request.auth != null;
    }
  }
}
```

### الخطوة 5: قواعد Storage
```javascript
rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    match /recitations/{userId}/{allPaths=**} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```

## التثبيت والتشغيل

### المتطلبات
- Android Studio Hedgehog (2023.1.1) أو أحدث
- JDK 17 أو أحدث
- Android SDK API 24 أو أحدث
- Gradle 8.2 أو أحدث

### خطوات التشغيل
1. استنسخ المشروع:
```bash
git clone https://github.com/yourusername/nadeem.git
cd nadeem
```

2. افتح المشروع في Android Studio

3. ضع ملف `google-services.json` في مجلد `app/`

4. قم بمزامنة Gradle:
```
File > Sync Project with Gradle Files
```

5. قم بتشغيل التطبيق:
```
Run > Run 'app'
```

## الاستخدام

### تسجيل حساب جديد
1. افتح التطبيق
2. انقر على "إنشاء حساب جديد"
3. أدخل الاسم الكامل والبريد الإلكتروني وكلمة المرور
4. انقر على "إنشاء الحساب"

### بدء التسميع
1. من الصفحة الرئيسية، انقر على "ابدأ التسميع الآن"
2. أو اختر سورة من القائمة
3. انقر على أيقونة الميكروفون للبدء
4. ابدأ التسميع
5. انقر على زر الإيقاف عند الانتهاء

### عرض الإحصائيات
- من الصفحة الرئيسية يمكنك رؤية:
  - عدد التسميعات الكلي
  - عدد السور المكتملة

## هيكل قاعدة البيانات

### مجموعة Users
```javascript
{
  "fullName": "string",
  "email": "string",
  "createdAt": "timestamp",
  "totalRecitations": "number",
  "completedSurahs": "number"
}
```

### مجموعة Recitations
```javascript
{
  "userId": "string",
  "surahNumber": "number",
  "surahName": "string",
  "audioUrl": "string",
  "duration": "number",
  "createdAt": "timestamp",
  "score": "number" // اختياري
}
```

## الألوان المستخدمة
- **Primary Green**: #2E7D32
- **Light Green**: #66BB6A
- **Gold**: #D4AF37
- **Dark Green**: #1B5E20
- **Background**: #F5F5F5

## الأذونات المطلوبة
```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
```

## المساهمة
نرحب بالمساهمات! يرجى اتباع الخطوات التالية:
1. Fork المشروع
2. أنشئ branch للميزة الجديدة (`git checkout -b feature/AmazingFeature`)
3. Commit التغييرات (`git commit -m 'Add some AmazingFeature'`)
4. Push إلى Branch (`git push origin feature/AmazingFeature`)
5. افتح Pull Request

## الترخيص
هذا المشروع مرخص تحت رخصة MIT - انظر ملف LICENSE للتفاصيل

## التواصل
- المطور: [اسمك]
- البريد الإلكتروني: [بريدك الإلكتروني]
- رابط المشروع: [رابط GitHub]

## شكر وتقدير
- شكر خاص لمجتمع المطورين المسلمين
- Firebase لتوفير خدمات البنية التحتية
- Material Design 3 للتصميم الجميل

---

**ملاحظة**: هذا التطبيق مصمم لمساعدة المسلمين في حفظ القرآن الكريم. نسأل الله أن ينفع به.

بِسْمِ اللَّهِ الرَّحْمَٰنِ الرَّحِيمِ
