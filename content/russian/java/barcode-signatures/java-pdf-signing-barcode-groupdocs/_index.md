---
categories:
- Java PDF Processing
date: '2026-07-20'
description: Узнайте, как создать barcode signature в PDF‑документах с помощью Java
  и GroupDocs.Signature. Пошаговое руководство с примерами кода и лучшими практиками.
keywords:
- create barcode signature
- how to add barcode
- generate code128 barcode
- add barcode pdf
- tamper evident barcode
lastmod: '2026-07-20'
linktitle: Создать Barcode Signature на Java
og_description: Создайте barcode signature в PDF с помощью Java и GroupDocs.Signature.
  Узнайте пошагово, как добавить штрих‑коды Code128, разместить их и защитить документы.
og_image_alt: 'Developer guide: Create barcode signature in PDF using Java and GroupDocs'
og_title: Создать Barcode Signature в PDF с помощью Java – Полное руководство
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to create barcode signature in PDF documents using Java and
    GroupDocs.Signature. Step-by-step tutorial with code examples and best practices.
  headline: How to Create Barcode Signature in PDF using Java
  type: TechArticle
- description: Learn how to create barcode signature in PDF documents using Java and
    GroupDocs.Signature. Step-by-step tutorial with code examples and best practices.
  name: How to Create Barcode Signature in PDF using Java
  steps:
  - name: Initialize the Signature object
    text: '**Definition anchor:** The `Signature` class is GroupDocs.Signature''s
      entry point for loading, modifying, and saving PDF documents. First, you need
      to tell GroupDocs which PDF you''re working with: **What''s happening here:**
      The `Signature` object loads your PDF into memory and prepares it for modifi'
  - name: Configure your barcode options (How to add barcode)
    text: '**Definition anchor:** `BarcodeSignOptions` encapsulates all settings required
      to render a barcode inside a PDF. Now let''s create the barcode signature with
      your data: - `"12345678"` is your barcode data — this could be an order ID,
      certificate number, or any identifier you need. - `Code128` is the '
  - name: Position your barcode (How to sign PDF with barcode)
    text: '**Definition anchor:** `SignatureOptions` provides layout properties such
      as page number, size, and alignment. Here''s where GroupDocs really shines —
      percentage‑based positioning means your barcode looks good on any PDF size:
      **Why percentages matter:** Imagine you''re signing both A4 documents and l'
  - name: Sign and save your document (How to add barcode pdf)
    text: 'Time to actually apply the signature and save your work: **Important note:**
      The output directory must exist before you run this code. GroupDocs won''t create
      nested directories for you, so create them first or handle that in your code:
      **What if something goes wrong?** Wrap this in a try‑catch block'
  type: HowTo
- questions:
  - answer: Yes! Call `signature.sign()` multiple times with different `BarcodeSignOptions`
      for each barcode type. Just ensure they don’t overlap.
    question: Can I use different barcode types in the same PDF?
  - answer: Code128 handles most ASCII characters fine. For Unicode or complex data,
      switch to QR codes—they support UTF‑8 encoding.
    question: How do I handle barcodes that contain special characters?
  - answer: Technically up to 128 characters, but readability drops significantly
      above 30‑40 characters. For larger payloads, use QR codes.
    question: What's the maximum data I can store in a Code128 barcode?
  - answer: Not noticeably—barcodes are vector graphics, typically adding only 5‑20
      KB per barcode depending on size and complexity.
    question: Will adding barcodes significantly increase my PDF file size?
  - answer: Yes! Use `options.setRotationAngle(90)` to rotate your barcode, which
      is handy for margin placement.
    question: Can I rotate barcodes or place them vertically?
  type: FAQPage
tags:
- pdf-signing
- barcode-signature
- document-security
- groupdocs
- java
- pdf
title: Как создать подпись Barcode Signature в PDF с помощью Java
type: docs
url: /ru/java/barcode-signatures/java-pdf-signing-barcode-groupdocs/
weight: 1
---

# Как создать штрих‑код подпись в PDF с помощью Java

