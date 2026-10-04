# حساباتي — النسخة المحلية

تطبيق حسابات شخصية بيشتغل على الموبايل. البيانات على الموبايل نفسه، ونسخة احتياطية على Google Drive بتاع صاحب الموبايل.

## الملفات

| الملف | بيعمل إيه |
| --- | --- |
| `index.html` | التطبيق كله (الشكل والحسابات). ده اللي بيتعدّل في أغلب التحديثات |
| `sw.js` | بيخلي التطبيق يشتغل من غير نت |
| `manifest.webmanifest` | اسم التطبيق وأيقونته عشان يتثبّت |
| `icon-*.png` | الأيقونات |
| `.nojekyll` | ملف فاضي لازم يفضل موجود (عشان GitHub Pages) |

## ١. ارفعه على GitHub Pages (مجاني)

1. اعمل حساب على github.com.
2. اضغط **+** فوق ← **New repository**. سمّيه بالظبط: `اسمك-على-جيت-هب.github.io` (مثلاً لو اليوزر `hossam80` يبقى `hossam80.github.io`). خليه **Public**، واضغط **Create repository**.
3. اضغط **uploading an existing file**، واسحب كل الملفات اللي في الفولدر ده (ومعاهم `.nojekyll`)، واضغط **Commit changes**.
4. **Settings** ← **Pages** ← في **Branch** اختار `main` و `/ (root)` ← **Save**.
5. استنى دقيقتين، وافتح `https://اسمك.github.io` من كروم على الموبايل، ومن التلات نقط اختار **تثبيت التطبيق** (أو إضافة إلى الشاشة الرئيسية).

الكود بيبقى ظاهر للناس لأن الريبو Public، بس **بياناتك مش جوه الكود**، دي على موبايلك بس.

## ٢. النسخة الاحتياطية على Google Drive (مرة واحدة)

1. ادخل console.cloud.google.com، واعمل **مشروع جديد** اسمه `Hesabaty`.
2. من القايمة: **APIs & Services** ← **Library** ← دوّر على **Google Drive API** ← **Enable**.
3. **Google Auth Platform** (أو OAuth consent screen) ← **Get started**:
   - اسم التطبيق: `حساباتي`، وإيميلك في الخانات المطلوبة.
   - Audience: **External**.
4. **Data Access** ← **Add or remove scopes** ← اختار `.../auth/drive.file` ← **Update** ← **Save**.
5. **Audience** ← **Publish app** عشان أي حد يقدر يربط حسابه. (الصلاحية `drive.file` مش محتاجة مراجعة من جوجل، لأن التطبيق بيشوف ملفاته هو بس.)
6. **Clients** ← **Create client** ← النوع **Web application**:
   - في **Authorized JavaScript origins** حط: `https://اسمك.github.io`
   - اضغط **Create**، وانسخ الـ **Client ID** (بيخلص بـ `.apps.googleusercontent.com`).
7. في GitHub افتح `index.html` ← القلم ✏️ ← دوّر على السطر:
   `var GOOGLE_CLIENT_ID = '';`
   وحط الـ Client ID بين العلامتين ← **Commit changes**.

الـ Client ID مش سر، عادي يبقى ظاهر في الكود.

## ٣. APK (اختياري)

1. ادخل pwabuilder.com وحط لينك موقعك ← **Package For Stores** ← **Android** ← **Generate**.
2. نزّل الملف المضغوط. جواه ملف APK تثبّته أو تبعته لأي حد، وملف اسمه `assetlinks.json`.
3. عشان التطبيق يفتح شاشة كاملة من غير شريط اللينك: في GitHub اعمل فولدر `.well-known` وارفع فيه `assetlinks.json` (اضغط **Add file** ← **Create new file** واكتب الاسم `.well-known/assetlinks.json` والزق محتواه).

## التعديل بعدين

- خد الملف المعدّل (غالباً `index.html`)، وفي GitHub: **Add file** ← **Upload files** ← اسحبه ← **Commit**.
- في دقيقة الموقع بيتحدث، وأي حد مثبّت التطبيق بياخد التحديث أول ما يفتحه وهو على نت.
- البيانات اللي على الموبايلات مش بتتأثر بالتحديث.
