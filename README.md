Eco-Sovereign — النواة (v2)
التشغيل
cd seed && python generate_mock.py && cd ..
cp backend/.env.example backend/.env   # املأ المفاتيح (التعليمات داخل الملف)
docker compose up --build
# الوثائق التفاعلية: http://localhost:8000/docs
الواجهة: Next.js 14+ مع Tailwind 3.3+ و react-leaflet و leaflet.
ضع frontend/public/sw.js في public/ وسجّله مرة واحدة: navigator.serviceWorker.register('/sw.js').
اختبار سريع
curl -X POST localhost:8000/api/v1/telemetry/evaluate-fire-risk -H 'Content-Type: application/json' \
  -d '{"station_code":"T1","temperature":42,"humidity":12,"wind_speed":35,"prev_ffmc":92,"prev_dmc":90,"prev_dc":400,"month":7}'
curl -X POST localhost:8000/api/v1/telemetry/ingest -H "X-API-Key: $STATION_API_KEY" -H 'Content-Type: application/json' \
  -d '{"station_code":"DZ-43-W01","temperature":41,"humidity":14,"wind_speed":30}'
ما تغيّر مقارنة بالنسخة الأولى
معادلة واحدة في risk_engine.py وهي نظام FWI الكندي الكامل (مُتحقَّق منه بقيم Van Wagner & Pickett المرجعية).
التشفير: Fernet للتفاصيل داخل القاعدة + TLS عند الـ proxy؛ حُذفت عبارة "100%".
التحقق من الموقع بـ ST_Covers على حدود الدولة + علامات تلاعب تُراجَع بشرياً.
تحديد المعدل (Redis)، ودعم دون اتصال (IndexedDB + Background Sync)، ولغات ar/fr/en.
قبل الإنتاج
استبدل المستطيلات التجريبية بحدود حقيقية (انظر seed/generate_mock.py).
عايِر عتبات FWI_LEVELS وعتبات الفيضان مع الديوان الوطني للأرصاد والمديرية العامة للغابات.
صور البلاغات: يُحفظ الآن الـ hash فقط؛ أضف تخزيناً كائنياً (S3/MinIO) برفع موقّع مسبقاً.
أضف مصادقة لمراجعي البلاغات (لوحة التحقق) ودور للقراءة فقط للجمهور.
