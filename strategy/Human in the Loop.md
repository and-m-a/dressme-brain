---
created: 2026-08-29
updated: 2026-08-29
status: active
tags: [strategy, content-factory, human-in-the-loop, evaluation, editorial-window]
---

# Human in the Loop

## Purpose

Этот документ фиксирует, **что человеку пришлось делать вручную при создании первых Editorial Windows и контента**, чтобы дальше постепенно сокращать ручной труд и повышать процент качественных автоматических результатов.

Human in the Loop здесь — не временный костыль и не цель «в конце полностью убрать человека». В fashion/editorial-контенте часть решений субъективна и зависит от вкуса. Цель Content Factory другая:

> **Автоматизировать дешёвые, повторяемые и проверяемые решения; оставлять человеку высокоуровневый editorial judgement; постоянно повышать acceptance rate так, чтобы человеку приходилось смотреть всё меньше слабых вариантов.**

Ключевой KPI автоматизации — не `0 human clicks`, а **меньше ручного времени на один publishable asset при сохранении или росте качества**.

---

## Что пришлось делать вручную при создании первого Editorial Window

### 1. Выбор самого Editorial Window

Даже с помощью AI человек пока должен:

1. посмотреть catalogue-first audit текущего live/in-stock ассортимента;
2. сравнить предложенные AI editorial directions;
3. проверить, действительно ли направление поддерживается товарами и реальными фотографиями;
4. оценить, насколько направление интересно бренду именно сейчас;
5. выбрать active Editorial Window.

То есть AI может сделать broad audit, clustering, предложить 3–5 направлений и объяснить их, но **финальный выбор Window пока остаётся human editorial decision**.

Позже можно сильно сократить этот этап:

```text
catalogue audit
→ AI proposes supported directions
→ AI scores catalogue support / seasonality / novelty / brand fit
→ human chooses from 2–3 strong options
```

Не нужно стремиться к автоматическому выбору Window до тех пор, пока не накоплено несколько реальных Window и человеческих решений, на которых можно учиться.

---

### 2. Поиск и отбор visual references

Человеку пришлось вручную искать и курировать reference images.

Недостаточно, чтобы фотография просто была «fashion». Нужно глазами проверять:

- насколько кадр **живой**, а не стерильный AI/catalogue shot;
- есть ли у модели **харизма**;
- чувствуется ли **motion / движение**;
- интересны ли поза, жест, ракурс и композиция;
- есть ли creative/editorial quality;
- привлекателен ли кадр сам по себе;
- подходит ли location / environment;
- соответствует ли референс текущему Editorial Window и ZAMETNA visual language;
- можно ли безопасно использовать его как reference для наших товаров, не потеряв commerce readability.

Reference Pool должен постепенно уменьшать эту работу: хорошие references сохраняются, тегируются и переиспользуются, а слабые исключаются.

Но Reference Pool сам по себе не решает задачу. Нужен **evaluation layer для качества самого reference**, чтобы в пул автоматически не попадали формально подходящие, но скучные фотографии.

---

### 3. Ручной отбор outfits

AI Stylist может сгенерировать и отранжировать outfits, но человеку пока приходится выбирать, какие из них действительно подходят:

- под текущий Editorial Window;
- под конкретную model identity / типаж;
- под выбранную location/reference direction;
- по общей fashion-привлекательности;
- по тому, хочется ли реально публиковать этот образ.

Важно сохранять не только выбранный outfit, но и **rejected alternatives + reason**, например:

- weak_window_fit;
- weak_model_fit;
- boring_combination;
- colour_balance;
- too_basic;
- too_sexy / too_conservative;
- product_visual_conflict;
- strong_outfit_but_for_another_window.

Эти данные позже позволяют улучшать retrieval, ranking и VLM evaluation.

---

### 4. Выбор варианта генерации

Одна генерация не должна считаться финальным результатом только потому, что она технически успешна.

Для сильного кадра может понадобиться несколько вариантов:

```text
outfit + reference + model + window
        ↓
N generation variants
        ↓
automatic evaluation layers
        ↓
shortlist of strongest variants
        ↓
human selects / approves
```

Вместо того чтобы человек вручную инициировал бесконечные rerun, pipeline должен сам уметь:

- сгенерировать несколько разумно отличающихся вариантов;
- отбраковать очевидно слабые;
- автоматически сделать retry, если качество ниже threshold;
- показать человеку маленький shortlist, а не весь шум.

---

## Evaluation layers

Один общий `quality score` слишком грубый. Причины плохой генерации разные, поэтому evaluation лучше разделять на независимые слои.

### Layer 1 — Product fidelity / reference correctness

Проверяет, насколько правильно переданы реальные товары:

- silhouette;
- colour;
- fabric / texture;
- transparency;
- length;
- construction details;
- print;
- neckline / sleeves / closures;
- другие визуально значимые свойства.

