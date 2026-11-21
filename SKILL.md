---
name: chat-summarizer
description: Summarize chats, videos, and written content in a consistent, trustworthy format. Use when the user sends a WhatsApp export (ZIP/TXT), a Telegram export or link, a YouTube link (video, Shorts, Live), a Word/PDF/Excel/CSV/PowerPoint file, a web page URL, or any text and asks for a summary, recap, or "لخصلي". Separates claims from facts, credits sources, and ends with a "أهم حاجة" takeaway.
---

# Chat Summarizer

Turns long or messy content into a short, structured, trustworthy summary.

## Supported inputs

| Type | Formats | How to extract |
|------|---------|----------------|
| Chats | WhatsApp export (ZIP / `_chat.txt`), Telegram export (HTML / JSON) or public link | See `references/whatsapp-export-parsing.md` |
| Videos | YouTube video, Shorts, Live | Transcript + metadata (title, channel, date, duration) |
| Word | `.docx`, `.doc` | `python-docx` |
| PDF | `.pdf` | `pdfplumber` or `pymupdf`; OCR if the PDF is scanned |
| Spreadsheets | `.xlsx`, `.csv` | `pandas` / `openpyxl` |
| Slides | `.pptx` | `python-pptx` |
| Web pages | URL | Fetch the page and extract the main text |
| Plain text | `.txt`, `.md`, code | Read directly |

If a file or link cannot be read, say so clearly. Never guess its content.

## Core rules

1. **Zero hallucination.** Report only what exists in the source. If something is unclear or missing, write "غير موضّح في المصدر".
2. **Claims vs. facts.** Keep what a speaker or author *claims* separate from what is *verified* or *documented*. Use wording like "يدّعي المتحدث أن..." for unverified statements.
3. **Attribution.**
   - Chats: sender name + date/time for each key point.
   - Videos: channel, publish date, duration, and timestamps for key points.
   - Documents and web pages: author and date, when available in the metadata.
4. **Offers vs. executed deals.** For prices, numbers, and deals, distinguish listed or offered prices from transactions that actually happened. Never present an offer as a completed deal.
5. **Structure.** Use headings, short bullets, and tables where they help. Keep it as short as the content allows.
6. **Large files.** Split into chunks, summarize each chunk, then merge into one summary. Do not skip sections.
7. **Tables and data.** Extract key indicators, trends, totals, and outliers. Do not list every row.
8. **Sensitive data.** Do not repeat full phone numbers, bank accounts, IBANs, passwords, or tokens found in the source. Mask them (e.g. `+212****3319`) and mention that they exist.
9. **Red flags.** If the content looks like a scam, a paid-service ad disguised as advice, or a policy violation (e.g. buying views, fake engagement), say so in a separate "ملاحظات" section.
10. **Closing takeaway.** Every summary ends with `✅ أهم حاجة:` followed by 1 to 3 sentences with the single most important conclusion.

## Output language

- Simple Egyptian Arabic, direct and clear.
- Technical terms stay in English (e.g. Shorts, Playlist, Retention, Invalid Traffic).
- If the user writes in another language, answer in that language.

## Output templates

### Chats (WhatsApp / Telegram)

```
ملخص محادثة: <اسم الجروب أو الشخص>
الفترة: <من تاريخ> إلى <تاريخ>
عدد المشاركين: <n> | عدد الرسائل: <n>

📌 النقاط الرئيسية
- <نقطة> (الاسم، التاريخ والوقت)

🧩 القرارات والمواعيد
- <قرار أو موعد> (الاسم، التاريخ)

💰 الأسعار والأرقام
| البند | معروض | منفّذ فعلاً | المصدر |

❓ أسئلة معلقة
- <سؤال لم يُرد عليه>

✅ أهم حاجة:
```

### Videos (YouTube)

```
ملخص فيديو: <العنوان>
القناة: <الاسم> | النشر: <التاريخ> | المدة: <mm:ss>
نوع الفيديو: <تعليمي / مراجعة / إعلان...>

📌 النقاط الرئيسية
🎬 التفاصيل بالتسلسل الزمني (جدول: الوقت | المحتوى)
💡 نصائح وآراء المتحدث
⚠️ ملاحظات هامة (ادعاءات غير مثبتة، إعلانات، مخالفات سياسات)
✅ أهم حاجة:
```

### Documents, PDFs, and web pages

```
ملخص: <العنوان>
المصدر: <ملف / رابط> | الكاتب: <لو متاح> | التاريخ: <لو متاح>

📌 الفكرة العامة
🧩 الأقسام الرئيسية (عنوان + 2 إلى 4 نقاط لكل قسم)
📊 الأرقام والجداول المهمة
⚠️ ملاحظات
✅ أهم حاجة:
```

### Spreadsheets and CSV

```
ملخص ملف بيانات: <اسم الملف>
الحجم: <عدد الصفوف والأعمدة> | الأوراق: <أسماء>

📌 محتوى الملف
📊 المؤشرات الرئيسية (إجماليات، متوسطات)
📈 الاتجاهات
⚠️ قيم شاذة أو بيانات ناقصة
✅ أهم حاجة:
```

## Workflow

1. Identify the input type and read the content with the matching method.
2. Check that the extraction is complete (page count, message count, duration).
3. Summarize with the matching template and the core rules.
4. Re-check every number, name, and date against the source.
5. Add the `✅ أهم حاجة:` line.

## Privacy

Chats and documents may contain personal information. Use them only for the requested summary, never store them, and never publish them in a public repository.
