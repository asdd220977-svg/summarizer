# chat-summarizer

[English](#english) | [العربية](#العربية)

---

## English

A skill for AI agents that summarizes chats, videos, and written content in a consistent, trustworthy format.

### What it summarizes

| Type | Supported formats |
|------|-------------------|
| Chats | WhatsApp export (ZIP), Telegram (HTML / links) |
| Videos | YouTube (regular videos, Shorts, Live streams) |
| Documents | Word (.docx, .doc), PDF (with OCR for scanned files) |
| Spreadsheets and slides | Excel (.xlsx), CSV, PowerPoint (.pptx) |
| Web | Web pages (via URL) |
| Plain text | Text, Markdown, code files |

### Summarization rules

- **Claims vs. facts:** speaker claims are kept separate from verified facts.
- **Attribution:** every point is credited to its source (sender and date/time for chats; author and date for documents, when available).
- **Offers vs. executed deals:** listed prices and offers are distinguished from actual transactions.
- **Clear structure:** headings, tables, and lists.
- **Large files:** split into chunks, summarized per chunk, then merged.
- **Data files:** key indicators, trends, and outliers.
- **Core Takeaway:** every summary ends with a short "أهم حاجة" conclusion.
- **No hallucination:** only what exists in the source is reported.
- **Output language:** simple Egyptian Arabic, with technical terms kept in English.

### Repository structure

```
summarizer/
├── SKILL.md                              # Skill definition, rules, and protocol
├── references/
│   └── whatsapp-export-parsing.md        # Notes on parsing WhatsApp exports
├── .gitignore
└── README.md
```

### Usage

Place the skill folder where your agent loads skills, then send it a file, a chat export, a video link, or a web page URL and ask for a summary.

### Privacy note

Never commit real chat exports, phone numbers, bank details, or API tokens to this repository.

---

## العربية

مهارة (Skill) لوكلاء الذكاء الاصطناعي بتلخّص المحادثات والفيديوهات والمحتوى المكتوب بشكل موحّد وموثوق.

### بتلخّص إيه

| النوع | الصيغ المدعومة |
|------|----------------|
| محادثات | واتساب (ملف ZIP)، تيليجرام (HTML / روابط) |
| فيديوهات | يوتيوب (فيديوهات عادية، Shorts، Live) |
| مستندات | Word (.docx, .doc)، PDF (مع OCR للملفات الممسوحة) |
| جداول وعروض | Excel (.xlsx)، CSV، PowerPoint (.pptx) |
| ويب | صفحات الويب (عن طريق الرابط) |
| نصوص | Text، Markdown، ملفات الكود |

### قواعد التلخيص

- **فصل الادعاءات عن الحقائق:** كلام المتحدث بيتفصل عن المعلومة المؤكدة.
- **النسب للمصدر:** كل نقطة بتتنسب لصاحبها (اسم المرسل والتاريخ والوقت في المحادثات، والكاتب والتاريخ في المستندات لو متاحين).
- **العروض مقابل التنفيذ الفعلي:** الأسعار المعروضة بتتفرق عن الصفقات اللي اتنفذت فعلاً.
- **هيكل واضح:** عناوين وجداول وقوائم.
- **الملفات الكبيرة:** بتتقسم وتتلخص جزء جزء، وبعدين بتتجمع.
- **ملفات البيانات:** استخراج المؤشرات والاتجاهات والقيم الشاذة.
- **أهم حاجة:** كل ملخص بيخلص بخلاصة قصيرة.
- **صفر هلوسة:** بنذكر بس اللي موجود في المصدر.
- **لغة الإخراج:** عامية مصرية مبسطة، والمصطلحات التقنية بالإنجليزي.

### هيكل المستودع

```
summarizer/
├── SKILL.md                              # تعريف المهارة والقواعد والبروتوكول
├── references/
│   └── whatsapp-export-parsing.md        # ملاحظات تحليل ملفات تصدير واتساب
├── .gitignore
└── README.md
```

### الاستخدام

حط فولدر المهارة في المكان اللي الـ agent بيحمّل منه المهارات، وبعدين ابعتله ملف أو تصدير محادثة أو رابط فيديو أو صفحة ويب واطلب تلخيص.

### ملاحظة خصوصية

ما ترفعش على المستودع محادثات حقيقية أو أرقام تليفونات أو بيانات بنكية أو توكنات.
