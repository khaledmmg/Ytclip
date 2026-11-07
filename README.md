# YtClip

[English](#english) | [العربية](#arabic)

---

<a name="english"></a>
## English

**YtClip** is a small Android app that downloads YouTube videos with [yt-dlp](https://github.com/yt-dlp/yt-dlp) and can trim them to a start/end time while downloading. It uses the [youtubedl-android](https://github.com/yausername/youtubedl-android) library (yt-dlp + ffmpeg bundled inside the app).

### Features
- Paste a link, or share it from the YouTube app (Share → YtClip).
- Choose an available video quality up to 4K, or download audio as M4A or MP3.
- A quick quality list appears first; a slower full-format scan runs only when requested.
- Trim with a range slider or enter hours, minutes, and seconds.
- See an approximate full-video and selected-clip size before downloading; the Files tab shows the actual saved size.
- Optional frame-accurate cut (slower, re-encodes the video).
- Background download queue with progress, pause, resume, cancel, and notifications.
- Video previews stay in the app instead of creating a separate JPG; audio cover art is embedded in the audio file.
- Custom dark/light backgrounds and accent colors, including blue.
- Updates yt-dlp automatically on launch.

### Requirements
- Android 10 (API 29) or newer.
- A 64-bit (arm64) phone for the prebuilt APK.

### Build the APK without Android Studio (GitHub Actions)
1. Create a free account on github.com and a **public** repository.
2. Upload `YtClip.zip` to the root of the repository (**Add file → Upload files**).
3. Create the file `.github/workflows/build.yml` (it unzips the project, builds it, and publishes the APK to Releases).
4. Open **Actions → Build APK → Run workflow**, then wait about 2 minutes for the green check mark.
5. Open **Releases**, download `app-debug.apk`, and install it.

> The APK is about 55–65 MB when built for arm64 only. Download it over Wi-Fi and keep the browser open until it finishes. If the install fails with "package seems invalid", the download was incomplete: delete the file and download it again.

### Install
- Open the APK and allow "Install from unknown sources" if Android asks.
- If Play Protect shows a warning, choose "Install anyway" (the app is self-built and not signed by Google Play).

### Usage
1. Wait until the app shows **Ready**.
2. Paste the YouTube link.
3. (Optional) Enter start and end times.
4. Press **Download**. Keep the app open until it finishes.

### Notes
- Only download content you own or have permission to download. Downloading from YouTube may violate its Terms of Service.
- If downloads stop working, YouTube probably changed something. Open the app with internet access so yt-dlp can update itself.

---

<a name="arabic"></a>
<div dir="rtl">

## العربية

**YtClip** تطبيق أندرويد صغير يحمّل فيديوهات يوتيوب باستخدام [yt-dlp](https://github.com/yt-dlp/yt-dlp) ويمكنه قصّها بحسب وقت البداية والنهاية أثناء التحميل. يعتمد على مكتبة [youtubedl-android](https://github.com/yausername/youtubedl-android) التي تضم yt-dlp وffmpeg داخل التطبيق.

### المزايا
- الصق الرابط، أو شاركه من تطبيق يوتيوب (مشاركة ← YtClip).
- اختر جودة متاحة حتى 4K، أو نزّل الصوت بصيغة M4A أو MP3.
- تظهر قائمة الجودات السريعة أولاً؛ ولا يبدأ الفحص الكامل الأبطأ إلا عند طلبه.
- قصّ المقطع باستخدام شريط التحديد أو بإدخال الساعات والدقائق والثواني.
- شاهد الحجم التقديري للفيديو كاملاً وللمقطع المحدد قبل التنزيل؛ ويعرض تبويب الملفات الحجم الفعلي بعد الحفظ.
- قص دقيق على مستوى الإطار اختيارياً (أبطأ، ويعيد ترميز الفيديو).
- قائمة تنزيلات تعمل في الخلفية مع التقدم والإيقاف والاستئناف والإلغاء والإشعارات.
- تظهر معاينة الفيديو داخل التطبيق دون إنشاء صورة JPG منفصلة، وتُضمّن صورة الغلاف في ملف الصوت.
- خلفيات داكنة وفاتحة وألوان تمييز قابلة للتخصيص، ومنها الأزرق.
- يحدّث yt-dlp تلقائياً عند فتح التطبيق.

### المتطلبات
- أندرويد 10 (API 29) أو أحدث.
- هاتف بمعالج 64 بت (arm64) لتشغيل ملف APK الجاهز.

### بناء ملف APK دون Android Studio (عبر GitHub Actions)
1. أنشئ حساباً مجانياً على github.com ومستودعاً **عاماً (Public)**.
2. ارفع الملف `YtClip.zip` إلى جذر المستودع (**Add file ← Upload files**).
3. أنشئ الملف `.github/workflows/build.yml` (يفك ضغط المشروع ويبنيه وينشر ملف APK في قسم Releases).
4. افتح **Actions ← Build APK ← Run workflow**، وانتظر نحو دقيقتين حتى تظهر علامة الصح الخضراء.
5. افتح **Releases** ونزّل `app-debug.apk` ثم ثبّته.

> حجم الملف نحو 55 إلى 65 ميغابايت عند البناء لمعالجات arm64 فقط. نزّله عبر الواي فاي، وأبقِ المتصفح مفتوحاً حتى يكتمل التنزيل. وإن ظهرت رسالة «الحزمة تبدو غير صالحة» عند التثبيت، فالتنزيل لم يكتمل: احذف الملف وأعد تنزيله.

### التثبيت
- افتح ملف APK وفعّل «التثبيت من مصادر غير معروفة» إن طلب أندرويد ذلك.
- إن ظهر تحذير من Play Protect فاختر «التثبيت على أي حال»، لأن التطبيق مبني ذاتياً وغير موقّع من متجر جوجل.

### طريقة الاستخدام
1. انتظر حتى تظهر عبارة **Ready** في التطبيق.
2. الصق رابط الفيديو.
3. (اختياري) أدخل وقت البداية والنهاية.
4. اضغط **Download**، وأبقِ التطبيق مفتوحاً حتى ينتهي.

### ملاحظات
- حمّل فقط المحتوى الذي تملكه أو لديك إذن بتحميله، فقد يخالف التحميل من يوتيوب شروط الخدمة.
- إن توقف التحميل فغالباً غيّر يوتيوب شيئاً في موقعه. افتح التطبيق وأنت متصل بالإنترنت ليحدّث yt-dlp نفسه.

</div>
