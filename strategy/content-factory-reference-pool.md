---
created: 2026-08-29
updated: 2026-08-29
status: concept
 tags: [strategy, content-factory, reference-pool, creative-direction, image-generation, zametna]
---

# Content Factory Reference Pool / Creative Memory

## Зачем

Content Factory не должен сводиться к буквальному копированию заранее выбранного pose/location reference для каждого кадра. Цель — сохранить точность товара и identity, но дать AI Creative Director контролируемую свободу придумывать fashion-editorial кадры: позы, body language, эмоции, ракурсы, композицию, локацию и micro-story.

Reference Pool нужен не как обязательная библиотека картинок, которые каждый раз напрямую передаются image model, а прежде всего как **creative memory / библиотека fashion cinematography primitives**.

## Три уровня контроля

### 1. Fixed / no creative freedom

То, что генератор не должен переизобретать:

- конкретные товары и их конструкция;
- цвет, ткань, фактура, прозрачность, отделка, fit и важные детали;
- identity выбранной модели;
- обязательные Brand Policy constraints.

Здесь используются product references, identity anchors и последующая fidelity validation.

### 2. Directed / Editorial Window context

Content Director / active Editorial Window задаёт контекст, но не режиссирует положение каждой руки:

- story / life scenario;
- current editorial mood;
- visual preset / photographic language;
- season / occasion;
- допустимый уровень sensuality / boldness;
- общий environment archetype;
- ограничения бренда.

Пример: `late-August Moscow, quiet expensive femininity, between work and an evening appointment, architectural city environment, editorial rather than e-commerce`.

### 3. Creative / model freedom

Внутри этих границ AI Creative Director и image model могут сами выбирать:

- pose и asymmetry;
- body language;
- micro-expression / gaze;
- camera angle;
- framing / negative space;
- movement;
- конкретное взаимодействие с environment;
- точный shot concept;
- последовательность кадров внутри carousel.

Цель — избегать generic e-commerce posing, centred standing poses и одинаковой influencer-фотографии. Модель должна ощущаться персонажем внутри сцены, а не манекеном, демонстрирующим одежду.

## Reference Pool

Пул может собираться вручную Content Director'ом и/или через controlled scraping/ingestion разрешённых источников. В него попадают только кадры, которые человек считает действительно сильными и полезными как creative inspiration.

Потенциально пул может быть большим: сотни или тысячи approved fashion/editorial references.

Ключевой принцип: **не обязательно передавать исходное изображение GPT-Image/другой image model при каждой генерации**.

Сначала VLM превращает reference в structured Creative DNA.

Пример полей:

```text
pose
body_language
facial_expression
gaze
movement
camera_angle
camera_distance
lens_feel
framing
composition
negative_space
location_archetype
interaction_with_environment
lighting
weather / atmosphere
visual_tension
editorial_mood
story_beat
why_this_frame_is_interesting
```

Важно описывать не только `что на картинке`, а **почему кадр работает**.

Плохое описание:

> woman standing near a wall

Полезное Creative DNA:

> asymmetrical leaning pose; shoulder against stone wall; torso turned slightly away; chin lowered; gaze past camera; crossed-leg tension; medium-low camera; strong negative space; restrained self-confidence.

Таким образом Reference Pool становится библиотекой reusable creative primitives, а не Pinterest-board, который Content Factory механически копирует.

## Retrieval / creative RAG

Active Editorial Window + outfit + current story могут формировать creative query, например:

```text
urban solitude + restrained sensuality + movement
```

Retriever возвращает несколько релевантных Creative DNA / primitives:

- варианты body language;
- movement patterns;
- camera compositions;
- location archetypes;
- expression patterns;
- lighting / atmosphere ideas.

LLM Creative Director комбинирует их и создаёт **новый shot concept**, а не обязан воспроизводить один исходный reference 1:1.

Пример результата:

> Narrow stone passage after rain. Model moves diagonally across frame rather than toward camera. She looks over her shoulder as if someone called her. Slightly low camera, long-lens compression, foreground obstruction, imperfect off-centre framing.

## Reference Pool не должен убивать креативность

Предпочтительный режим:

1. Creative Director сначала пробует спроектировать scene / shots из Editorial Window, outfit и Brand/Visual context самостоятельно.
2. Reference retrieval используется как inspiration, diversity mechanism или помощь при слабом/банальном concept.
3. Hard image reference применяется только когда мы сознательно хотим конкретный pose, composition, location grammar или другой сильный visual trick.

Рабочая продуктовая гипотеза, которую нужно тестировать, а не считать фиксированной математикой:

```text
majority: free creative direction
minority: retrieved Creative DNA inspiration
rare: hard pose/location/composition reference
```

Не нужно превращать `70/20/10` или любую другую пропорцию в hard-coded quota до тестов.

## Carousel / micro-story

Carousel лучше проектировать как одну маленькую editorial scene, а не как пять независимых генераций.

Пример story seed:

> She leaves the gallery and has twenty minutes before dinner.

LLM Creative Director сначала создаёт storyboard, например:

1. Establishing — пространство / движение / wide frame;
2. Character — medium frame, expression / gaze;
3. Fashion detail — ткань, рука, движение, но не банальный packshot;
4. Hero — самый сильный editorial fashion frame;
5. Exit / imperfect moment — вход в дверь, посадка в машину, поворот, уход из кадра.

Все кадры принадлежат одной локации или одной логичной micro-story, но позы, framing и camera distance меняются.

Только после storyboard каждый shot отправляется в image generation.

## Proposed Content Factory layer

```text
ACTIVE EDITORIAL WINDOW
+ OUTFIT / PRODUCTS
+ BRAND POLICY
+ VISUAL PRESET
        ↓
LLM CREATIVE DIRECTOR
        ↓
scene / micro-story / storyboard
        ↓
optional Creative Reference Pool retrieval
        ↓
shot concepts
        ↓
IMAGE GENERATION
(product refs + identity anchors + shot brief)
        ↓
VLM EVALUATION
        ↓
Approved Content Pool
```

Creative Director должен разделять `must preserve` и `may invent`.

## Evaluation

Generated content нельзя оценивать только по product fidelity. Нужны отдельные dimensions:

```text
product_fidelity
identity_consistency
editorial_quality
pose_quality
body_language
composition
charisma / character_presence
location_quality
visual_non_genericness
story_coherence (for carousel)
brand_fit
window_fit
```

Если товар передан точно, но кадр выглядит как generic catalogue/influencer image, он может быть технически корректным, но editorial-failed.

Если creative concept интересный, но товар искажен — также reject/regenerate.

## MVP / experimentation

Не строить огромный scraper/RAG/storage до проверки основной гипотезы.

Первый тест можно сделать вручную:

1. собрать 30–100 действительно сильных references;
2. руками approve их Content Director'ом;
3. прогнать VLM extraction в Creative DNA;
4. сравнить три режима на одинаковых outfits / Window:
   - free creative brief only;
   - creative brief + retrieved text Creative DNA;
   - hard image reference;
5. сравнить human preference, charisma/editorial score, diversity и product fidelity;
6. только после доказанного преимущества масштабировать ingestion, embeddings/retrieval и automatic routing.

## Strategic principle

**Catalogue decides what we show. Editorial Window decides what story/world is active. Creative Director decides how to shoot it. Reference Pool expands the Creative Director's visual vocabulary without forcing Content Factory to copy a reference for every frame.**
