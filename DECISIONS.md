# DECISIONS — Bayan
> انسخ القالب إلى `DECISIONS.md`. أضف قرارًا جديدًا لكل تغيير يؤثر في البيانات أو الجودة أو الخدمة.  

## Decision D-001 — اعتماد TF-IDF كخط أساس لتصنيف النصوص
- **Date:** 2026-11-03
- **Gate:** B — Text classification
- **Status:** accepted
- **Owner:** Reema  Alzurayqi

### Context | السياق

أجرينا تجربة تصنيف نصوص ببيانات اصطناعية صغيرة. استخدمنا تقسيم التدريب والتحقق نفسه عند المقارنة، وكانت مجموعة التحقق تحتوي على 8 أمثلة فقط. درّبنا Transformer بنمط full_finetune لحقبتين مع ثلاث بذور: 42 و43 و44. نحتاج تحديد خط الأساس الذي سنرجع إليه في التجارب التالية، دون اعتبار هذه النتائج تقديرًا لجودة النموذج على بيانات حقيقية.

### Options considered | البدائل

| Option | Benefit | Cost/risk | Evidence |
|---|---|---|---|
| A: TF-IDF baseline | بسيط، وحقق نتيجة تحقق أعلى في هذه التجربة | لا نعرف بعد أداءه على بيانات حقيقية وأوسع | Validation Macro-F1 = 0.6667 |
| B: Transformer full fine-tuning | يسمح بتجربة نموذج متعدد اللغات وتقييم أثر البذرة | أعلى كلفة تدريبية، ونتيجته أقل من خط الأساس هنا | ثلاث بذور؛ متوسط Validation Macro-F1 = 0.5333 |

### Decision | القرار

نعتمد TF-IDF خطًا مرجعيًا لتجارب تصنيف النصوص القادمة، ولا نعتمد Transformer الحالي بدلًا منه بناءً على نتائج هذه التجربة. القرار يخص المقارنة التجريبية فقط؛ اختيار نموذج نهائي للخدمة مؤجل حتى التقييم على بيانات مناسبة.

### Evidence | الدليل

- Report/test/commit: `reports/day2_classification_distinction_metrics.json` و`text_classification_EXPLORE.ipynb`.
- Metric and result label: النتائج موسومة `MEASURED_SMOKE`. حقق Transformer في التحقق Macro-F1 بقيم 0.5500 و0.5167 و0.5333 للبذور 42 و43 و44؛ المتوسط 0.5333، والمدى 0.5167–0.5500. حقق TF-IDF baseline قيمة 0.6667 على التحقق.
- Slice or failure considered: مجموعة التحقق صغيرة جدًا (8 أمثلة) والبيانات اصطناعية. لم تُستخدم مجموعة الاختبار لاختيار البذرة.

### Consequences and rollback | الأثر والرجوع

- Positive consequence: أصبح لدينا خط أساس واضح ونتائج ثلاث بذور موثقة للمقارنة اللاحقة.
- Limitation/new risk: فرق النتائج في 8 أمثلة لا يكفي للجزم بأن TF-IDF أفضل عمومًا أو أن Transformer غير مناسب للمشروع.
- Rollback trigger: ظهور تقييم موثوق على بيانات مناسبة يغيّر المقارنة أو يكشف مشكلة في التقسيم أو حساب المقياس.
- Rollback path: نراجع تقرير النتائج والتقسيم، ونسجل قرارًا جديدًا يحدّث اختيار النموذج مع الإبقاء على هذا القرار كسجل لما توصّلنا إليه وقت التجربة.

---

## قرارات إلزامية قبل Gate E

- [ ] tokenizer + max length.
- [ ] Arabic preprocessing profile.
- [ ] task model/baseline and split.
- [ ] semantic encoder/index/k/threshold.
- [ ] metric/slices/error priorities.
- [ ] performance budget.
- [ ] ONNX/INT8 adopt or reject.
- [ ] served artefact + preprocessing/label versions.