Если товар искажён, фотография не должна проходить дальше только потому, что она красивая.

**Failure action:** reject / regenerate with stronger product constraints or references.

### Layer 2 — Editorial / creative quality

Отдельная модель/VLM должна оценивать не точность товара, а качество фотографии как fashion-content:

- charisma;
- liveliness;
- motion;
- pose quality;
- composition;
- camera angle;
- visual tension / energy;
- attractiveness;
- editorial feeling;
- отсутствие ощущения «generic AI model standing still»;
- насколько кадр хочется остановиться и рассмотреть.

**Failure action:** regenerate with changed pose / composition / camera / motion / reference while keeping the accepted outfit and product constraints.

### Layer 3 — Editorial Window / brand fit

Проверяет:

- соответствует ли кадр active Editorial Window;
- не выпадает ли из ZAMETNA visual language;
- соответствует ли нужному scenario / mood / season;
- не нарушает ли Brand Policy.

Сильный кадр, который не подходит текущему Window, не обязательно плохой: его можно сохранить в Bench/Content Pool для другого Window.

### Layer 4 — Technical / visual defects

Отдельно стоит ловить очевидные generation defects:

- anatomy problems;
- broken hands/fingers;
- duplicated objects;
- impossible garment geometry;
- strange logos/text;
- rendering artefacts;
- unrealistic intersections;
- inconsistent identity when identity anchor is required.

---

## Retry logic must depend on the reason for failure

Нельзя на любой reject просто запускать ту же генерацию ещё раз.

```text
product fidelity failed
→ reinforce product references / product prompt / generation method

creative quality failed
→ keep product + outfit, vary pose / camera / motion / composition / reference

window fit failed
→ change environment / styling context / reference direction

technical defect
→ regenerate same concept
```

Так evaluation превращается не только в фильтр, но и в **routing signal для следующей попытки**.

---

## Human approval remains a first-class stage

Полностью автоматизировать editorial judgement сейчас не нужно.

Человек особенно полезен там, где вопрос звучит не «есть ли ошибка?», а:

- этот кадр реально цепляет?
- есть ли в нём характер?
- хочется ли его публиковать?
- соответствует ли он тому, каким мы хотим видеть ZAMETNA?
- какой из нескольких хороших вариантов сильнее именно сейчас?

Задача автоматизации — сделать так, чтобы на human approval попадали **3 сильных варианта вместо 30 случайных**.

---

## Learning loop

Каждое human action желательно превращать в данные.

Сохранять:

- что человек approved / rejected;
- reason codes;
- выбранный вариант среди alternatives;
- Editorial Window;
- outfit/products;
- model identity;
- reference IDs;
- prompt/model/version;
- evaluation scores по каждому layer;
- retry count;
- был ли контент в итоге опубликован;
- позже — publication performance.

Это создаёт собственный dataset DressMe/ZAMETNA для улучшения prompts, thresholds, VLM judges, retrieval/ranking и потенциальных learned rankers.

---

## Что измерять

Основные operational metrics:

- **human acceptance rate** — какой % кандидатов человек принимает;
- **first-pass acceptance rate**;
- attempts / generations per accepted asset;
- retries by failure reason;
- human review time per accepted asset;
- number of candidates shown to human per accepted asset;
- outfit acceptance rate;
- reference acceptance rate;
- product-fidelity failure rate;
- creative-quality failure rate;
- Editorial Window fit failure rate;
- cost per accepted/published asset.

Главная цель каждого следующего слоя автоматизации — улучшать один из этих показателей.

---

## Practical automation priority

Автоматизировать в первую очередь то, где человек делает повторяемую фильтрацию:

1. catalogue-first audit и предложение supported editorial directions;
2. reference ingestion + tagging + deduplication;
3. reference quality / charisma / motion / creativity evaluation;
4. outfit shortlist + VLM ranking;
5. product-fidelity evaluation;
6. creative/editorial-quality evaluation;
7. targeted retry based on failure reason;
8. generation of several variants + automatic shortlist;
9. logging human decisions and rejection reasons;
10. позже — recommendation/ranking of the next content item for publication.

Оставлять человеку:

- выбор active Editorial Window из сильных supported directions;
- финальный taste-level approval сильных references;
- финальный выбор outfit, пока acceptance rate недостаточно высокий;
- финальный выбор publishable generation;
- publication/editorial judgement, пока не накоплена достаточная decision history.

---

## North Star

```text
Human does everything
        ↓
AI produces options, human filters heavily
        ↓
AI evaluation removes obvious failures
        ↓
AI retries intelligently and produces small strong shortlist
        ↓
human makes only high-value editorial decisions
```

**North Star:** не убрать человека из Content Factory, а сделать human attention редким и дорогим ресурсом, который тратится только там, где действительно нужен вкус и редакторское решение.
