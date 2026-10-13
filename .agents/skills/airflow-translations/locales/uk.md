<!-- SPDX-License-Identifier: Apache-2.0
     https://www.apache.org/licenses/LICENSE-2.0 -->

# Ukrainian (uk)

This document provides locale-specific instructions for translating English
Airflow UI strings into Ukrainian. It inherits all global rules from the parent
[SKILL.md](../SKILL.md).

## Translation Philosophy

The goal is an interface that feels natural to a Ukrainian-speaking developer
without sacrificing precision or alienating people used to English technical
terminology. Three principles decide every term:

1. **Translate when an exact, widely used Ukrainian equivalent exists.** Don't
   transliterate a word that already has an established native counterpart with
   the same connotation.
2. **Transliterate when a translation sounds artificial** or is no longer
   perceived as a translation — «асет» is clearer than «актив», «провайдер» is
   already part of the technical vocabulary.
3. **Keep the original for proper names, abbreviations, and technical
   identifiers** — `Dag`, `XCom`, `API` are part of the programming interface,
   not of natural language.

## 1. Terms Kept in English

| Term | Why it is not translated |
|------|--------------------------|
| `Dag` | Airflow's central concept. «Даг» is possible but reads poorly. Used as `Dag` with Ukrainian case endings after a hyphen: `Dag-а`, `Dag-и`, `Dag-ів`. |
| `XCom` | Proper name of Airflow's cross-task data mechanism. Any translation («крос-комунікація») only confuses. |
| `API`, `REST`, `JSON` | Universally understood abbreviations. |
| `URI`, `URL` | Technical protocol abbreviations. |
| `Task SDK` | Product component name. |

### Declension of abbreviations

Letter-by-letter abbreviations (А-ПІ, Джей-Сон, У-ЕР-ЕЛ) **are not declined**
(Ukrainian orthography):

- ✅ `формат JSON`, `конфігурація API`
- ❌ `JSON-а`, `API-у`

Only name-like abbreviations that are read as words are declined: `Airflow-а`,
`Dag-а`, `XCom-и`.

### Declension of `Dag`

`Dag` is an invariable foreign word, so case endings are attached with a hyphen:

| Case | Form | Example |
|------|------|---------|
| Nominative | `Dag` | «Dag активний» |
| Genitive | `Dag-а` / `Dag-ів` | «Запуск Dag-а», «Список Dag-ів» |
| Accusative | `Dag` / `Dag-и` | «Запустити Dag», «Переглянути Dag-и» |

```json
"dagRun_one": "Запуск Dag-а",
"dagRun_other": "Запуски Dag-а",
"dagId": "Ідентифікатор Dag-а",
"browse": { "xcoms": "XCom-и" }
```

> Airflow 3 documentation spells the concept `Dag` (not `DAG`), and this locale
> follows that spelling.

## 2. Transliterated Terms

Many technical terms are already established in Ukrainian IT usage as direct
transliterations:

