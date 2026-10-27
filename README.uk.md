[English](README.md) | [Русский](README.ru.md) | **Українська** | [Deutsch](README.de.md)

# WARDOGS: гайд з картопляної графіки 🥔

Ультранизька («картопляна») графіка для **WARDOGS**: налаштування Potato у грі, один рядок у `GameUserSettings.ini` та **LOD Bias** через **NVIDIA Profile Inspector**.

**Коротко:** налаштування Potato у грі → `sg.ShadowQuality=4` у GameUserSettings.ini (файл лише для читання) → NVIDIA Profile Inspector з LOD Bias **+3**. У результаті: жодних тіней, набагато менше листя і пласкі текстури з низькою деталізацією.

*Оновлено: 2026-10-27. Гра й далі оновлюється, тому налаштування можуть змінитися.*

![WARDOGS до і після картопляної графіки](images/before-after.png)

*На скриншоті «після» стоїть максимальний LOD Bias +15. Рекомендоване значення — +3 ([чому](#який-lod-bias-обрати)).*

> ⚠️ **Використовуйте на власний ризик.** Розробники поки ніяк не висловлювалися щодо NVIDIA Profile Inspector і в майбутньому можуть його заборонити. Якщо це станеться, поверніть усе як було (див. [Як усе скасувати](#як-усе-скасувати)).

---

## Що знадобиться

* **Відеокарта NVIDIA.** NVIDIA Profile Inspector працює лише з драйверами NVIDIA. Кроки 1–2 підходять для будь-якої відеокарти.
* **NVIDIA Profile Inspector** (NPI) з офіційного GitHub: https://github.com/Orbmu2k/nvidiaProfileInspector/releases
* Близько 10 хвилин

---

## Крок 1. Налаштування в грі

Відкрийте налаштування графіки в грі та виставте все як у таблиці. В **Overall Quality** з'явиться **Custom** — так і має бути.

*Назви налаштувань наведено як в англійському інтерфейсі гри.*

| Налаштування | Значення |
|:--|:--|
| **RESOLUTION QUALITY** | |
| Anti-Aliasing Method | NVIDIA DLSS |
| NVIDIA DLSS | DLAA |
| DLSS-G (DLSS Frame Generation) | Off |
| **GEOMETRY** | |
| Mesh Detail | Potato |
| Nanite Material Visibility Culling | Enabled |
| **ENVIRONMENT** | |
| View Distance | High |
| Shading | Potato |
| **LIGHTING** | |
| Global Illumination | Disabled |
| Shadows | Low *(у кроці 2 тіні вимикаються повністю)* |
| Reflections | Potato |
| **EFFECTS** | |
| Effects | Low |
| Particle Spawn Rate | Potato |
| **POST-PROCESSING** | |
| Post-Processing | Potato |
| Motion Blur | Disabled |
| Depth of Field | Disabled |
| Lens Flare | Disabled |
| Bloom | Disabled |
| **TEXTURES** | |
| World | Potato |
| Character | Potato |
| Effects | Potato |
| Texture Streaming | Potato |

* DLSS / DLAA працює лише на відеокартах RTX.
* Повзунки «Quality» у Motion Blur, Depth of Field, Lens Flare та Bloom стають сірими, коли ефект вимкнено. Не звертайте на них уваги.

**Застосуйте налаштування й повністю закрийте гру.** Крок 2 виконується лише із закритою грою.

---

## Крок 2. Повністю вимикаємо тіні (GameUserSettings.ini)

Мінімум тіней у меню — Low, але через файл конфігурації можна опуститися ще нижче.

1. Переконайтеся, що WARDOGS **повністю закрита**. Ніколи не редагуйте цей файл, коли гра запущена.
2. Натисніть **Win + R**, вставте `%localappdata%\Wardogs\Saved\Config\WindowsClient` і натисніть **Enter**.
3. **Зробіть резервну копію:** скопіюйте **GameUserSettings.ini** у надійне місце, наприклад на робочий стіл.
4. Відкрийте **GameUserSettings.ini** у Блокноті, натисніть **Ctrl + F** і знайдіть `sg.ShadowQuality`.
5. Замініть цей рядок на `sg.ShadowQuality=4`, збережіть файл і закрийте Блокнот.
6. Клацніть правою кнопкою миші на **GameUserSettings.ini** → **Властивості** → позначте **Лише для читання** → **OK**. Так гра не перезапише вашу зміну.

> 💡 Поки файл доступний лише для читання, зміни в меню налаштувань гри не зберігаються. Щоб щось змінити пізніше: зніміть «Лише для читання» → змініть налаштування в грі → закрийте гру → повторіть кроки 4–6.

---

## Крок 3. NVIDIA Profile Inspector (LOD Bias)

LOD Bias змушує гру використовувати версії текстур із меншою деталізацією. Текстури стають розмитішими, а листя меншає.

Завантажте NPI за посиланням вище, розпакуйте архів і запустіть `nvidiaProfileInspector.exe`.

### Варіант A: імпорт готового профілю (найпростіше)

1. Завантажте один із профілів. Відкрийте файл і натисніть **Download raw file**.
    * [`WARDOGS_potato_LOD3_balanced.nip`](profiles/WARDOGS_potato_LOD3_balanced.nip) (**рекомендовано**, LOD Bias +3)
    * [`WARDOGS_potato_LOD15_max.nip`](profiles/WARDOGS_potato_LOD15_max.nip) (максимальна картопля, LOD Bias +15, ламає мінікарту)
2. У NPI натисніть на панелі інструментів **Import user defined profiles** і виберіть файл `.nip`.
3. Натисніть **Apply changes** (праворуч угорі).

### Варіант B: ручне налаштування

1. У полі **Profiles** угорі введіть `WARDOGS` і виберіть профіль.
    * Профілю WARDOGS немає? Натисніть **Create new profile** і назвіть його `WARDOGS`. Потім натисніть **Add application to current profile** і виберіть `wardogsclient-win64-shipping.exe` у теці з грою. У Steam її можна відкрити так: правий клік на WARDOGS → Керування → Переглянути локальні файли (Manage → Browse local files).
2. Змініть три налаштування з таблиці нижче. Значення можна вибрати у випадному списку або ввести hex-код вручну.
3. Натисніть **Apply changes** (праворуч угорі).
4. Якщо гра була запущена, перезапустіть її.

| Налаштування | Значення | Hex |
|:--|:--|:--|
| Antialiasing - Transparency Supersampling | AA_MODE_REPLAY_MODE_ALL | `0x00000008` |
| Texture filtering - Driver Controlled LOD Bias | Off | `0x00000000` |
| Texture filtering - LOD Bias | +3 *(див. нижче)* | `0x00000018` |

Перші два налаштування потрібні, щоб драйвер узагалі застосував ваш LOD Bias. Без них третє нічого не робить.

---

## Який LOD Bias обрати?

| LOD Bias | Hex | Результат |
|:--|:--|:--|
| **+3** | `0x00000018` | **Рекомендовано.** Добрий баланс між зручністю гри та перевагою. Мінікарта працює. |
| від +4 до +15 | — | ❌ Мінікартою неможливо користуватися. |
| +15 | `0x00000078` | Максимальна картопля. Це скриншот «після». |

**Коротко: ставте +3**, якщо не готові грати без мінікарти.

*Підказка: hex-значення = LOD Bias × 8. Наприклад, +3 → 24 → `0x18`.*

---

## Як усе скасувати

* **NPI:** виберіть профіль WARDOGS → натисніть **Restore current profile to NVIDIA defaults** → **Apply changes**.
* **Тіні:** коли гра закрита, зніміть **Лише для читання** з GameUserSettings.ini і поверніть резервну копію.
* **У грі:** виберіть будь-який пресет в **Overall Quality**.

---

## Відомі проблеми

* **Мінікартою неможливо користуватися:** LOD Bias вищий за +3. Поверніть +3 (`0x00000018`).
* **Налаштування в грі не зберігаються:** GameUserSettings.ini досі доступний лише для читання після кроку 2. Так і має бути.
* **Відеокарта AMD / Intel:** NPI працює лише з NVIDIA, але кроки 1–2 однаково підійдуть.

---

## Шпаргалка

![Шпаргалка WARDOGS: усі налаштування](images/cheatsheet.png)

Щось змінилося після оновлення гри? [Створіть issue](../../issues).
