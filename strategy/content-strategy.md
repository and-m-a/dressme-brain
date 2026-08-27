---
created: 2026-08-26
updated: 2026-08-27
status: active
tags: [strategy, content, instagram, editorial-window, content-factory, zametna]
---

# ZAMETNA Content Strategy

Связано: [Brand DNA](brand-dna-draft.md), [архетипы](archetypes.md), [storytelling](storytelling.md), [ИИ-стилист](ии-стилист.md), [ИИ-контент-завод](ии-контент-завод.md).

## Дано

ZAMETNA — premium fashion marketplace женской одежды российских дизайнеров.

Текущие вводные:

- около **600 SKU** разных брендов, стилей и occasions;
- несколько пересекающихся fashion-сценариев / персон: **City Professional, Premium Everyday, Social / Occasion, Fashion Connoisseur**;
- premium positioning;
- бесплатная доставка и **оплата после примерки** как важные коммерческие преимущества;
- AI Stylist, который собирает outfits из реального каталога;
- у товаров есть **Visual Passports**: type/slot, colour, material, fit, season, formality, style, visual weight, on-model media и другие признаки;
- Visual Passport используется для retrieval/scoring; реальные product photos — финальный visual source of truth при конфликте;
- Content Factory умеет превращать outfit в AI fashion image / carousel / Reel / публикацию;
- marginal cost AI-контента позволяет теоретически делать 1–2+ качественных публикации в день;
- задача стилиста — не перебрать все комбинации, а стабильно находить примерно **1–2 сильных publishable outfit в день**;
- органический Instagram рассматривается как гипотеза acquisition-канала, которую ещё нужно доказать бизнесом.

## Главная проблема

Если каждый день выбирать просто лучший доступный outfit, лента быстро становится набором хороших, но несвязанных миров:

```text
Quiet Luxury → Sexy → Business → Romantic → Casual → Fashion Forward
```

Каждый пост отдельно может быть сильным, но профиль начинает ощущаться как несколько разных брендов.

Обратный экстремум тоже плох:

```text
2–3 недели Quiet Luxury → 2–3 недели Occasion → 2–3 недели Fashion Forward
```

Тогда человек из другой части аудитории может зайти в неподходящий момент и не увидеть себя вообще.

**Исходный вопрос:** как гармонично сочетать 3–4 разных fashion-сценария в одном Instagram так, чтобы человек увидел «это про меня», но соседние посты всё равно ощущались одной ZAMETNA-вселенной?

## Итоговый ответ

Не разделять аудиторию по длинным блокам и не смешивать контент случайно.

```text
ONE BRAND UNIVERSE
        ↓
Brand Narrative + Brand Policy + Visual Language
        ↓
Editorial Window = temporary weighted context
        ↓
Content Pool of strong available candidates
        ↓
Dynamic / initially manual publication selection
        ↓
Instagram + attribution + analytics
```

Ключевой вывод после нескольких раундов критики:

> **Editorial Window остаётся, но это НЕ сценарий из 9 последовательных постов. Это временная функция приоритетов для Content Factory.**

Каждая публикация должна работать самостоятельно, потому что Instagram в основном потребляется через Feed / Reels / recommendations, а не как линейный журнал.

## 1. Brand Narrative — semantic identity

Narrative описывает характер, но не притворяется machine-enforced policy.

Рабочее направление:

- primary archetype: **Lover**;
- supporting archetype: **Ruler**;
- modern feminine premium;
- feminine, desirable, polished, confident;
- sensuality — controlled, not vulgar.

Narrative используется человеком, LLM/VLM и prompt generation. Подробности — в [Brand DNA](brand-dna-draft.md) и [архетипах](archetypes.md).

## 2. Brand Policy — глобальные машинные границы

Policy должна реально отклонять неподходящие Window / Content.

Примеры правил:

```json
{
  "sensuality": { "max": 3 },
  "fashion_boldness": { "max": 4 },
  "feed_rules": {
    "packshot_as_cover": false
  },
  "outfit_color_rules": {
    "max_dominant_colors": 2,
    "prefer_neutral_base": true
  },
  "allowed_visual_presets": [
    "zametna_editorial_v1"
  ]
}
```

Window может быть строже глобального policy, но не шире него.

## 3. Visual Language / Preset

