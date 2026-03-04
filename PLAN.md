# Prompt Builder

Создай веб-приложение "Prompt Builder" — конструктор промптов для LLM. Один файл index.html (inline CSS + JS).

## Требования

### UI Layout
- Две колонки: слева поля ввода, справа live preview промпта (обновляется при каждом нажатии клавиши)
- Мобилка: одна колонка, переключение между редактором и превью кнопкой
- Тёмная тема по умолчанию, тогл светлой
- Glassmorphism стиль, современный минималистичный дизайн
- Весь UI на русском

### Поля ввода
1. **Роль** — textarea, placeholder: "Кто выполняет задачу? (например: опытный SMM-специалист)"
2. **Задача** — textarea (главное поле, крупнее), placeholder: "Что нужно сделать?"
3. **Контекст** — textarea, placeholder: "Вводные данные, ситуация, бэкграунд"
4. **Аудитория** — textarea, placeholder: "Для кого результат?"
5. **Формат** — textarea, placeholder: "Как оформить? (длина, структура, стиль)"
6. **Ограничения** — textarea, placeholder: "Чего избегать, лимиты"

### Дополнительные фичи
- **Few-shot примеры**: кнопка "➕ Добавить пример" — появляются пары полей "Вход" / "Выход", можно добавить до 3 штук, каждую можно удалить
- **Chain of Thought**: тогл-переключатель "Пошаговое мышление" — добавляет в промпт инструкцию думать пошагово
- **Пресеты**: кнопка "Загрузить пресет" — выпадающий список с готовыми заполненными примерами

### 6 шаблонов (табы сверху)
1. 📝 Текст — поля адаптированы под копирайтинг
2. 💻 Код — под программирование
3. 📊 Анализ — под аналитику
4. 🎨 Изображение — под генерацию картинок (промпт для DALL-E/Midjourney)
5. 🧠 Брейншторм — под генерацию идей
6. 📋 Универсальный — дефолтный

Каждый шаблон меняет placeholders полей и имеет свой пресет.

### Пресеты (по одному на шаблон)
- Текст: пост в Telegram о запуске продукта
- Код: рефакторинг функции авторизации
- Анализ: сравнение трёх CRM-систем
- Изображение: киберпанк-город на закате
- Брейншторм: идеи для тимбилдинга
- Универсальный: написать инструкцию по онбордингу

### Генерация промпта (live preview)
Промпт собирается автоматически из заполненных полей. Формат:

Ты — {роль}.

{задача}

Контекст: {контекст}
Аудитория: {аудитория}
Формат: {формат}
Ограничения: {ограничения}

Если CoT включён, добавить: "Сначала проанализируй задачу шаг за шагом, затем дай финальный результат."

Если есть примеры, добавить блок "Примеры:" с парами Вход/Выход.

Пустые поля пропускаются (не показываются в промпте).

### Кнопки
- **Скопировать** — копирует промпт в буфер, меняет текст на "✓ Скопировано" на 2 сек
- **Сбросить** — очищает все поля
- Ссылки-кнопки: ChatGPT, Claude, Gemini, DeepSeek — открывают соответствующий чат в новой вкладке

### Дизайн
- Фон: #0f0f23 (тёмная) / #f5f5f5 (светлая)
- Карточки: backdrop-filter blur, полупрозрачные
- Accent: #6366f1 (indigo)
- Шрифт: system-ui
- Border-radius: 12px
- Transitions: 0.2s ease

---

## Implementation Tasks

### Task 1: Fix field types, colors, placeholders, and few-shot limit
- [x] Change Role field from input to textarea with correct placeholder from spec
- [x] Change Audience field from input to textarea with correct placeholder from spec
- [x] Update all placeholder texts to match spec exactly
- [x] Fix background color to #0f0f23 (dark) and accent to #6366f1
- [x] Limit few-shot examples to max 3 (hide add button when 3 reached)

### Task 2: Add light/dark theme toggle
- [x] Add CSS variables for light theme (#f5f5f5 background, adjusted surfaces/text)
- [x] Add theme toggle button in header
- [x] Implement theme switching JS logic with CSS class toggle

### Task 3: Rework presets and template system
- [x] Make tabs only change placeholders (not fill fields)
- [x] Add "Загрузить пресет" button with dropdown menu
- [x] Create specific preset content matching spec descriptions
- [x] Reset button clears fields but keeps current template placeholders

### Task 4: Fix prompt generation format and copy button
- [x] Change prompt format to flat style matching spec (no markdown headers)
- [x] Fix CoT text to match spec exactly
- [x] Change copy button to show "✓ Скопировано" text for 2 sec instead of toast
- [x] Remove MD copy button (not in spec)

### Task 5: Polish and final validation
- [x] Ensure mobile responsiveness works correctly with all new features
- [x] Verify all 6 templates have correct placeholders and presets
- [x] Test theme toggle persistence and visual correctness
- [x] Final review of all spec requirements