В этом руководстве вы узнаете, как **создать штрих‑код подпись** в PDF‑файлах с помощью Java и GroupDocs.Signature. Штрих‑код подписи встраивает машинно‑читаемые идентификаторы, которые одновременно являются доказательством целостности и легко сканируются — идеально подходят для контрактов, сертификатов, счетов и любых документов, требующих надёжной проверки.

## Быстрые ответы
- **Что такое штрих‑код подпись?** Штрих‑код, встроенный в PDF, который хранит структурированные данные и может быть считан сканерами или программным обеспечением.  
- **Какой тип штрих‑кода рекомендуется?** Code128, потому что он компактно обрабатывает буквенно‑цифровые данные.  
- **Нужна ли лицензия?** Бесплатная пробная версия подходит для тестирования; полная лицензия требуется для продакшн.  
- **Можно ли разместить штрих‑код на любой размер страницы?** Да — используйте позиционирование в процентах для автоматического масштабирования.  
- **Штрих‑код векторный?** Да, он добавляет к PDF всего несколько килобайт и остаётся чётким при любой разрешающей способности.  

## Что такое штрих‑код подпись?
Штрих‑код подпись — это векторный штрих‑код, встроенный непосредственно в страницу PDF, выступающий одновременно как визуальный элемент и как криптографическая подпись, которую можно проверить позже. Он хранит структурированные данные, такие как идентификаторы или метки времени, и обеспечивает целостность документа, предоставляя машинно‑читаемую ссылку.

## Почему штрих‑код подписи важны для ваших PDF
Штрих‑код подписи дают PDF компактный, машинно‑читаемый идентификатор, который можно мгновенно отсканировать, устраняя ручной ввод данных и снижая количество ошибок. Поскольку они встроены как векторная графика, они остаются чёткими при любой разрешающей способности и добавляют к файлу всего несколько килобайт. Такое сочетание читаемости, доказательства целостности и небольшого размера делает их идеальными для контрактов, счетов, сертификатов и любых документов, требующих надёжной проверки.

Вот задача, с которой вы, вероятно, сталкивались: необходимо добавить уникальные идентификаторы в PDF, которые одновременно машинно‑читаемы и свидетельствуют о попытке подделки. Возможно, вы работаете над системой управления документами, обрабатываете сертификаты или имеете дело с контрактами, требующими последующей проверки.

Именно здесь штрих‑код подписи оказываются полезными. В отличие от простых текстовых штампов, штрих‑коды позволяют встраивать структурированные данные, которые сканеры (и ваше программное обеспечение) могут сразу считать. Кроме того, сочетая их с подписанием PDF через GroupDocs.Signature для Java, вы получаете мощный способ отслеживать и проверять документы без необходимости сложных запросов к базе данных.

В этом руководстве вы узнаете, как реализовать штрих‑код подпись в ваших Java‑PDF — от базовой настройки до готового к продакшн кода с гибким позиционированием. Независимо от того, создаёте ли вы систему выставления счетов, генератор сертификатов или платформу управления контрактами, к концу вы получите всё необходимое.

**Чему вы научитесь:**
- Настройка GroupDocs.Signature для Java за несколько минут  
- Создание штрих‑кодов Code128 (и почему они часто являются лучшим выбором)  
- Размещение штрих‑кодов с помощью позиционирования в процентах, которое работает для любого размера PDF  
- Избежание распространённых ошибок, с которыми сталкиваются разработчики  
- Корректное тестирование вашей реализации  

## Как создать штрих‑код подпись в Java
Создание штрих‑кода подписи в Java включает загрузку целевого PDF, настройку параметров штрих‑кода, таких как данные, тип, размер и позиция, а затем применение подписи для создания нового документа. GroupDocs.Signature обрабатывает рендеринг и криптографическое связывание, поэтому вам нужно лишь передать нужные параметры и управлять путями к файлам.

## Предварительные требования и проверка окружения
Прежде чем приступать, убедитесь, что у вас готовы следующие элементы:

- **Java Development Kit (JDK) 8 или новее** — требуется для всех библиотек GroupDocs Java.  
- **Maven или Gradle** — для управления зависимостью GroupDocs.Signature.  
- **IDE** (например, IntelliJ IDEA, Eclipse или VS Code с Java‑расширениями).  
- **GroupDocs.Signature for Java** (рекомендуется версия 23.12 или новее).  
- **Базовые знания Java** — вы должны уверенно создавать классы, обрабатывать исключения и работать с вводом‑выводом файлов.  

