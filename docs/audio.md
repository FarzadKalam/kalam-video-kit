# صدا، رونویسی و SFX

این کیت صدای فارسی تولید نمی‌کند. نریشن از کاربر می‌آید؛ برای گفتار موجود، صدای منبع مرجع است. ابزار ASR محلی با نصب اختیاری `scripts/setup-asr.ps1` آماده می‌شود. مدل Whisper در کش همان درایو ذخیره می‌شود و فایل مشتری به API فرستاده نمی‌شود. دانلود اولیهٔ مدل اینترنت و چندصد مگابایت فضا می‌خواهد؛ روی CPU ممکن است کند باشد.

```powershell
node scripts/kit.mjs media extract .local/projects/job/assets/voice.wav .local/projects/job/analysis/speech.wav
.local/asr-venv/Scripts/python.exe scripts/transcribe.py .local/projects/job/analysis/speech.wav --output .local/projects/job/analysis/transcript.json
```

خروجی word timestamp تخمین ASR است؛ اسامی، سکوت انتهایی و همگامی با گفتار باید بازبینی شوند. Whisper جای forced alignment تضمین‌شده نیست. زمان را از طول متن تقسیم نکن. در برش‌ها source in/out و offset را به زمان خروجی تبدیل و ثبت کن.

SFX مشترک در `assets/sfx/` با منبع در `assets/provenance.json` ثبت شده‌اند. برای هر رویداد مهم، نوع و زمان SFX را در نقشهٔ بیت‌ها بنویس؛ پرشدن نوار و افزایش اعداد می‌تواند صدای پیوسته/پله‌ای متناسب بگیرد. موسیقی از فایل مجاز پروژه می‌آید، نه دانلود خودکار.

گفتار باید واضح بماند. loudness و peak با FFmpeg اندازه‌گیری شود، ducking و gain با شنیدن خروجی انتخاب شوند؛ بالا بودن ولوم هم‌معنی کیفیت نیست. در گزارش بنویس آیا واقعاً شنیده‌ای یا فقط اندازه‌گیری فنی انجام شده است.