| English | Ukrainian | Rationale |
|---------|-----------|-----------|
| Operator | Оператор | Long established in Ukrainian (mathematical operator, telecom operator). |
| Trigger | Тригер | Standard term from electronics and programming. |
| Triggerer | Тригерер | `Trigger` (the object) and `Triggerer` (the component) are distinct entities that appear on the same screen; collapsing both into «тригер» loses information. |
| Provider | Провайдер | «Постачальник» is technically correct, but for Airflow provider packages «провайдер» is more precise and more familiar. |
| Plugin | Плагін | «Додаток» and «розширення» are broader; «плагін» names a pluggable module exactly. |
| Asset | Асет | «Ресурс», «актив», «об'єкт даних» are all imprecise. «Асет» keeps the term unique and is widely used in the community. |
| Job | Процес | A Job in Airflow is a long-running component process (`SchedulerJob`) with a host, PID and heartbeat, not a unit of work, so «Процес» names it exactly. «Завдання» is already taken by `Task`; «задача» is its near-synonym and would blur the two. The transliteration «джоб» reads as slang. Job type filter labels follow the component names: «Процес планувальника», «Процес тригерера», «Процес Dag-процесора». Only the label is translated; the filter still sends `SchedulerJob` etc. to the API, and the Jobs table column shows those raw class names. |
| Partition | Партиція | Established in data engineering (Spark, Kafka partitions). Derived form: «партиційований запуск Dag-а». |
| Slot | Слот | Pool slots; «місце» would be ambiguous. |
| Map / Mapped | Мапінг / Мапінгові | Dynamic task mapping. «Відображення» reads as "displayed" in a UI («відображені завдання» = "shown tasks»), and «розгорнуті» is already taken by expand/collapse. `map_index` → «Індекс мапінгу», `notMapped` → «Без мапінгу». |

```json
"taskInstance": {
  "pool": "Пул",
  "poolSlots": "Слоти пулу",
  "triggerer": { "title": "Інформація про тригерер" }
},
"asset_one": "Асет",
"asset_other": "Асети"
```

## 3. Fully Translated Terms

Terms with an exact and natural Ukrainian equivalent are translated in full:

| English | Ukrainian | Rationale |
|---------|-----------|-----------|
| Task | Завдання | Neutral and precise. |
| Run | Запуск | Verbal noun from «запустити»; conveys a one-time execution. |
| Schedule | Розклад | Standard scheduling and sysadmin term. |
| Timetable | Розклад | Same word as `Schedule`: the UI never shows the two side by side, and «часовий розклад» reads as redundant («Тип розкладу», «Типів розкладу не знайдено»). |
| Connection | З'єднання | Technically exact; used in networking documentation. |
| State | Стан | «Статус» is also used, but «стан» is more neutral and precise for machine states. |
| Catchup | Довиконання | Conveys that Airflow "completes" missed schedule intervals — more precise than a literal «наздоганяння». |
| Backfill | Дозаповнення | The «до-» prefix conveys completion of what is missing. |
| Duration | Тривалість | Exact translation for a time span. |
| Queue | Черга | Standard data-structure term. |
| Default | Типовий | «За замовчуванням» is a calque; «типовий» is shorter and fits in a button. Not to be confused with `Standard` («стандартні поля»), which stays «стандартний». |
| Parse / Reparse | Обробка / Повторна обробка | «Парсинг», «перепарсити» are jargon and out of place in UI labels. |
| Watcher | Спостерігач | Asset watcher; the natural agent noun. |
| Alias | Псевдонім | Standard Ukrainian computing term. |
| Team | Команда | Multi-team deployments. |
| Executor | Виконавець | The component that executes tasks. |
| Heartbeat | Сигнал активності | Used consistently for scheduler, triggerer, and job heartbeats («Останній сигнал активності»). «Активний сигнал» reads as "an active signal", not a heartbeat. |
| Trigger rule | Правило запуску | Decides when a task starts; «правило тригера» would wrongly point at the deferrable `Trigger`. |
| Worker | Воркер | «Виконавець» is already taken by `Executor`. |
| Dag bundle | Набір Dag-ів | A bundle is a set of Dag files from one source (Git repository, local folder, S3) with a name and a version. Short forms: «Назва набору», «Версія набору», «Набори». «Пакет» is already taken by provider packages («Назва пакета»), «джерело» by sources («Показати джерело», «асет-джерело»), and the transliteration «бандл» reads as slang. |
| Download / Upload | Завантажити / Виберіть файл | Using «завантажити» for both directions is ambiguous; file pickers say «Виберіть файл». |
| Awaiting input (state) | Очікує відповіді | A Human-in-the-loop task waiting for a person's response. Matches the HITL strings («Відповідь отримано», «Необхідна відповідь») and the other waiting states («Очікує повторної спроби»); «введення» reads as typing on a keyboard. |
| Dashboard | Головна | The Airflow home dashboard. It is a narrow sidebar label, the page's own title already uses `nav.home` («Головна»), and «Панель керування» wraps under the icon. |
| Drain / Draining | Завершити розпочате / Призупиняється | Let in-flight Dag runs finish, then pause. «Довиконати» is already taken by `Catchup`. The state is the reflexive imperfective «Призупиняється», which sits naturally next to «Активний» and «Призупинений»; actions use «Завершити розпочате й призупинити». |
| Iteration (loop) | Ітерація | Loop-task iterations («Ітерація {{index}}», «Максимальна кількість ітерацій»). |
| Callback | Зворотний виклик | Standard Ukrainian computing term; «колбек» is jargon. |

```json
"states": {
  "running":   "Виконується",
  "success":   "Успіх",
  "failed":    "Невдача",
  "queued":    "У черзі",
  "scheduled": "Заплановано",
  "skipped":   "Пропущено",
  "deferred":  "Відкладено"
},
"task_one": "Завдання",
"dagDetails": {
  "catchup": "Довиконання",
  "schedule": "Розклад"
}
```

## Plural Forms

Ukrainian has **four plural forms**, mapped onto i18next suffixes:

| Suffix | Case | When it applies | Example |
|--------|------|-----------------|---------|
| `_one` | nominative singular | 1, 21, 31, 41, … | 1 завдання, 21 завдання |
| `_few` | nominative plural | 2-4, 22-24, 32-34, … | 22 завдання |
| `_many` | genitive plural | 0, 5-20, 25-30, … | 5 завдань |
| `_other` | see below | fractions (1.5, 2.7, …) **or** a standalone label with no `{{count}}` | see below |

```json
"taskInstance_one":   "Екземпляр завдання",
"taskInstance_few":   "Екземпляри завдань",
"taskInstance_many":  "Екземплярів завдань",
"taskInstance_other": "Екземпляри завдань"
```

### Never hard-code the number in `_one`

English `_one` means exactly 1, so the English source may write the digit
literally ("Delete 1 connection"). Ukrainian `_one` also covers 21, 31, 41, …,
so a literal `1` renders "Видалити 1 з'єднання" for a count of 21. Always
interpolate `{{count, number}}`, which i18next guarantees is present whenever a plural
is resolved:

```json
// ✅
"deleteConnection_one": "Видалити {{count, number}} з'єднання"
// ❌ — renders "1" when count is 21
"deleteConnection_one": "Видалити 1 з'єднання"
```

The exception is a `_one` key that the code calls directly, without `count`
(`translate("dagWarnings.error_one")`). There `{{count, number}}` would render
verbatim, so keep the literal number: `"error_one": "1 помилка"`. Check the call
site when an English `_one` has no `{{count}}`.

### The dual role of `_other`

**Role 1 — formal (fractions with `{{count}}`).** When `{{count}}` is present,
this form is selected for fractional values (1.5, 2.7). Such values are rare in
Airflow's UI, so this is mostly a technical fallback:

```json
"deleteConnection_other": "Видалити {{count, number}} з'єднання",
"affected_other": "{{count, number}} запуску буде розпочато.",
"pendingDagRun_other": "{{count, number}} очікуваного запуску Dag-а"
```

Fractions take the **genitive singular**: «1,5 запуску», «2,5 змінної». An
adjective between the number and the noun agrees with the noun, so it is
genitive singular too: «1,5 очікуваного запуску», never «1,5 очікуваних
запуску».

**Role 2 — practical (standalone label without `{{count}}`).** When the string
contains no `{{count}}`, the `_other` key is called directly from code as the
generic category name — navigation menus, table headings, section titles. That
needs the **nominative plural**, exactly like `_few`:

```json
"taskInstance_other": "Екземпляри завдань",
"dagRun_other": "Запуски Dag-а"
```

### Algorithm for `_other`

1. **Does the string contain `{{count}}`?**
2. If **no** — copy the `_few` form (nominative plural).
3. If **yes**, look at **where** `{{count}}` sits:
   - **Inside a numeral phrase** (`{{count}} завдання`, `Видалити {{count}}
     змінної`) — noun in **genitive singular**, modifiers in **genitive
     plural**: «Останніх 1,5 запуску Dag-а».
   - **In parentheses or brackets** (`Необхідні дії ({{count}})`, `Екземпляри
     завдань [{{count}}]`) — this is a label with a counter badge, not a numeral
     phrase. Use the **nominative plural**, like `_few`.

> **Why `_few` is the model for label context.** `_few` is the natural
> nominative plural («Запуски», «Екземпляри»), whereas `_many` is genitive and
> only reads correctly next to a number («5 запусків»). Headings and navigation
> without a number need the nominative.

## Verb Aspect

- **Action buttons and menu items** — perfective infinitive: «Видалити»,
  «Додати», «Скасувати»
- **Placeholders and instructions** — imperative: «Виберіть стан», «Додайте
  примітку…», «Вкажіть ключ»
- **Success messages** — impersonal passive, perfective: «Успішно видалено»,
  «Запуск розпочато»
- **Failure messages** — «Не вдалося …», not «… не вдався»: «Не вдалося
  виконати пробний запуск»
- **Current state** — imperfective: «Виконується», «Призупиняється»,
  «Завантаження…»

`success` and `failed` are nouns («Успіх», «Невдача») on purpose: the adverb
«невдало» also means "clumsily" («невдалий жарт»), which is wrong for a state
badge.

`upstream_failed` is «Невдача в попередньому завданні», not «Невдача
попередника»: the genitive reads as the predecessor's own misfortune, and
upstream tasks are «Попередні» everywhere else in the UI.

For the same reason, an entity in the failed state is «неуспішний», never
«невдалий». «Невдалі завдання» or «Невдалі Dag-и» read as "badly made tasks/Dags",
while «неуспішний» mirrors «успішний»: «Неуспішні завдання», «Позначити
завдання як неуспішне», «Немає неуспішних запусків».

## Style

- **Log levels stay in English** (`DEBUG`, `INFO`, `WARNING`, `ERROR`,
  `CRITICAL`) — they must match what appears in the log lines themselves.
- **Timestamp column headers** use «Час …» («Час створення», «Час оновлення»),
  never a dangling «Створено о».
- **Tooltips**: «Натисніть {{hotkey}}, щоб …», not «Натисніть {{hotkey}} для …».
- **Toggle** is not «Перемкнути X»: write «Показати або приховати X»,
  «Увімкнути або вимкнути X», «Розгорнути або згорнути X».
- **Quotes** are «…» everywhere, including around `{{placeholders}}` and
  `$t()` references. The only straight `"` are inside literal JSON examples
  (`{"key": "value"}`).
- **Ellipsis** is the single character «…», never three dots, even where the
  English source uses `...`. The exception is literal JSON (`{"key": "value", ...}`).
- **Required-field validation** is «Вкажіть <поле>» or «Обов'язкове поле», not
  the calque «<Поле> є обов'язковим».
- Prefer «Усі» at the start of a label; «всі» only mid-sentence after a vowel.
- Avoid calques: «такі» (not «наступні») for "the following", «наявні»
  (not «існуючі»), «під час» (not «при»), «у разі» (not «у випадку»),
  «Буде видалено …» (not «Це видалить …»), «враховувати» (not «включати»)
  for "include in a count".

## Addressing the User

Use the polite **«ви»** form in confirmation dialogs:

```json
"confirmation": "Ви впевнені, що хочете видалити {{resourceName}}? Цю дію неможливо скасувати."
```

## Word Order in Compound Terms

Ukrainian compound terms follow "head noun + dependent noun in the genitive":

| English | Ukrainian | Structure |
|---------|-----------|-----------|
| Airflow configuration | конфігурація Airflow-а | конфігурація (чого?) + Airflow |
| user interface | інтерфейс користувача | інтерфейс (чий?) + користувача |
| task instance | екземпляр завдання | екземпляр (якого?) + завдання |
| Dag run | запуск Dag-а | запуск (чий?) + Dag-а |
| connection pool | пул з'єднань | пул (яких?) + з'єднань |
| JSON response | відповідь JSON | відповідь (яка?) + JSON |

> "Generic + proper" is the norm. "Proper + generic" is acceptable only for
> established terms.

## Interpolation and Case Agreement

A substituted noun keeps one fixed form, but Ukrainian needs the case the
sentence governs.

- **Don't copy `$t()` from English into a sentence.** `$t(key)` pastes in that
  key's translation, always in the same form. "Search $t(common:dag_other)"
  works in English, but in Ukrainian it renders «Пошук Dag-и» instead of «Пошук
  Dag-ів». Write the word in the case the sentence needs: «Пошук Dag-ів». Keep
  `$t()` only for a button name in quotes, which never changes form: «Натисніть
  «$t(review.viewAll)», щоб переглянути всі».
- **A value with one host takes that host's case.** `deadlineAlerts.referenceType.*`
  only fills `{{reference}}` after «від», so it is genitive: «логічної дати».
- **A label substituted by code stays nominative.** `common.toaster.*` gets
  `{{resourceName}}` as «Запуски Dag-а» or «Змінна», so «Успішно видалено 5
  {{resourceName}}» breaks; put the placeholder where the nominative fits, such
  as after a colon. Strings concatenated in code (`TriggeredRuns.tsx`) need a
  code fix.

## Preserve Leading and Trailing Whitespace

Some English strings carry a leading or trailing space because the UI
concatenates them with another string. Keep that whitespace:

```json
"created": "Відповідь створено о ",
"thirdConfirmMessage": " Ви впевнені, що хочете продовжити?"
```