## Настройка GroupDocs.Signature в вашем проекте
Подключить библиотеку к проекту просто. Выберите ваш инструмент сборки:

**Для пользователей Maven** добавьте эту зависимость в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Используете Gradle?** Добавьте эту строку в ваш `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Предпочитаете ручную настройку?** Скачайте JAR напрямую с [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) и добавьте его в ваш classpath.

### Получение лицензии
Прежде чем перейти к полной эксплуатации, вам нужно решить вопрос лицензирования:

- **Бесплатная пробная версия:** Идеально для тестирования — получите её на сайте GroupDocs, чтобы изучить основные функции.  
- **Временная лицензия:** Нужно больше времени для оценки? Оформите 30‑дневную временную лицензию.  
- **Полная лицензия:** Готовы к продакшн? Приобретите лицензию с неограниченным использованием.  

Вот быстрая проверка, чтобы убедиться, что всё работает:

```java
Signature signature = new Signature("sample.pdf");
System.out.println("Signature object created successfully.");
```

Если код выполнится без ошибок, вы готовы!

## Как создать штрих‑код подпись в Java
А теперь самая интересная часть — подпишем PDF штрих‑кодом. Мы разобьём процесс на небольшие шаги, чтобы вы точно понимали, что происходит на каждом этапе.

### Шаг 1: Инициализация объекта Signature
**Определение:** Класс `Signature` — точка входа GroupDocs.Signature для загрузки, изменения и сохранения PDF‑документов.

Сначала нужно указать GroupDocs, с каким PDF вы работаете:

```java
Signature signature = new Signature("input.pdf");
```

**Что происходит:** Объект `Signature` загружает ваш PDF в память и подготавливает его к изменениям. Убедитесь, что путь к файлу правильный — частая ошибка — использование обратных слешей в Windows без экранирования (используйте `\\` или просто прямые слеши, которые работают кроссплатформенно).

### Шаг 2: Настройка параметров штрих‑кода (Как добавить штрих‑код)
**Определение:** `BarcodeSignOptions` инкапсулирует все настройки, необходимые для отрисовки штрих‑кода внутри PDF.

Теперь создадим штрих‑код подпись с вашими данными:

```java
BarcodeSignOptions options = new BarcodeSignOptions("12345678");
options.setEncodeType(BarcodeEncodeType.Code128);
```

- `"12345678"` — ваши данные штрих‑кода; это может быть номер заказа, номер сертификата или любой необходимый идентификатор.  
- `Code128` — тип кодирования (подробнее о выборе типа ниже).  

**Полезный совет:** Code128 может обрабатывать как цифры, так и буквы, что делает его универсальным для большинства случаев. Если нужны только цифры, `Code39` может быть проще, но Code128 предоставляет большую гибкость.

### Шаг 3: Позиционирование штрих‑кода (Как подписать PDF штрих‑кодом)
**Определение:** `SignatureOptions` предоставляет свойства макета, такие как номер страницы, размер и выравнивание.

Здесь GroupDocs действительно проявляет себя — позиционирование в процентах гарантирует, что ваш штрих‑код будет выглядеть хорошо на любом размере PDF:

```java
options.setLeft(10);   // 10% from the left edge
options.setTop(90);    // 90% from the bottom edge (near the footer)
options.setWidth(30);  // 30% of page width
options.setHeight(10); // 10% of page height
options.setPageNumber(1);
```

**Почему важны проценты:** Представьте, что вы подписываете как документы формата A4, так и формы юридического размера. При позиционировании в процентах ваш штрих‑код автоматически масштабируется и выглядит одинаково на обоих. Использование фиксированных пикселей сделает штрих‑код слишком маленьким на больших документах или слишком большим на маленьких.

**Пример из практики:** На странице A4 (595 × 842 пункта) штрих‑код шириной 30 % будет примерно 180 пунктов. На юридическом листе (612 × 1008 пунктов) он будет около 184 пунктов — автоматически пропорционально.

### Шаг 4: Подписание и сохранение документа (Как добавить штрих‑код в PDF)
Пора применить подпись и сохранить результат:

```java
signature.sign(outputPath, options);
```

**Важно:** Каталог вывода должен существовать до запуска кода. GroupDocs не создаст вложенные каталоги автоматически, поэтому создайте их заранее или обработайте это в коде:

```java
new File("output").mkdirs();
```

**Что делать, если что‑то пошло не так?** Оберните код в блок try‑catch:

```java
try {
    signature.sign("signed.pdf", options);
} catch (Exception e) {
    e.printStackTrace();
}
```

## Выбор правильного типа штрих‑кода для ваших нужд (генерация штрих‑кода Code128)
GroupDocs поддерживает несколько форматов штрих‑кодов, и выбор правильного важен. Ниже практическое сравнение:

**Code128 (Наш выбор по умолчанию):**
- **Оптимально для:** Смешанных буквенно‑цифровых данных (идентификаторы типа "INV2024-001")  
- **Вместимость:** До 128 символов ASCII  
- **Почему выигрывает:** Компактен, широко поддерживается, обрабатывает и буквы, и цифры  
- **Когда использовать:** Когда нужна гибкость и тип данных заранее неизвестен  

**Code39:**
- **Оптимально для:** Простых буквенно‑цифровых кодов  
- **Вместимость:** 43 символа (A‑Z, 0‑9 и некоторые символы)  
- **Почему стоит рассмотреть:** Старые сканеры часто поддерживают его лучше  
- **Когда использовать:** При работе с устаревшими системами или когда важна простота, а не плотность данных  

**QR Code:**
- **Оптимально для:** Больших объёмов данных (URL, JSON)  
- **Вместимость:** До 3 KB данных  
- **Почему мощный:** Может хранить сложные структуры данных, встроенная коррекция ошибок  
- **Когда использовать:** Когда нужно встроить структурированные данные или URL  

**EAN/UPC:**
- **Оптимально для:** Идентификации товаров  
- **Вместимость:** Фиксированная длина числовых кодов (8‑13 цифр)  
- **Когда использовать:** При работе с розничной торговлей или системами учёта  

**Краткое руководство по выбору:**  
- Нужны буквы и цифры? → Code128  
- Только цифры, проще? → Code39  
- Много данных или URL? → QR Code  
- Товарные/розничные коды? → EAN/UPC  

## Распространённые подводные камни и как их избежать (штрих‑код с доказательством подделки)
Вот проблемы, с которыми разработчики сталкиваются чаще всего (чтобы вам не пришлось):

### Проблема 1: Позиционирование штрих‑кода выглядит неправильно
**Симптом:** Штрих‑код появляется в неожиданных местах или обрезается.  
**Распространённые причины:**  
- Использование пиксельных значений на разных размерах страниц  
- Забывание, что координаты PDF начинаются с нижнего левого угла, а не верхнего  
- Отступы, выталкивающие содержимое за видимую область  

**Решение:** Всегда используйте позиционирование в процентах для согласованности:

```java
options.setLeft(5);
options.setTop(95);
options.setWidth(40);
options.setHeight(12);
```

### Проблема 2: Текст штрих‑кода нечитаем
**Симптом:** Закодированный текст отображается, но сканеры не могут его считать.  
**Причины:**  
- Штрих‑код слишком маленький для объёма данных  
- Неправильный тип кодирования для ваших данных  
- Низкий контраст между полосами и фоном  

**Решение:** Подбирайте размер штрих‑кода в соответствии с длиной данных. Для Code128 с 10‑15 символами стремитесь к ширине минимум 8‑10 % от ширины страницы.

### Проблема 3: Исключения, связанные с путями к файлам
**Симптом:** `FileNotFoundException` или аналогичные ошибки.  
**Причины:**  
- Жёстко закодированные пути Windows с одиночными обратными слешами  
- Каталог вывода не существует  
- Проблемы с правами доступа к файлам  

**Решение:** Используйте прямые слеши (они работают везде) и сначала создавайте каталоги:

```java
Path output = Paths.get("output/signed.pdf");
Files.createDirectories(output.getParent());
```

### Проблема 4: Проблемы с памятью при работе с большими PDF
**Симптом:** Ошибки нехватки памяти при обработке больших документов.  
**Решение:** Закрывайте объект `Signature`, когда закончите, чтобы освободить ресурсы:

```java
signature.close();
```

## Тестирование реализации штрих‑кода
Перед развертыванием убедитесь, что ваши штрих‑коды действительно работают. Ниже практический чек‑лист тестирования:

### 1. Тест визуального осмотра
Откройте подписанный PDF и проверьте:
- Виден ли штрих‑код и правильно ли он размещён?  
- Он выглядит чётко (не размытый и не пикселизированный)?  
- Есть ли достаточное пустое пространство вокруг него?

### 2. Тест сканирования
Используйте приложение‑сканер штрих‑кодов на телефоне (например, «Barcode Scanner» или «QR & Barcode Reader») для проверки:
- Сканер может считать ваш штрих‑код  
- Декодированные данные совпадают с тем, что вы закодировали  
- Он работает с разных углов и расстояний

### 3. Кроссплатформенный тест
Откройте ваш PDF на разных устройствах:
- Windows (Adobe Reader, Chrome)  
- Mac (Preview, Chrome)  
- Мобильные устройства (iOS, Android)  

Убедитесь, что штрих‑код отображается корректно везде.

### 4. Код автоматического тестирования
Вот простой тест, который вы можете выполнить:

```java
Signature testSignature = new Signature("signed.pdf");
List<BarcodeSignature> signatures = testSignature.search(BarcodeSignature.class);
if (signatures.size() > 0) {
    System.out.println("Barcode found: " + signatures.get(0).getText());
}
```

## Реальные примеры использования штрих‑код подписей
Рассмотрим, где эта техника действительно проявляет себя в производственных системах:

### 1. Генерация и проверка сертификатов
**Сценарий:** Вы создаёте обучающую платформу, выдающую сертификаты об окончании.  
**Реализация:** Сгенерируйте уникальный ID сертификата (например, "CERT‑2024‑00123") и внедрите его как штрих‑код Code128 в правый нижний угол. Сканирование штрих‑кода позволяет вашему API мгновенно получить детали сертификата, устраняя ручной ввод данных.

### 2. Системы отслеживания счетов
**Сценарий:** Ваша компания обрабатывает тысячи счетов ежемесячно.  
**Реализация:** Добавьте номер счета и дату оплаты в виде QR‑кода, расположенного так, чтобы оборудование сканирования могло легко его считать. Автоматические системы сортировки могут направлять счета без участия человека, сокращая время обработки с часов до минут.

### 3. Управление юридическими контрактами
**Сценарий:** Юридическая фирма должна отслеживать версии контрактов и их изменения.  
**Реализация:** Каждая версия контракта получает уникальный штрих‑код, включающий ID контракта, номер версии и дату подписи. Сканирование во время аудитов автоматически выводит полную историю версий.

### 4. Безопасность медицинских записей
**Сценарий:** Больница хочет предотвратить несанкционированный доступ к записям.  
**Реализация:** Внедрите в штрих‑код ID пациента и метку времени создания записи. Только аутентифицированные устройства могут декодировать и получить доступ к полной записи, а каждое сканирование создаёт журнал аудита для соответствия требованиям.

## Советы по оптимизации производительности (безопасность Java‑документов)
При подписании большого количества PDF‑ов важна производительность. Ниже несколько советов для плавной работы:

### Стратегия пакетной обработки
Вместо подписи по одному документу, подпишите их пакетно:

```java
for (String filePath : pdfList) {
    Signature batchSignature = new Signature(filePath);
    batchSignature.sign(outputPath, options);
    batchSignature.close();
}
```

**Почему это помогает:** Повторное использование объекта параметров и правильное закрытие ресурсов предотвращает утечки памяти.

### Управление памятью для больших PDF
Для PDF‑ов более 50 MB:
- Обрабатывайте их последовательно, а не загружайте несколько одновременно.  
- Используйте try‑with‑resources для гарантии очистки.  
- Следите за размером кучи и при необходимости корректируйте параметры JVM: `-Xmx2g`.

### Кеширование часто используемых штрих‑кодов
Если вы подписываете множество документов одним и тем же штрих‑кодом, кешируйте экземпляр `BarcodeSignOptions`:

```java
BarcodeSignOptions cachedOptions = new BarcodeSignOptions("STATIC_ID");
cachedOptions.setEncodeType(BarcodeEncodeType.Code128);
```

## Когда использовать штрих‑код подписи (и когда нет)
**Идеальные сценарии:**
- Вам нужны машинно‑читаемые идентификаторы документов.  
- Документы будут сканироваться или обрабатываться автоматически.  
- Вы хотите отслеживание с доказательством подделки без цифровых сертификатов.  
- Требуется интеграция с существующей инфраструктурой штрих‑кодов.  

**Не рекомендуется, когда:**
- Нужны юридически обязательные цифровые подписи (используйте цифровые сертификаты).  
- Документы будут просматриваться только людьми (может быть достаточно простого текстового водяного знака).  
- Работаете с очень небольшими документами, где штрих‑код займет большую часть страницы.  
- Требования безопасности требуют шифрования — штрих‑коды видимы и сканируемы любым.

**Можно ли комбинировать подходы?** Конечно! Многие системы используют одновременно штрих‑код подписи для отслеживания и цифровые подписи для юридической силы.

## Часто задаваемые вопросы
**В:** Можно ли использовать разные типы штрих‑кодов в одном PDF?  
**О:** Да! Вызовите `signature.sign()` несколько раз с разными `BarcodeSignOptions` для каждого типа штрих‑кода. Просто убедитесь, что они не перекрываются.

**В:** Как обрабатывать штрих‑коды, содержащие специальные символы?  
**О:** Code128 корректно работает с большинством символов ASCII. Для Unicode или сложных данных переключитесь на QR‑коды — они поддерживают кодировку UTF‑8.

**В:** Какой максимальный объём данных можно хранить в штрих‑коде Code128?  
**О:** Технически до 128 символов, но читаемость резко падает выше 30‑40 символов. Для больших объёмов используйте QR‑коды.

**В:** Увеличит ли добавление штрих‑кодов заметно размер PDF?  
**О:** Нет, штрих‑коды — векторная графика, обычно добавляют лишь 5‑20 KB на штрих‑код в зависимости от размера и сложности.

**В:** Можно ли вращать штрих‑коды или размещать их вертикально?  
**О:** Да! Используйте `options.setRotationAngle(90)` для вращения штрих‑кода, что удобно для размещения у полей.

**В:** Как сделать так, чтобы штрих‑коды появлялись на каждой странице многостраничного PDF?  
**О:** Пройдитесь по страницам и примените подпись к каждой. См. класс `PagesSetup` в документации GroupDocs для управления тем, какие страницы подписываются.

**В:** Что делать, если сканер штрих‑кода не может считать сгенерированный код?  
**О:** Сначала проверьте, поддерживает ли сканер выбранный тип штрих‑кода. Затем увеличьте размер штрих‑кода — большинство проблем вызвано слишком маленькими полосами. Стремитесь к ширине минимум 1 дюйм (2.54 см) для надёжного считывания.

## Дополнительные ресурсы
**Документация:**  
- [GroupDocs.Signature for Java Docs](https://docs.groupdocs.com/signature/java/)  
- [API Reference Guide](httpshttps://reference.groupdocs.com/signature/java/)  

**Скачивание и лицензирование:**  
- [Download Latest Version](https://releases.groupdocs.com/signature/java/)  
- [Free Trial Access](https://releases.groupdocs.com/signature/java/)  
- [Get Temporary License](https://purchase.groupdocs.com/temporary-license/)  
- [Purchase Full License](https://purchase.groupdocs.com/buy)  

**Сообщество и поддержка:**  
- [Support Forum](https://forum.groupdocs.com/c/signature/) - Active community with GroupDocs engineers  

**Последнее обновление:** 2026-07-20  
**Тестировано с:** GroupDocs.Signature 23.12 (Java)  
**Автор:** GroupDocs  

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

```java
import com.groupdocs.signature.Signature;

