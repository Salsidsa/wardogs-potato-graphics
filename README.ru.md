[English](README.md) | **Русский** | [Українська](README.uk.md) | [Deutsch](README.de.md)

# WARDOGS: гайд по картофельной графике 🥔

Ультранизкая («картофельная») графика для **WARDOGS**: настройки Potato в игре, одна строка в `GameUserSettings.ini` и **LOD Bias** через **NVIDIA Profile Inspector**.

**Кратко:** настройки Potato в игре → `sg.ShadowQuality=4` в GameUserSettings.ini (файл только для чтения) → NVIDIA Profile Inspector с LOD Bias **+3**. В итоге: никаких теней, намного меньше листвы и плоские текстуры с низкой детализацией.

*Обновлено: 2026-10-27. Игра продолжает обновляться, поэтому настройки могут измениться.*

![WARDOGS до и после картофельной графики](images/before-after.png)

*На скриншоте «после» стоит максимальный LOD Bias +15. Рекомендуемое значение — +3 ([почему](#какой-lod-bias-выбрать)).*

> ⚠️ **Используйте на свой страх и риск.** Разработчики пока никак не высказывались о NVIDIA Profile Inspector и в будущем могут его запретить. Если это случится, верните всё как было (см. [Как всё откатить](#как-всё-откатить)).

---

## Что понадобится

* **Видеокарта NVIDIA.** NVIDIA Profile Inspector работает только с драйверами NVIDIA. Шаги 1–2 подходят для любой видеокарты.
* **NVIDIA Profile Inspector** (NPI) с официального GitHub: https://github.com/Orbmu2k/nvidiaProfileInspector/releases
* Около 10 минут

---

## Шаг 1. Настройки в игре

Откройте настройки графики в игре и выставьте всё как в таблице. В **Overall Quality** появится **Custom** — так и должно быть.

*Названия настроек указаны как в английском интерфейсе игры.*

| Настройка | Значение |
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
| Shadows | Low *(в шаге 2 тени отключаются полностью)* |
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

* DLSS / DLAA работает только на видеокартах RTX.
* Ползунки «Quality» у Motion Blur, Depth of Field, Lens Flare и Bloom становятся серыми, когда эффект выключен. Не обращайте на них внимания.

**Примените настройки и полностью закройте игру.** Шаг 2 делается только с закрытой игрой.

---

## Шаг 2. Полностью отключаем тени (GameUserSettings.ini)

Минимум теней в меню — Low, но через файл конфигурации можно опуститься ниже.

1. Убедитесь, что WARDOGS **полностью закрыта**. Никогда не редактируйте этот файл при запущенной игре.
2. Нажмите **Win + R**, вставьте `%localappdata%\Wardogs\Saved\Config\WindowsClient` и нажмите **Enter**.
3. **Сделайте резервную копию:** скопируйте **GameUserSettings.ini** в надёжное место, например на рабочий стол.
4. Откройте **GameUserSettings.ini** в Блокноте, нажмите **Ctrl + F** и найдите `sg.ShadowQuality`.
5. Замените эту строку на `sg.ShadowQuality=4`, сохраните файл и закройте Блокнот.
6. Щёлкните правой кнопкой мыши по **GameUserSettings.ini** → **Свойства** → отметьте **Только чтение** → **ОК**. Так игра не перезапишет ваше изменение.

> 💡 Пока файл доступен только для чтения, изменения в меню настроек игры не сохраняются. Чтобы что-то поменять позже: снимите «Только чтение» → измените настройку в игре → закройте игру → повторите шаги 4–6.

---

## Шаг 3. NVIDIA Profile Inspector (LOD Bias)

LOD Bias заставляет игру использовать версии текстур с меньшей детализацией. Текстуры становятся размытее, а листвы становится меньше.

Скачайте NPI по ссылке выше, распакуйте архив и запустите `nvidiaProfileInspector.exe`.

### Вариант A: импорт готового профиля (проще всего)

1. Скачайте один из профилей. Откройте файл и нажмите **Download raw file**.
    * [`WARDOGS_potato_LOD3_balanced.nip`](profiles/WARDOGS_potato_LOD3_balanced.nip) (**рекомендуется**, LOD Bias +3)
    * [`WARDOGS_potato_LOD15_max.nip`](profiles/WARDOGS_potato_LOD15_max.nip) (максимальная картошка, LOD Bias +15, ломает миникарту)
2. В NPI нажмите на панели инструментов **Import user defined profiles** и выберите файл `.nip`.
3. Нажмите **Apply changes** (справа вверху).

### Вариант B: ручная настройка

1. В поле **Profiles** вверху введите `WARDOGS` и выберите профиль.
    * Профиля WARDOGS нет? Нажмите **Create new profile** и назовите его `WARDOGS`. Затем нажмите **Add application to current profile** и выберите `wardogsclient-win64-shipping.exe` в папке с игрой. В Steam её можно открыть так: правый клик по WARDOGS → Управление → Просмотреть локальные файлы (Manage → Browse local files).
2. Измените три настройки из таблицы ниже. Значение можно выбрать в выпадающем списке или ввести hex-код вручную.
3. Нажмите **Apply changes** (справа вверху).
4. Если игра была запущена, перезапустите её.

| Настройка | Значение | Hex |
|:--|:--|:--|
| Antialiasing - Transparency Supersampling | AA_MODE_REPLAY_MODE_ALL | `0x00000008` |
| Texture filtering - Driver Controlled LOD Bias | Off | `0x00000000` |
| Texture filtering - LOD Bias | +3 *(см. ниже)* | `0x00000018` |

Первые две настройки нужны, чтобы драйвер вообще применил ваш LOD Bias. Без них третья ничего не делает.

---

## Какой LOD Bias выбрать?

| LOD Bias | Hex | Результат |
|:--|:--|:--|
| **+3** | `0x00000018` | **Рекомендуется.** Хороший баланс между играбельностью и преимуществом. Миникарта работает. |
| от +4 до +15 | — | ❌ Миникартой невозможно пользоваться. |
| +15 | `0x00000078` | Максимальная картошка. Это скриншот «после». |

**Кратко: ставьте +3**, если не готовы играть без миникарты.

*Подсказка: hex-значение = LOD Bias × 8. Например, +3 → 24 → `0x18`.*

---

## Как всё откатить

* **NPI:** выберите профиль WARDOGS → нажмите **Restore current profile to NVIDIA defaults** → **Apply changes**.
* **Тени:** при закрытой игре снимите **Только чтение** с GameUserSettings.ini и верните резервную копию.
* **В игре:** выберите любой пресет в **Overall Quality**.

---

## Известные проблемы

* **Миникартой невозможно пользоваться:** LOD Bias выше +3. Верните +3 (`0x00000018`).
* **Настройки в игре не сохраняются:** GameUserSettings.ini всё ещё доступен только для чтения после шага 2. Так и должно быть.
* **Видеокарта AMD / Intel:** NPI работает только с NVIDIA, но шаги 1–2 всё равно подойдут.

---

## Шпаргалка

![Шпаргалка WARDOGS: все настройки](images/cheatsheet.png)

Что-то изменилось после обновления игры? [Создайте issue](../../issues).
