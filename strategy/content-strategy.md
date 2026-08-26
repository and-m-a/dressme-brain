---
created: 2026-08-26
updated: 2026-08-26
status: active
tags: [strategy, content, instagram, editorial-window, zametna]
---

# ZAMETNA Content Strategy

## Goal

Instagram ZAMETNA должен последовательно вести аудиторию:

**увидела → заинтересовалась → подписалась → захотела образ/товар → перешла на сайт → купила.**

Контент должен одновременно поддерживать визуальную привлекательность бренда, коммерческую ценность и разумную стоимость производства.

## Content Mix

Основные рубрики:

- **Образ дня** — AI-образ из товаров ZAMETNA. Главная задача: desire.
- **Product Focus** — существующие фотографии одного товара. Дешёвый коммерческий контент.
- **Подборки** — например, «5 платьев на ужин». Главная задача: reach, saves, discovery.
- **Как носить** — стилизация одного товара несколькими способами.

Не весь контент должен быть дорогим AI-контентом. Готовые фотографии товаров должны регулярно использоваться вместе с генерируемым контентом.

## Editorial Window

**Editorial Window — временная визуальная и смысловая глава Instagram.**

В течение примерно **6–12 публикаций** контент должен ощущаться частью одной истории, а не набором случайных хороших постов.

Window задаёт:

- основную ЦА / persona;
- mood;
- occasion;
- сезон;
- уровень formal / casual;
- уровень sensuality;
- палитру;
- стили и силуэты;
- visual language.

Пример:

### Back to Moscow / September

- Persona: City Professional
- Mood: polished, feminine, metropolitan
- Occasions: work, meetings, dinner
- Palette: black, cream, chocolate, burgundy
- Sensuality: moderate
- Style: premium, feminine, sophisticated

Красивый образ, который не соответствует текущей Editorial Window, **не плохой — он просто отправляется в Bench на потом**.

Главное правило:

> Мы выбираем не самый красивый пост вообще, а лучший следующий пост для текущей главы ZAMETNA.

### Editorial Window в контент-заводе

Editorial Window должна стать **first-class сущностью**, к которой можно привязывать Content и генерации, а не оставаться только текстом в prompt.

MVP-направление:

- создавать и редактировать window вручную;
- автоматическую генерацию window с нуля оставить low priority;
- по параметрам window и Visual Passport собирать подходящий product pool;
- при необходимости материализовать его через существующую Collection;
- запускать ИИ-стилиста внутри этого пула;
- сохранять snapshot ключевых параметров window для уже созданного контента, чтобы последующее редактирование window не меняло исторический смысл генерации.

Два способа интеграции со стилистом и рекомендуемый staged hybrid описаны в [ИИ-стилисте](ии-стилист.md#editorial-window-как-вход-в-ии-стилиста).

## Target Audiences / Personas

У marketplace может быть много ЦА. Не нужно ограничивать весь бизнес 2–3 сегментами.

При этом **одна Editorial Window должна работать преимущественно на одну основную persona и максимум одну-две secondary personas**.

Базовые personas ZAMETNA:

### City Professional
Современная городская женщина. Хочет выглядеть дорого, женственно и собранно.

### Fashion Connoisseur
Интересуется дизайном и стилем. Ищет необычные вещи, крой и бренды с характером.

### Social / Occasion
Рестораны, свидания, мероприятия, вечеринки. Нужны эффектные и более sensual образы.

### Young Affluent
Молодая обеспеченная аудитория. Хочет актуальную, современную, статусную fashion-эстетику.

### Premium Everyday
Более широкая ЦА. Не обязательно deeply into fashion, но хочет красивые, качественные и дорогие-looking вещи на каждый день.

Возраст вторичен. Для fashion важнее:

**lifestyle + occasion + aesthetic + fashion boldness + formality + sensuality + trend sensitivity.**

## Content Selection

Каждый кандидат проходит три уровня:

1. **Quality** — хорошо ли выглядит образ и достаточно ли точно переданы товары.
2. **Editorial Fit** — соответствует ли он текущей Editorial Window.
3. **Feed Fit** — хорошо ли он работает именно после последних публикаций.

Например, даже сильный total-black evening look можно отложить, если последние публикации уже были чёрными вечерними образами.

Статусы:

- **PUBLISH** — подходит сейчас.
- **BENCH** — хороший контент, но не для текущей window.
- **REGENERATE** — идея хорошая, реализация слабая.
- **REJECT** — контент не соответствует уровню ZAMETNA.

## Feedback Loop

Контент-завод должен быть closed loop:

**Stylist → Preview → Evaluation → Editorial Selection → Final Content → Instagram → Analytics → следующий выбор.**

Для каждого поста собираем минимум:

- reach;
- non-followers reach;
- likes;
- saves;
- sends;
- profile visits;
- follows;
- product clicks;
- add-to-cart;
- orders.

Со временем ZAMETNA должна принимать решения не только на основе вкуса команды, но и на основе собственной статистики: какие personas, стили, цвета, occasions, рубрики и типы образов действительно работают на нашу аудиторию.
