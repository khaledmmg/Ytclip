<div align="center">

# YtClip

**Download, trim and keep videos & audio — fast, clean, and fully yours.**
A premium Android downloader built on yt-dlp · FFmpeg · aria2c

[English](#english) · [العربية](#arabic)

</div>

---

<a name="english"></a>
## English

### Why YtClip
YtClip pairs the power of **yt-dlp** with an interface designed like a modern iOS/Material app:
a full format list with accurate sizes, a precise trimmer, live speed meter, queue management and a built-in browser —
all in one APK, no ads, no accounts required.

### Highlights
| | |
|---|---|
| **Browse & download** | Built-in browser (YouTube, Facebook, Instagram, TikTok, X) with a one-tap **Download** button, ad/tracker blocking, and link detection from clipboard, Share and "Open with". |
| **Smart quality list** | Every real quality from 144p to **4K**, plus **M4A / MP3 128K / MP3 320K**, each with an honest size estimate (the size of the file that will actually be downloaded). |
| **Precise trimming** | Two modes: a range **slider** with ±1 s / ±10 s nudges and presets, or **type** hours:minutes:seconds. Sizes update live for the clip, and the sheet shows *“Clip 0:45 of 3:10:40 · about 34 MB”*. |
| **Cover art inside the file** | The thumbnail is always embedded as cover art (no stray image files). Title, chapters and metadata are embedded too. |
| **Subtitles & translation** | Optional: Original, English, Arabic, French, Spanish or any language code — including YouTube's auto-translated captions. Embed in the video or save `.srt`. Or download subtitles only. |
| **Turbo downloads** | aria2c with up to 16 connections per file, parallel queue (1–3 at once), speed limit, automatic safe fallback and **auto-retry** when the connection drops. |
| **Live speed meter** | Total speed, peak and average with a live graph on the Downloads tab, per-file speed & ETA, and speed in the notification. |
| **Queue control** | Pause / resume / cancel each download, *Pause all*, *Cancel all*, background downloading with a foreground notification, resume from partial files. |
| **Playlists & batch** | Pick videos from a playlist, or paste several links at once. Optional one-tap mode (no sheet). |
| **SponsorBlock** | Optionally cut sponsor / intro / outro segments. |
| **Library** | Search, sort, rename, share, delete; thumbnails, `720P | duration` labels and **CC** badges; storage totals. |
| **Themes** | 4 backgrounds + **Auto** (follows the system) × 10 vivid accents, subtle animations (can be turned off). |
| **Google account** | Sign in inside the app (or import `cookies.txt`) for age-restricted videos and bot checks. |
| **Pro touches** | Low-storage warning, launcher shortcuts (*Paste & download*, *Downloads*), crash report on next launch, full error log for failed downloads. |

### Install (no Android Studio needed)
1. Create a free GitHub account and a **public** repository.
2. Upload `YtClip.zip` to the repository root and add `.github/workflows/build.yml` (below).
3. Open **Actions → Build APK → Run workflow** and wait ~2–3 minutes.
4. Open **Releases**, download `app-debug.apk`, install it (allow “unknown sources”; choose *Install anyway* on Play Protect).

```yaml
name: Build APK
on:
  workflow_dispatch:
permissions:
  contents: write
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: unzip -q YtClip.zip
      - uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: 17
      - uses: gradle/actions/setup-gradle@v4
        with:
          gradle-version: 8.9
      - run: gradle assembleDebug
        working-directory: YtClip
      - uses: softprops/action-gh-release@v2
        with:
          tag_name: build-${{ github.run_number }}
          files: YtClip/app/build/outputs/apk/debug/app-debug.apk
```

### Using the app
1. **Browse** → open a video (or paste a link on Home) → tap **Download**.
2. Pick a quality in the list, optionally **trim**, add **subtitles**, then **Download**.
3. Follow progress in **Downloads** (speed meter, per-file controls). Finished files appear under **Downloaded** and in your gallery (`Movies/YtClip`, `Music/YtClip`).

### Settings (download settings only)
Default quality · metadata & cover art · folder name · fast reading · turbo downloads · simultaneous downloads · connections · speed limit · ask before downloading · Wi-Fi only · auto-retry · precise trimming · Google account · **engine version & update**.

### Troubleshooting
- **Qualities take a while the first time.** YouTube's player must be processed once; YtClip keeps a persistent cache and warms it up in the background. Later reads take seconds. Settings → *Download engine* shows the yt-dlp version and updates it.
- **Only 360p is listed.** Wait for *“Loading all qualities…”* to finish; the quick read only knows a few formats.
- **A download failed.** YtClip retries in three steps (rich → direct-safe → single-file compatibility mode), restarts cleanly, and treats an unavailable/rate-limited subtitle as non-fatal. If FFmpeg's clip cut fails, a device stream-copy cutter is tried for compatible files; it may start at the next keyframe and be less precise. If it still fails, tap the item in **Downloads** to see the full log (copy / share it).
- **Google refuses sign-in inside the app.** Use *Import cookies.txt* from your browser instead.
- **Turbo not working on a site.** YtClip retries automatically without it; you can also switch it off in Settings.
- **Keep the engine updated** (Settings → Download engine). Recent yt-dlp releases also fix a security issue related to aria2c.

### How it works
`MainActivity` (UI) → `DL` (process-wide engine: queue, cache, retries, MediaStore saving) → **youtubedl-android** (yt-dlp + Python + QuickJS) with **FFmpeg** and **aria2c**.
The engine lives for the whole process, so rotating the phone or changing the theme never interrupts a download. A full details file is reused when it is ready; otherwise the download starts from the URL rather than relying on the quick, potentially incomplete format list.

### Privacy
No analytics, no ads, no server. Network calls go only to the sites you use, YouTube's public suggestion/oEmbed endpoints, SponsorBlock (if enabled) and GitHub (engine updates). Cookies stay on your device.

### Legal
Download only content you own or have permission to download. Respect the terms of the sites you use and local law.

### Credits
[yt-dlp](https://github.com/yt-dlp/yt-dlp) · [youtubedl-android](https://github.com/yausername/youtubedl-android) · [FFmpeg](https://ffmpeg.org) · [aria2](https://aria2.github.io) · [QuickJS](https://bellard.org/quickjs/) · [Material Components](https://github.com/material-components/material-components-android)

### Changelog (recent)
- **9.1** — fixes delayed trim-time fields and adds a clip-length badge; adds clean three-stage download fallback and non-fatal subtitles; measures speed from real file growth (including turbo and clips), estimates ETA when size information is available, and adds a device stream-copy clip fallback for compatible media.
- **9.0** — vivid palettes + Auto theme, new app icon, grouped settings, pinned Download bar, live speed meter, search suggestions & recent searches, rename, low-storage warning, auto-retry, launcher shortcuts, faster reads (lighter details, link prefetch, faster defaults).
- **8.0** — persistent yt-dlp cache (fixes minutes-long reads), accurate trim-aware sizes, embedded cover art, refined icons.
- **7.x** — aria2c turbo, playlists, batch links, SponsorBlock, crash reporter, SnapTube-style quality list.

---

<a name="arabic"></a>
<div dir="rtl">

## العربية

### لماذا YtClip
يجمع YtClip قوة **yt-dlp** مع واجهة أنيقة بأسلوب تطبيقات iOS الحديثة: قائمة جودات كاملة بأحجام دقيقة، وقصّ مضبوط، وعدّاد سرعة حيّ، وإدارة قائمة التحميل، ومتصفح مدمج — في ملف APK واحد، بلا إعلانات ولا حساب إجباري.

### أبرز المزايا
- **تصفّح وتحميل:** متصفح مدمج (يوتيوب وفيسبوك وإنستغرام وتيك توك وإكس) مع زر **Download** بلمسة واحدة، وحجب الإعلانات والمتتبّعات، والتقاط الروابط من الحافظة والمشاركة و«فتح بواسطة».
- **قائمة جودات ذكية:** كل الجودات الحقيقية من 144p إلى **4K** مع **M4A وMP3 128K وMP3 320K**، وبجانب كل منها حجم تقديري صادق للملف الذي سيُحمَّل فعلاً.
- **قصّ دقيق:** وضعان: **شريط منزلق** مع أزرار ±1 و±10 ثوانٍ وإعدادات جاهزة، أو **كتابة** الساعات والدقائق والثواني. تتحدث الأحجام فوراً، ويعرض الملخص: «Clip 0:45 of 3:10:40 · about 34 MB».
- **غلاف داخل الملف:** تُضمَّن الصورة المصغرة دائماً غلافاً داخل الملف (دون ملفات صور منفصلة)، مع العنوان والفصول والبيانات الوصفية.
- **الترجمة:** اختيارية: الأصلية أو الإنجليزية أو العربية أو الفرنسية أو الإسبانية أو أي رمز لغة، وتشمل الترجمة التلقائية من يوتيوب. تُضمَّن في الفيديو أو تُحفظ بصيغة `.srt`، أو تحمّل الترجمة وحدها.
- **تحميل توربو:** aria2c بما يصل إلى 16 اتصالاً للملف، وقائمة متوازية (1–3 معاً)، وحد للسرعة، وعودة تلقائية آمنة، و**إعادة محاولة تلقائية** عند انقطاع الاتصال.
- **عدّاد السرعة الحي:** السرعة الكلية وأعلى سرعة والمتوسط مع رسم بياني حيّ في تبويب Downloads، وسرعة كل ملف ووقته المتبقي، والسرعة في الإشعار.
- **التحكم بالقائمة:** إيقاف واستئناف وإلغاء لكل ملف، وإيقاف الكل وإلغاء الكل، والتحميل في الخلفية بإشعار دائم، والاستئناف من الأجزاء الجزئية.
- **قوائم التشغيل والدفعات:** اختر فيديوهات من قائمة تشغيل، أو الصق عدة روابط معاً. ووضع اختياري بلمسة واحدة دون نافذة.
- **SponsorBlock:** قصّ مقاطع الرعاة والمقدمات والخواتيم اختيارياً.
- **المكتبة:** بحث وفرز وإعادة تسمية ومشاركة وحذف، مع صور مصغرة وعلامات `720P | المدة` وشارة **CC** وإجماليات المساحة.
- **السمات:** 4 خلفيات + **تلقائي** (يتبع النظام) × 10 ألوان نابضة، وحركات خفيفة يمكن إيقافها.
- **حساب جوجل:** سجّل الدخول داخل التطبيق (أو استورد `cookies.txt`) لتخطي قيود العمر وفحوص الروبوت.
- **لمسات احترافية:** تحذير المساحة المنخفضة، واختصارات الشاشة الرئيسية (*Paste & download* و*Downloads*)، وتقرير الانهيار عند الفتح التالي، وسجل كامل لأخطاء التحميل.

### التثبيت (دون Android Studio)
1. أنشئ حساباً مجانياً على GitHub ومستودعاً **عاماً**.
2. ارفع `YtClip.zip` إلى جذر المستودع وأضف الملف `.github/workflows/build.yml` (المذكور أعلاه).
3. افتح **Actions ← Build APK ← Run workflow** وانتظر نحو 2–3 دقائق.
4. افتح **Releases** ونزّل `app-debug.apk` وثبّته (فعّل «مصادر غير معروفة»، واختر «التثبيت على أي حال» عند تحذير Play Protect).

### طريقة الاستخدام
1. **Browse** ← افتح فيديو (أو الصق رابطاً في الصفحة الرئيسية) ← اضغط **Download**.
2. اختر الجودة من القائمة، ثم **القص** اختيارياً، وأضف **الترجمة** إن شئت، ثم **Download**.
3. تابع التقدم في **Downloads** (عدّاد السرعة وأزرار كل ملف). تظهر الملفات المكتملة في **Downloaded** وفي معرض الصور (`Movies/YtClip` و`Music/YtClip`).

### الإعدادات (إعدادات التحميل فقط)
الجودة الافتراضية · البيانات الوصفية والغلاف · اسم المجلد · القراءة السريعة · التحميل التوربو · التنزيلات المتزامنة · الاتصالات · حد السرعة · السؤال قبل التحميل · واي فاي فقط · إعادة المحاولة التلقائية · القص الدقيق افتراضياً · حساب جوجل · **إصدار المحرك وتحديثه**.

### حل المشاكل
- **الجودات تتأخر في أول مرة:** يحتاج مشغّل يوتيوب إلى معالجة واحدة؛ يحتفظ YtClip بذاكرة مؤقتة دائمة ويسخّنها في الخلفية، فتصير القراءات التالية في ثوانٍ. وفي الإعدادات صف *Download engine* يعرض إصدار yt-dlp ويحدّثه.
- **تظهر 360p فقط:** انتظر انتهاء «Loading all qualities…»؛ فالقراءة السريعة لا تعرف إلا تنسيقات قليلة.
- **فشل التحميل:** يعيد YtClip المحاولة على ثلاث مراحل (غنية ثم آمنة من الرابط ثم وضع توافق بملف واحد) مع تنظيف الملفات الجزئية، ويعدّ تعذر الترجمة غير قاتل. إذا فشل قص FFmpeg، تُجرّب أداة قص من النظام للملفات المتوافقة؛ وقد يبدأ القص من أقرب إطار رئيسي ويكون أقل دقة. وإن استمر الفشل فاضغط على الملف في **Downloads** لترى السجل كاملاً (انسخه أو شاركه).
- **ترفض جوجل تسجيل الدخول داخل التطبيق:** استخدم *Import cookies.txt* من متصفحك.
- **لا يعمل التوربو مع موقع ما:** يعيد YtClip المحاولة تلقائياً بدونه، ويمكنك إيقافه من الإعدادات.
- **أبقِ المحرك محدَّثاً** (الإعدادات ← Download engine)؛ فالإصدارات الحديثة من yt-dlp تعالج أيضاً ثغرة أمنية متعلقة بـ aria2c.

### كيف يعمل
`MainActivity` (الواجهة) ← `DL` (محرك يعيش مع العملية: القائمة والذاكرة المؤقتة وإعادة المحاولة والحفظ في MediaStore) ← **youtubedl-android** (yt-dlp وPython وQuickJS) مع **FFmpeg** و**aria2c**. لا يضيع التحميل عند تدوير الهاتف أو تغيير السمة. يُعاد استخدام ملف التفاصيل الكامل إن كان جاهزاً؛ وإلا يبدأ التنزيل من الرابط لتجنب الاعتماد على قائمة الجودة السريعة غير المكتملة.

### الخصوصية
لا تحليلات ولا إعلانات ولا خادم. تذهب الاتصالات فقط إلى المواقع التي تستخدمها، وإلى واجهتَي الاقتراحات وoEmbed العامتين من يوتيوب، وSponsorBlock (إن فعّلته)، وGitHub (لتحديث المحرك). وتبقى ملفات الكوكيز على جهازك.

### تنبيه قانوني
حمّل فقط المحتوى الذي تملكه أو لديك إذن بتحميله، والتزم بشروط المواقع التي تستخدمها وبالقانون المحلي.

</div>