public class QuickTest {
    public static void main(String[] args) {
        try {
            Signature signature = new Signature("test-document.pdf");
            System.out.println("GroupDocs.Signature is ready to go!");
        } catch (Exception e) {
            System.err.println("Setup issue: " + e.getMessage());
        }
    }
}
```

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
Signature signature = new Signature(filePath);
```

```java
import com.groupdocs.signature.options.sign.BarcodeSignOptions;
import com.groupdocs.signature.domain.barcodes.BarcodeTypes;

BarcodeSignOptions options = new BarcodeSignOptions("12345678");
options.setEncodeType(BarcodeTypes.Code128);
```

```java
import com.groupdocs.signature.domain.enums.MeasureType;
import com.groupdocs.signature.domain.Padding;

// Use percentages instead of fixed pixels
options.setLocationMeasureType(MeasureType.Percents);
options.setLeft(5);  // 5% from the left edge
options.setTop(5);   // 5% from the top

// Size it proportionally too
options.setSizeMeasureType(MeasureType.Percents);
options.setWidth(10);  // 10% of page width
options.setHeight(5);  // 5% of page height

// Add some breathing room with margins
Padding margins = new Padding();
margins.setLeft(1);
margins.setTop(1);
margins.setRight(1);
options.setMargin(margins);
```

