<div align="center">

<img src="https://xtop-app.pages.dev/logo.png" width="96" alt="XTop" />

# XTop

**جزيرة واحدة… ومساحة شغلك كلها.**

لوحة عائمة للمطوّرين — دوّر على مشاريعك، افتحها في المحرر الصح والترمنال الصح،
وخلّي الملاحظات والـ API والـ git والاجتماعات والتذكيرات على بُعد ضغطة زرار.
واسأل X، المساعد اللي جوه البرنامج، عن أي نافذة — بيشتغل بأداة الـ AI اللي عندك
أصلًا، من غير أي مفتاح API.

[![تحميل](https://img.shields.io/github/v/release/kareem-elgamal/XTop?style=for-the-badge&color=0b6fc4&label=%D8%AA%D8%AD%D9%85%D9%8A%D9%84)](https://github.com/kareem-elgamal/XTop/releases/latest)
[![الوثائق](https://img.shields.io/badge/docs-xtop--app.pages.dev-6b3fb0?style=for-the-badge)](https://xtop-app.pages.dev/ar/)
[![ويندوز](https://img.shields.io/badge/Windows-10%20%2F%2011-555?style=for-the-badge)](https://xtop-app.pages.dev/ar/guide/download)

[English](README.md) · [الوثائق](https://xtop-app.pages.dev/ar/) · [التحميل](https://github.com/kareem-elgamal/XTop/releases/latest)

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://xtop-app.pages.dev/shots/island-expanded-ar-dark.png">
  <img src="https://xtop-app.pages.dev/shots/island-expanded-ar-light.png" width="560" alt="جزيرة XTop مفتوحة: الاختصارات السريعة وآخر مشاريعك.">
</picture>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://xtop-app.pages.dev/shots/island-chat-ar-dark.png">
  <img src="https://xtop-app.pages.dev/shots/island-chat-ar-light.png" width="560" alt="X، المساعد اللي جوه البرنامج، بيرد في الجزيرة ومعاه الملفات اللي اتغيّرت.">
</picture>

</div>

<div dir="rtl" align="right">

## التحميل

**[⭳ حمّل XTop ←](https://github.com/kareem-elgamal/XTop/releases/latest)**

| الملف | هو إيه |
| --- | --- |
| **`XTop Setup <version>.exe`** | المثبّت. بيضيف اختصار في قائمة ابدأ وعلى سطح المكتب، وأداة إلغاء تثبيت. خُد ده. |
| **`XTop-portable-<version>.exe`** | ملف واحد بيشتغل على طول. مناسب للفلاشة أو لجهاز مش قادر تثبّت عليه. |

الاتنين نفس البرنامج، ومحدش فيهم محتاج Node.js ولا أي حاجة تتثبّت الأول.

> [!WARNING]
> البرنامج مش موقّع رقميًا، فـ SmartScreen هيقول إن الناشر غير معروف.
> اختار **More info → Run anyway**.

XTop برنامج **ويندوز**. بيفتح المحرر بتاعك، وبيشغّل Windows Terminal و WSL،
ومحتاج جلسة سطح مكتب ويندوز عشان أيقونة شريط المهام والجزيرة.

## بعد ما يشتغل

XTop مش بيفتح نافذة خاصة بيه — بيروح لـ **شريط المهام**، وبيحط كبسولة صغيرة — الجزيرة — على
حرف الشاشة. اضغط <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>Space</kbd>، أو اضغط على
الجزيرة، أو أيقونة شريط المهام، عشان تفتح اللوحة — وخانة البحث بتكون جاهزة على طول.

كمّل من **[البداية ←](https://xtop-app.pages.dev/ar/guide/getting-started)**

## اللي جواه

| | |
| --- | --- |
| **[مشاريعك بأي اسم](https://xtop-app.pages.dev/ar/services/panel)** | مجموعات وأسماء بديلة وبحث مرن. `Enter` بيفتح المحرر، و `Shift+Enter` بيفتح ترمنال — في ويندوز أو في WSL حسب المشروع. |
| **[أوامر سريعة في ترمنال حقيقي](https://xtop-app.pages.dev/ar/services/commands-terminal)** | أوامر لكل مشروع ولكل مجموعة وأوامر عامة، بتشتغل في جلسة pty بتبويبات محتفظة بالمخرجات. |
| **[اختبار API عارف مشروعك](https://xtop-app.pages.dev/ar/services/api)** | الـ base URL بييجي من `.env` بتاع المشروع نفسه، والطلبات المحفوظة بتتخزن جوه المشروع، و `Ctrl+Shift+A` بيفتح تبويب سريع من الكليب بورد. |
| **[اجتماعات مفرَّغة على جهازك](https://xtop-app.pages.dev/ar/services/meetings)** | المايك وصوت النظام، التفريغ بيتم على جهازك بـ Whisper، وبعدين تلخيص لقرارات ومهام. |
| **[ملاحظات Markdown على الهارد](https://xtop-app.pages.dev/ar/services/notes)** | دفتر عام + ملاحظات لكل مشروع، ملفات `.md` تقدر تعملها commit أو sync أو grep. |
| **[معلومات Git](https://xtop-app.pages.dev/ar/services/git)** | الفرع الحالي، وكام commit قدام/ورا، وحالة الملفات، وتبديل الفروع، والرسم البياني للـ commits. |
| **[مواقيت الصلاة والأذكار](https://xtop-app.pages.dev/ar/services/islamic)** | تنبيه بعد الأذان بدقائق، وزرار تأجيل بيهرب من الماوس، وأذكار الصباح والمساء بعدّادات. |
| **[التذكيرات](https://xtop-app.pages.dev/ar/services/reminders)** | مرة واحدة أو متكررة، مع تأجيل، وبتفضل شغّالة حتى لو البرنامج اتقفل. |
| **[النسخ الاحتياطي والاستعادة](https://xtop-app.pages.dev/ar/services/backup)** | نسخة `.zip` بضغطة أو بجدول زمني، في أي فولدر — وممكن يكون فولدر مزامن مع السحابة. |
| **[مشاريع بدء التشغيل](https://xtop-app.pages.dev/ar/services/startup)** | مشاريع بتفتح نفسها في المحرر أو الترمنال أول ما البرنامج يشتغل. |

عربي وإنجليزي في كل النوافذ، الإنجليزية هي الافتراضية، و RTL كامل مع العربية.

## الوثائق

كل حاجة على **[xtop-app.pages.dev](https://xtop-app.pages.dev/ar/)** بالعربي والإنجليزي:

- [البداية](https://xtop-app.pages.dev/ar/guide/getting-started) — أول عشر دقايق
- [اختصارات الكيبورد](https://xtop-app.pages.dev/ar/guide/shortcuts) — كلها
- [الإعدادات](https://xtop-app.pages.dev/ar/reference/settings) · [أين تُحفظ البيانات](https://xtop-app.pages.dev/ar/reference/data)
- [حل المشاكل](https://xtop-app.pages.dev/ar/reference/troubleshooting)

## عن الـ repo ده

الـ repo ده هو بيت **التحميل والوثائق** لـ XTop. الكود المصدري مش منشور هنا.

لقيت مشكلة أو عايز خاصية؟ افتح
[issue](https://github.com/kareem-elgamal/XTop/issues).

</div>

---

<div align="center">

من صنع [Karim Sayed](https://github.com/kareem-elgamal)

</div>
