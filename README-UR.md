# Ultra HD Wallpapers — Android `app` module

یہ ZIP صرف `app/` ماڈیول فراہم کرتی ہے تاکہ اسے آپ کے موجودہ Android/Gradle پروجیکٹ میں شامل کیا جا سکے۔ یہ مکمل اصل پروجیکٹ یا تیار APK/AAB نہیں ہے، کیونکہ آپ کا موجودہ root پروجیکٹ اور اس کی Gradle configuration موصول نہیں ہوئی۔

## اس ماڈیول میں کیا ہے؟
- Java پر مبنی Android ایپ، اضافی third-party libraries کے بغیر
- تصاویر کی فہرست، نام سے تلاش، Favorites
- تصویر پر کلک کرکے Android WallpaperManager سے wallpaper لگانا
- تصاویر کے لیے `app/src/main/assets/wallpapers/` فولڈر
- APK اور AAB بنانے کے لیے Android Gradle Plugin کا app build script
- compileSdk/targetSdk 36 (اس کے لیے مناسب Android SDK اور compatible Android Gradle Plugin درکار ہے)

## استعمال
1. اپنے GitHub repository کے root میں `app` فولڈر upload کریں۔ فولڈر کے اندر کی فائلیں اپنی جگہ برقرار رکھیں۔
2. root `settings.gradle.kts` میں یہ لائن موجود ہونی چاہیے:

```kotlin
include(":app")
```

3. root `build.gradle.kts` یا `settings.gradle.kts` کی plugin management میں `com.android.application` plugin کی compatible version پہلے سے declare ہونی چاہیے۔ اس module کی `app/build.gradle.kts` میں plugin version جان بوجھ کر نہیں لکھی گئی تاکہ root project کے version سے ٹکراؤ نہ ہو۔
4. Android Studio میں Gradle Sync کریں۔ اگر root project میں Android Gradle Plugin موجود نہیں تو compatible plugin version شامل کریں اور Gradle wrapper کو اسی کے مطابق update کریں۔
5. اپنی قانونی طور پر استعمال کی اجازت رکھنے والی JPG/PNG/WebP تصاویر `app/src/main/assets/wallpapers/` میں رکھیں۔ مثال: `Nature_4K.jpg`, `Space_8K.webp`۔ خالی فولڈر میں کوئی اصل wallpaper شامل نہیں ہے۔
6. GitHub Actions میں `./gradlew :app:assembleDebug` سے debug APK اور `./gradlew :app:bundleRelease` سے release AAB بنائیں۔ Release APK/AAB کے لیے signing configuration اور محفوظ GitHub Secrets درکار ہیں۔

## اہم وضاحت
- یہ starter app module ہے، Play Store approval کی ضمانت نہیں دیتا۔
- صرف فائل کے نام میں 4K/8K لکھنے سے تصویر 4K/8K نہیں بنتی؛ اصل image dimensions اور license verify کریں۔
- Play Console کی موجودہ target API، Data safety، privacy policy، content rating، app signing اور دیگر شرائط submission سے پہلے دوبارہ چیک کریں۔
- اگر آپ کے موجودہ repository میں `gradlew` واقعی root پر موجود نہیں تو یہ ZIP اسے فراہم نہیں کرتی؛ Gradle Wrapper Android Studio/Gradle سے generate کرکے root میں commit کرنا ہوگا۔