Главный визуальный клей аккаунта — не persona quota, а повторяемый photographic language:

- lighting;
- colour / contrast processing;
- camera distance and framing;
- posing;
- environment quality;
- editorial realism;
- commerce readability of the garment.

Но preset нельзя качественно придумать только текстом. Первый `zametna_editorial_v1` должен родиться глазами:

```text
existing strong generations + 10–15 test frames
        ↓
15–20 candidates side by side
        ↓
choose the coherent 6–9 reference assets
        ↓
formalize lighting / framing / processing / environment rules
        ↓
zametna_editorial_v1
```

Позже возможны контролируемые seasonal micro-variations, чтобы избежать sterile preset fatigue, но не разные визуальные миры каждый день.

## 4. Editorial Window

**Editorial Window = временная тема + fashion envelope + weights + operational product policy.**

Это first-class entity / snapshot context для генераций и публикаций, но не жёсткое расписание.

Window задаёт:

- current editorial theme;
- season / occasion emphasis;
- style direction;
- диапазоны formality / sensuality / fashion boldness;
- color direction;
- audience weights;
- occasion weights;
- visual preset;
- product policy, например `require_stock`.

### Первый Window: Back to Moscow / September

```json
{
  "name": "Back to Moscow / September",
  "fashion_direction": {
    "season": "early_autumn",
    "primary_style": "quiet_luxury",
    "style_accents": ["feminine_tailoring"],
    "formality": { "min": 2, "max": 4 },
    "sensuality": { "min": 1, "max": 3 },
    "fashion_boldness": { "min": 1, "max": 3 }
  },
  "audience_weights": {
    "city_professional": 0.45,
    "premium_everyday": 0.25,
    "social_occasion": 0.20,
    "fashion_connoisseur": 0.10
  },
  "occasion_weights": {
    "work": 0.30,
    "meeting": 0.20,
    "city_everyday": 0.20,
    "dinner": 0.20,
    "event": 0.10
  },
  "color_direction": {
    "base": ["black", "cream", "chocolate", "warm_beige"],
    "accents": ["burgundy"]
  },
  "product_policy": {
    "require_stock": true,
    "require_visual_passport": true
  },
  "visual_preset_id": "zametna_editorial_v1"
}
```

**Weights are priorities, not quotas.** Не надо генерировать слабый Fashion Connoisseur пост только потому, что JSON «должен» дать ему 10%.

## 5. Как сочетать несколько ЦА

Рабочая гипотеза: наши «ЦА» могут быть не четырьмя независимыми женщинами, а **четырьмя сценариями жизни одной широкой premium female audience**.

Одна и та же женщина может быть:

- City Professional утром;
- Premium Everyday в выходной;
- Social / Occasion вечером;
- Fashion Connoisseur иногда.

Поэтому Window меняет **центр тяжести**, но не запрещает соседние сценарии.

Примеры:

- `Back to Moscow` → больше City Professional;
- `Autumn Evenings` → больше Social / Occasion;
- `Weekend in Moscow` → больше Premium Everyday;
- fashion event / designer focus → больше Fashion Connoisseur.

Это предположение нужно проверить по данным: посмотреть пересечение между товарными/style clusters не только по заказам, но и по product views, favourites, cart additions и orders. Если кластеры почти не пересекаются, возможно, под одной вывеской реально живут две разные аудитории и стратегию надо пересмотреть.

## 6. AI Stylist + Visual Passports

Генерация должна быть hybrid и bottom-up от реального каталога:

```text
CURRENT STOCK
+
VISUAL PASSPORTS
+
EDITORIAL WINDOW
        ↓
cheap retrieval / scoring
        ↓
AI Stylist shortlist
        ↓
VLM checks real product photos
        ↓
strong approved outfits
```

Visual Passport — structured retrieval signal. Actual images — visual truth.

Шкалы вроде `sensuality 2 vs 3` нельзя считать объективным измерением. Их полезнее использовать как **soft ordinal signals**: важно, чтобы система обычно понимала relative order `more restrained → more sensual`, а не притворялась, что разница между 2 и 3 физически точна.

Подробнее — [ИИ-стилист](ии-стилист.md).

## 7. Content Pool

Content Factory создаёт не только «следующий пост прямо сейчас», а небольшой буфер сильных approved candidates.