```java
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithPercents/sample_signed.pdf";
signature.sign(outputFilePath, options);
```

```java
Path outputPath = Paths.get(outputFilePath);
Files.createDirectories(outputPath.getParent());
signature.sign(outputFilePath, options);
```

```java
try {
    signature.sign(outputFilePath, options);
    System.out.println("PDF signed successfully at: " + outputFilePath);
} catch (Exception e) {
    System.err.println("Signing failed: " + e.getMessage());
    e.printStackTrace();
}
```

```java
options.setLocationMeasureType(MeasureType.Percents);
options.setLeft(5);  // 5% from left works on any page width
```

```java
options.setWidth(10);  // Give it room to breathe
options.setHeight(5);  // Maintain proper aspect ratio
```

```java
String filePath = "documents/sample.pdf";  // Works on Windows, Mac, Linux
Files.createDirectories(Paths.get("output/signed"));
```

```java
try (Signature signature = new Signature(filePath)) {
    signature.sign(outputFilePath, options);
} // Automatically closes and releases memory
```

```java
import org.junit.Test;
import static org.junit.Assert.*;

public class BarcodeSignatureTest {
    
    @Test
    public void testBarcodeSigning() {
        String testPdf = "test-data/sample.pdf";
        String output = "test-output/signed.pdf";
        
        try (Signature signature = new Signature(testPdf)) {
            BarcodeSignOptions options = new BarcodeSignOptions("TEST123");
            options.setEncodeType(BarcodeTypes.Code128);
            
            signature.sign(output, options);
            
            // Verify output file exists
            assertTrue(new File(output).exists());
            
            // Verify file size increased (signature was added)
            long originalSize = new File(testPdf).length();
            long signedSize = new File(output).length();
            assertTrue(signedSize > originalSize);
            
        } catch (Exception e) {
            fail("Signing should not throw exception: " + e.getMessage());
        }
    }
}
```

```java
List<String> pdfFiles = Arrays.asList("doc1.pdf", "doc2.pdf", "doc3.pdf");

for (String pdfFile : pdfFiles) {
    try (Signature signature = new Signature(pdfFile)) {
        BarcodeSignOptions options = createBarcodeOptions(); // Reuse options
        signature.sign(getOutputPath(pdfFile), options);
    }
}
```

```java
// Create options once, reuse many times
BarcodeSignOptions templateOptions = createStandardBarcodeOptions();

// For each document, clone and customize
BarcodeSignOptions documentOptions = templateOptions.clone();
documentOptions.setText(uniqueDocumentId);
```

## Похожие руководства
- [Java Barcode Signature Tutorial - Add, Verify & Manage Barcodes in PDFs](/signature/java/barcode-signatures/)  
- [Create Barcode Signature in Java – Update PDF Barcodes](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)  
- [How to read QR code PDF using Java and GroupDocs.Signature](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)