У каждого candidate сохраняем metadata:

- product IDs / brands;
- persona / scenario;
- occasion;
- style / season;
- sensuality / formality;
- model / environment;
- format / hook;
- content quality;
- Editorial Window fit;
- stock snapshot;
- generation / evaluation versions.

На старте **не нужен пул 40–100**. Это создаёт cold-start bottleneck. Практичный initial buffer: **10–20 реально publishable assets**, после чего pipeline должен производить немного быстрее, чем Instagram их расходует.

## 8. Publication Router — позже; сначала manual + logs

Целевая идея router:

```text
publication score =
quality
+ editorial fit
+ stock/commercial relevance
+ seasonality
+ freshness/diversity
- recent product repetition
- recent outfit repetition
- recent visual/persona repetition
```

Но на старте 8–10 коэффициентов будут выдуманы из головы и создадут иллюзию точности.

**MVP:** первые ~30 публикаций выбираем руками из approved pool, но логируем причины выбора и альтернативы.

Если нужна минимальная автоматизация, максимум:

```text
quality + editorial_window_fit + stock - same_product_last_7_days
```

После накопления реальных логов и performance можно строить более умный router.

## 9. Repetition, reuse и 600 SKU

SKU не «сгорает» после одной публикации.

Один сильный товар можно рестайлить:

```text
black trousers + white shirt
black trousers + corset
black trousers + knitwear
black trousers + blazer
```

Один asset/outfit может стать разными publications: editorial image, carousel, Reel, detail, `office → dinner`, `1 item / 3 ways`, ad creative.

Реальный риск — **repetition fatigue**, а не арифметическое исчерпание 600 SKU.

Нужно хранить и позже учитывать:

- `product_last_published_at`;
- publication count per product / outfit pair / brand;
- model / environment exposure;
- recent pair repetition.

В перспективе у стилиста должны существовать два режима:

- `discover_new_outfit`;
- `restyle_product`.

## 10. Content formats — независимые свойства

Не фиксировать ложную дихотомию `desire` vs `acquisition`.

Один пост может одновременно быть:

- beautiful / desirable;
- shareable / saveable;
- commercial;
- discovery-oriented.

Пример: «3 образа: офис → ужин» может быть premium editorial и одновременно полезным acquisition asset.

## 11. Profile layer: Bio / Highlights / Pinned

Feed не обязан один закрывать весь ассортимент и все сценарии.

Человек из recommendations часто сначала оценивает профиль за секунды. Поэтому permanent profile layer должен постоянно объяснять оффер и давать быстрый self-identification независимо от текущего Window.

Рабочее направление:

- Bio: российские дизайнеры / примерка до оплаты / бесплатная доставка;
- Highlights: **WORK / EVERYDAY / EVENING / HOW TO BUY** (названия для клиента, не внутренние persona labels);
- pinned posts могут объяснять ZAMETNA, оффер и лучшие сценарии.

Это дешёвый способ держать постоянное coverage нескольких use-cases, не превращая feed в квотную кашу.

## 12. Attribution с первого дня

Нельзя через 100 публикаций знать reach и не знать, что принесло заказы.

Нужна цепочка:

```text
Instagram Publication
↔ internal Content / Publication ID
↔ Outfit
↔ Products
↔ Editorial Window
↔ tracked site visit
↔ cart / order
```

Для переходов использовать tracked URLs / UTM там, где формат даёт ссылку, с `utm_source=instagram`, organic medium, window/campaign и конкретным `publication_id` / asset context.

## 13. Analytics и learning

С первого поста сохраняем content metadata и Instagram/commercial metrics:

- reach / non-follower reach;
- saves / shares;
- profile visits / follows;
- site / product visits;
- cart additions;
- orders / kept purchases, если атрибуция доступна.

**Не делать псевдонаучные выводы по одному experimental post.** Instagram слишком шумный и confounded.

Первое окно — baseline collection. После примерно **30–50 публикаций** ищем operational failure modes; после **50–100+** можно искать устойчивые directional patterns по persona/style/occasion/model/format, всё ещё без притворства строгим A/B test.

## 14. Stock — runtime concern

Window может требовать `require_stock: true`, но stock lifecycle не должен ломать Window.

Перед публикацией:

```text
candidate → current stock check
in stock → publish
out of stock → replace / regenerate / remove candidate
```

## 15. Legal / brand-operational risk

До масштабирования AI-generated контента нужно проверить текущие договоры и права на brand/product media и производные AI creatives. Если договоры это не покрывают явно, лучше закрепить правила использования заранее и по возможности как часть предлагаемой брендам услуги, а не узнавать о конфликте постфактум.

Это отдельный legal/partner risk, не задача Editorial Window.

## 16. Ключевые риски и что с ними делаем

### Grid fallacy / chronological drama
**Риск:** строить `core → adjacent → experiment → transition` как будто пользователь читает Instagram подряд.

**Решение:** slots убраны из core architecture; каждый post должен работать independently.

### Audience coverage превращается в кашу
**Риск:** обязательные квоты заставят публиковать слабое или натягивать persona на тему.

**Решение:** audience **weights**, не quotas; визуальная связность держится Brand Policy + Visual Preset + Window context.

### Instagram «не поймёт» несколько ЦА
**Риск:** слишком разные смысловые clusters могут размыть audience signal.

**Решение:** считаем их adjacent scenarios как гипотезу и проверяем фактическое пересечение поведения пользователей.

### 600 SKU / catalogue fatigue
**Риск:** сильные товары будут повторяться.

**Решение:** reuse + restyling + repetition memory; не считать SKU одноразовым asset.

### VLM semantic precision illusion
**Риск:** sensuality/formality scores выглядят объективнее, чем есть.

**Решение:** использовать как soft ordinal signals и человечески/VLM-калиброванные criteria, не физическую истину.

### Router overfitting before data
**Риск:** много весов без baseline создают непредсказуемый selection.

**Решение:** первые ~30 publications manual; либо очень простой score.

### Content Pool cold start
**Риск:** пытаться накопить 40–100 approved assets до запуска.

**Решение:** начать с 10–20 strong assets и держать rolling buffer.

### Visual preset fatigue
**Риск:** один язык через 60–90 дней станет стерильным.

**Решение:** стабильное ядро + контролируемые seasonal micro-variations после данных.

### Empty visual presets
**Риск:** `zametna_editorial_v1` становится красивым ID без реального содержания.

**Решение:** сначала reference images, потом правила.

### Learning from noise
**Риск:** объявить «sensuality +1 дала +28% reach» по одному посту.

**Решение:** сохранять evidence, не принимать решения на единичном observation; pattern search только после достаточной истории.

### Feed-only thinking
**Риск:** забыть Bio / Highlights / pinned и заставлять feed показывать всё всем.

**Решение:** permanent profile layer закрывает оффер и основные scenarios постоянно.

### Missing attribution
**Риск:** знать engagement, но не знать commercial impact.

**Решение:** publication-level attribution с первого дня.

## 17. MVP launch order

1. На основе уже сгенерированных образов + 10–15 тестовых кадров собрать 15–20 visual candidates.
2. Глазами выбрать coherent reference set и зафиксировать `zametna_editorial_v1`.
3. Создать первый Window **Back to Moscow / September** как weighted context, не расписание.
4. Собрать initial approved pool **10–20 publishable assets**.
5. Первые ~30 публикаций выбирать вручную; логировать metadata, причины выбора, alternatives и results.
6. Параллельно оформить Bio / Highlights / pinned, attribution и stock pre-publish check.
7. На 30–50 публикациях разобрать реальные operational bottlenecks: acceptance rate, pool depletion, repetition, stock failures, visual consistency.
8. На 50–100+ публикациях искать content patterns и только тогда усложнять publication router.
9. Следующий Editorial Window на MVP выбирается человеком. Automatic planner / rotation — позже.

## 18. Что эта архитектура НЕ доказывает

Она отвечает на вопрос:

> **как системно выпускать coherent premium content из разнородного marketplace-каталога.**

Она не отвечает сама по себе на главный business question:

> **может ли organic Instagram привести платящую аудиторию premium fashion marketplace.**

Это отдельная гипотеза поверх нескольких Windows:

```text
Instagram recommendation reach
→ profile
→ site
→ product / cart
→ order
→ kept purchase
```

Успех Content Factory нельзя подменять успехом acquisition-канала. Обе вещи нужно измерять отдельно.
