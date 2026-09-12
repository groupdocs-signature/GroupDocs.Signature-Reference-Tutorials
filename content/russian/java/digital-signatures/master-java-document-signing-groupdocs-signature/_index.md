---
categories:
- Java Development
- Document Management
date: '2026-08-25'
description: Узнайте, как добавить barcode в PDF‑документы на Java с помощью GroupDocs.Signature.
  Это пошаговое руководство показывает, как добавить barcode GS1DotCode, извлекать
  изображения и избегать распространённых ошибок.
keywords:
- how to add barcode
- groupdocs signature java
- pdf document barcode
lastmod: '2026-08-25'
linktitle: Добавить barcode в PDF на Java
og_description: Узнайте, как добавить barcode в PDF на Java с помощью GroupDocs.Signature.
  Пошаговое руководство, примеры кода и советы по устранению неполадок для barcode
  GS1DotCode.
og_image_alt: Guide showing Java code to embed GS1DotCode barcode into a PDF using
  GroupDocs.Signature
og_title: Как добавить barcode в PDF на Java – Полное руководство
schemas:
- author: GroupDocs
  dateModified: '2026-08-25'
  description: Learn how to add barcode to PDF documents in Java using GroupDocs.Signature.
    This step‑by‑step guide shows how to add GS1DotCode barcodes, extract images,
    and avoid common pitfalls.
  headline: How to Add Barcode to PDF in Java
  type: TechArticle
- description: Learn how to add barcode to PDF documents in Java using GroupDocs.Signature.
    This step‑by‑step guide shows how to add GS1DotCode barcodes, extract images,
    and avoid common pitfalls.
  name: How to Add Barcode to PDF in Java
  steps:
  - name: Validate GS1 payloads before encoding.
    text: Validate GS1 payloads before encoding.
  - name: Choose barcode dimensions that balance scan reliability with layout constraints.
    text: Choose barcode dimensions that balance scan reliability with layout constraints.
  - name: Combine barcode signatures with cryptographic signatures for full security
      coverage.
    text: Combine barcode signatures with cryptographic signatures for full security
      coverage.
  type: HowTo
- questions:
  - answer: GS1DotCode is a compact 2‑D dot matrix that stores up to **3,116 characters**
      in a smaller footprint than QR codes, making it ideal for tiny labels and high‑speed
      printing.
    question: What is GS1DotCode and why is it different from QR codes?
  - answer: The free trial is limited to evaluation and adds a watermark to output
      files. Production use requires a purchased or temporary 30‑day license.
    question: Can I use a free trial for production deployments?
  - answer: Set `setPageNumber(pageIndex)` on the `BarcodeSignOptions` object, then
      adjust `setLeft()` and `setTop()` to place it precisely.
    question: How do I position the barcode on a specific page?
  - answer: 'Yes. Provide the password when constructing the `Signature` object: `new
      Signature("file.pdf", "password")`.'
    question: Does GroupDocs.Signature support password‑protected PDFs?
  - answer: Aim for at least **108 pt × 108 pt** (1.5 in × 1.5 in). Larger sizes improve
      readability, especially on low‑resolution printers.
    question: What is the minimum barcode size for reliable scanning?
  type: FAQPage
tags:
- java
- pdf-signing
- barcodes
- groupdocs
- document-security
title: Как добавить barcode в PDF на Java
type: docs
url: /ru/java/digital-signatures/master-java-document-signing-groupdocs-signature/
weight: 1
---

# Как добавить штрих‑код в PDF на Java

## Введение

Когда‑то вам приходилось бороться с подлинностью документов в вашем Java‑приложении? Вы не одиноки. Будь то система учёта запасов, управление контрактами или обработка документов цепочки поставок, с большой вероятностью вам понадобится надёжный способ автоматически подписывать и проверять PDF‑файлы.

Традиционные цифровые подписи хороши, но иногда требуется нечто более специализированное — например, подписи‑штрих‑коды, которые без проблем работают со сканирующими системами и автоматизированными рабочими процессами. Здесь на помощь приходят штрих‑коды GS1DotCode.

**Что вы узнаете:**
- Как подписывать PDF‑документы штрих‑кодами GS1DotCode в Java
- Как извлекать и сохранять изображения подписи‑штрих‑кода
- Когда (и почему) использовать подписи‑штрих‑коды вместо традиционных методов
- Распространённые подводные камни и как их избежать

К концу этого руководства у вас будет готовое решение, которое можно интегрировать в любой Java‑проект.

## Быстрые ответы
- **Какая библиотека добавляет штрих‑коды в PDF на Java?** GroupDocs.Signature for Java.  
- **Какой формат штрих‑кода покрывается?** GS1DotCode, компактная 2‑D матрица точек.  
- **Нужна ли платная лицензия?** Бесплатная пробная версия подходит для тестирования; для продакшна требуется коммерческая лицензия.  
- **Можно ли извлечь штрих‑код как изображение?** Да, используя API `BarcodeSignature`.  
- **Какая версия Java требуется?** JDK 8 или выше.

## Что такое добавление штрих‑кода?
*Добавление штрих‑кода* относится к процессу программного встраивания графического изображения машинно‑читаемого штрих‑кода в PDF‑файл так, чтобы штрих‑код стал частью потока содержимого документа. Это включает генерацию изображения штрих‑кода, позиционирование его на странице и сохранение изменённого PDF, обеспечивая возможность поиска и печати штрих‑кода.

## Почему выбирают штрих‑коды GS1DotCode?
GS1DotCode разработан для ситуаций, когда пространство ограничено. В отличие от линейных штрих‑кодов, растягивающихся по горизонтали, DotCode создаёт 2‑D матрицу точек, упаковывающую огромный объём информации в небольшую площадь. Это делает его идеальным для:

- **Маленьких этикеток продукции**, где каждый миллиметр на счету  
- **Высокоскоростной печати** на производственных линиях (формат специально для этого)  
- **Отслеживания в цепочке поставок**, где необходимо кодировать сложные структуры данных  

Формат может вместить до **3 116 символов** в компактном пространстве и надёжно читается даже при высокой скорости сканирования или частичном повреждении. Если вы работаете в рознице или логистике, ваши партнёры, скорее всего, уже используют стандарты GS1 — так что вы говорите на одном языке.

> **Pro tip:** Используйте GS1DotCode, когда нужно разместить более 20 символов на этикетке размером менее 1 дюйм × 1 дюйм.

## Предварительные требования

Прежде чем приступить к кодированию, убедитесь, что ваша среда удовлетворяет следующим требованиям.

### Требуемые библиотеки и зависимости
- **GroupDocs.Signature for Java** 23.12 или новее (поддерживает **30+** форматов документов)  
- Maven или Gradle для управления зависимостями

### Настройка окружения
- **JDK 8** или новее, установленный и добавленный в `PATH`  
- IDE, например IntelliJ IDEA, Eclipse или NetBeans  
- Пример PDF‑файла для экспериментов (любой незащищённый PDF подойдёт)

### Необходимые знания
- Базовый синтаксис Java (переменные, методы, объекты)  
- Знакомство с объявлением зависимостей в Maven или Gradle  
- Понимание работы с файловым вводом/выводом в Java (например, `FileInputStream`)

Если чего‑то из перечисленного не хватает, приостановите работу и установите недостающие компоненты; последующие шаги предполагают их наличие.

## Настройка GroupDocs.Signature for Java

### Maven
Если вы используете Maven, добавьте следующую зависимость в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

Maven автоматически скачает библиотеку и все необходимые транзитивные зависимости.

### Gradle
Для пользователей Gradle вставьте эту строку в ваш файл `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

Gradle разрешит пакет тем же «hands‑off» способом.

### Прямое скачивание
Если вы предпочитаете ручное управление, скачайте JAR‑файлы со страницы официальных релизов: [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/). Поместите JAR‑ы в classpath вашего проекта.

**Pro tip:** Maven или Gradle упрощают будущие обновления — достаточно увеличить номер версии.

### Приобретение лицензии
GroupDocs предлагает три варианта лицензирования:

- **Бесплатная пробная** — без кредитной карты, на выводимых файлах есть водяные знаки  
- **Временная лицензия** — 30‑дневная полная оценка функций  
- **Коммерческая лицензия** — убирает ограничения пробной версии и предоставляет права на продакшн

После получения файла лицензии разместите его в папке ресурсов вашего проекта и загрузите перед созданием любого объекта `Signature`.

`License.setLicense` загружает файл лицензии GroupDocs, включая полные возможности без ограничений пробной версии.

Запустите следующий фрагмент, чтобы убедиться, что библиотека загружается корректно:

```java
import com.groupdocs.signature.Signature;

public class InitializeGroupDocs {
    public static void main(String[] args) {
        // Create an instance of Signature
        Signature signature = new Signature("path/to/your/document.pdf");
        
        System.out.println("Initialization successful!");
    }
}
```

Если вы видите «Initialization successful!», настройка завершена. В противном случае проверьте classpath и путь к лицензии.

## Руководство по реализации

Мы рассмотрим две основные функции: (1) подпись PDF штрих‑кодом GS1DotCode и (2) извлечение этого штрих‑кода в виде файла‑изображения.

### Функция 1: подпись документа штрих‑кодом GS1DotCode

#### Как подписать PDF штрих‑кодом GS1DotCode в Java?

Загрузите целевой PDF с помощью `new Signature("source.pdf")`, сконфигурируйте объект `BarcodeSignOptions` с данными в формате GS1 и вызовите `sign()`, чтобы получить новый PDF с внедрённым штрих‑кодом. Эта операция записывает штрих‑код непосредственно в поток содержимого PDF, сохраняя его при печати и повторном сканировании.

Процесс состоит из трёх коротких шагов: создать экземпляр `Signature`, настроить `BarcodeSignOptions` и вызвать `sign()`. Ниже показан код, демонстрирующий каждый шаг.

##### 1. инициализировать объект подписи
Класс `Signature` — точка входа для всех операций обработки документов в GroupDocs.Signature.

```java
import com.groupdocs.signature.Signature;

String sourceFilePath = "YOUR_DOCUMENT_DIRECTORY/document.pdf";
final Signature signature = new Signature(sourceFilePath);
```

> **Why this matters:** The `Signature` object abstracts file handling, streaming large PDFs efficiently without loading the entire file into memory.

##### 2. настроить параметры штрих‑кода
`BarcodeSignOptions` позволяет задать тип штрих‑кода, кодируемые данные, позицию и размеры.

```java
import com.groupdocs.signature.domain.signatures.BarcodeSignature;
import com.groupdocs.signature.options.sign.BarcodeSignOptions;
import com.groupdocs.signature.domain.barcodes.BarcodeTypes;

BarcodeSignOptions gs1DotCodeOptions = new BarcodeSignOptions("(01)04912345123459(15)970331(30)128(10)ABC123", BarcodeTypes.GS1DotCode);
gs1DotCodeOptions.setLeft(100); // Set barcode position
gs1DotCodeOptions.setTop(100);
gs1DotCodeOptions.setHeight(150);
gs1DotCodeOptions.setWidth(200);
```

> **Key points:**  
> - The encoded string follows GS1 Application Identifiers (AIs) such as `(01)` for GTIN, `(15)` for expiration date, etc.  
> - `setLeft()` and `setTop()` use points (72 pts = 1 in).  
> - Minimum recommended size for reliable scanning is **108 pt × 108 pt** (1.5 in × 1.5 in).

##### 3. подписать документ
Добавьте сконфигурированные параметры в список (можно комбинировать несколько типов подписи) и вызовите `sign()`.

```java
import java.util.ArrayList;
import java.util.List;

List<com.groupdocs.signature.options.sign.SignOptions> listOptions = new ArrayList<>();
listOptions.add(gs1DotCodeOptions);
signature.sign("YOUR_OUTPUT_DIRECTORY/signed_document_with_gs1dotcode.pdf", listOptions);
```

> **Performance note:** Re‑using a single `Signature` instance for batch operations reduces object‑creation overhead and improves throughput.

### Функция 2: сохранить содержимое подписи‑штрих‑кода в файл

#### Как извлечь изображение штрих‑кода из подписанного PDF в Java?

`BarcodeSignature` представляет объект подписи‑штрих‑кода, извлечённый из подписанного документа, предоставляя доступ к его данным и изображению.

Создайте экземпляр `BarcodeSignature` (или получите его через `search()`), прочитайте его Base64‑закодированные данные изображения через `getContent()`, декодируйте их и запишите байты в PNG‑файл. Это даст отдельное изображение, которое можно отобразить в UI или отправить на принтер этикеток.

##### 1. имитировать создание подписи‑штрих‑кода
В реальных сценариях вы бы получили `BarcodeSignature` из результата поиска; здесь мы создаём его вручную для иллюстрации.

```java
import com.groupdocs.signature.domain.signatures.BarcodeSignature;
import java.io.FileOutputStream;

String base64String = "SampleBase64EncodedData";
BarcodeSignature barcodeSignature = new BarcodeSignature(base64String);
```

##### 2. сохранить содержимое в файл
Декодируйте строку Base64 и запишите полученные байты на диск, используя блок try‑with‑resources.

```java
int imageNumber = 1;
String formatExtension = ".png";  // Assume PNG format

try (FileOutputStream outputStream = new FileOutputStream("YOUR_OUTPUT_DIRECTORY/barcode_image" + imageNumber + formatExtension)) {
    byte[] byteArray = barcodeSignature.getContent();
    if (byteArray != null) {
        outputStream.write(byteArray);
    }
}
```

> **Gotcha:** `getContent()` may return `null` if the signature was created without embedding an image. Always check for `null` before writing.

## Распространённые проблемы и их решения

### Проблема: штрих‑код не сканируется
**Симптомы:** Штрих‑код выглядит нормально в просмотрщике PDF, но сканеры выдают ошибки.

**Решения:**
- Увеличьте размер штрих‑кода минимум до **108 pt × 108 pt**.  
- Убедитесь, что разрешение принтера **≥ 300 dpi**.  
- Проверьте, что строка данных GS1 соответствует правильному синтаксису AI; отсутствие скобки ломает сканер.

### Проблема: OutOfMemoryError при работе с большими PDF
**Симптомы:** Обработка документов более **50 MB** приводит к ошибкам нехватки памяти.

**Решения:**
- Запустите JVM с большим объёмом кучи, например `-Xmx2g`.  
- Обрабатывайте документы небольшими партиями.  
- Явно освобождайте объекты `Signature`: `signature.dispose()` после каждого файла.

### Проблема: штрих‑код выглядит размытым
**Симптомы:** В результирующем PDF штрих‑код пикселизирован.

**Решения:**
- Используйте большие размеры; библиотека рендерит векторную графику, когда это возможно, но уменьшение после генерации приводит к артефактам.  
- Избегайте преобразования растровой графики в векторную; позвольте GroupDocs рендерить напрямую из векторного определения.

### Проблема: исключения лицензии
**Симптомы:** Ошибки типа «License not found» или «Trial limitations exceeded».

**Решения:**
- Поместите файл лицензии в корень classpath (`src/main/resources`).  
- Вызовите `License.setLicense("GroupDocs.Signature.lic")` **до** создания любого объекта `Signature`.  
- Для временных лицензий проверьте дату истечения (30 дней с момента выдачи).

## Когда использовать этот подход

### Хорошие сценарии применения
- **Отслеживание в цепочке поставок** — встраивание идентификаторов продукции, номеров партий и сроков годности непосредственно в транспортные документы.  
- **Автоматическая печать этикеток** — генерация штрих‑кодов «на лету» для каждого PDF‑счёта.  
- **Регулируемые отрасли** — стандарты GS1 обязательны во многих розничных и медицинских сферах.  

### Когда рассматривать альтернативы
- Если нужна только криптографическая целостность, стандартная PKI‑подпись более уместна.  
- Для простых визуальных аннотаций может хватить текстовой подписи или штампа‑изображения.  
- Когда размер документа критичен, избегайте добавления высокоразрешённых изображений штрих‑кода; вместо этого используйте QR‑коды, которые могут быть меньше при сопоставимой плотности данных.

## Лучшие практики безопасности

### Проверка данных
Очистите любые пользовательские данные перед их кодированием в штрих‑код. Некорректные строки GS1 могут вызвать ошибки сканирования или, в худшем случае, переполнение буфера в устаревшем программном обеспечении сканеров.

### Управление доступом
Внедрите ролевую модель доступа (RBAC), чтобы только уполномоченные пользователи могли вызывать API подписи. Храните файл лицензии в безопасном месте и ограничьте права доступа к файловой системе.

### Аудит‑логирование
Записывайте каждую операцию подписи с деталями: идентификатор пользователя, метка времени, путь к исходному файлу и точный GS1‑полезный груз. Пример фрагмента логирования:

```java
// Simple logging example (use a proper logging framework in production)
System.out.println("Document signed by: " + userId + " at " + new Date());
System.out.println("Barcode data: " + barcodeData);
```

### Обнаружение подделки
Сочетайте подпись‑штрих‑код с криптографической цифровой подписью. Штрих‑код предоставляет машинно‑читаемые данные, а цифровая подпись гарантирует целостность и невозможность отказа.

## Практические применения

### 1. Управление цепочкой поставок
Каждая упаковочная накладная получает штрих‑код GS1DotCode, кодирующий GTIN, партию и пункт назначения. Сканеры на каждом пункте автоматически обновляют ERP‑систему, снижая ручной ввод ошибок на **98 %**.

### 2. Контроль запасов
При поступлении товаров PDF‑документ подписывается штрих‑кодом, содержащим номер заказа и количество позиций. Сотрудники склада сканируют штрих‑код, и база данных запасов обновляется в реальном времени.

### 3. Точка продаж в рознице
Счета, распечатанные со штрих‑кодом, позволяют кассирам обрабатывать возвраты, просто сканируя счёт вместо ручного ввода ID транзакции, сокращая среднее время обслуживания на **30 секунд** за возврат.

### 4. Медицинская документация
Рецепты, подписанные штрих‑кодом GS1DotCode, включают идентификатор пациента, код лекарства и инструкцию дозировки. Аптеки сканируют штрих‑код, устраняя ошибки транскрипции, которые могут привести к неблагоприятным лекарственным событиям.

## Соображения по производительности

### Управление памятью
GroupDocs.Signature потоково обрабатывает PDF‑данные, но всё равно следует своевременно закрывать ресурсы:

```java
try (Signature signature = new Signature(sourceFilePath)) {
    // Do your signing operations here
} // Signature automatically disposed here
```

Использование try‑with‑resources гарантирует, что объект `Signature` освободит файловые дескрипторы даже при возникновении исключения.

### Советы по пакетной обработке
- Переиспользуйте один экземпляр `BarcodeSignOptions`, если полезная нагрузка одинаковая для множества документов.  
- Параллелизуйте подпись с помощью `ExecutorService` для CPU‑интенсивных задач; типичный 8‑ядерный сервер может подписать **≈ 150 PDF‑файлов в минуту**, если каждый файл менее 5 MB.  
- Ограничьте внешние вызовы проверки лицензии, чтобы избежать ограничения скорости (rate‑limit).

### Оптимизация формата файла
- Предпочитайте PDF/A‑1b для архивирования; он сжимает потоки и уменьшает размер файла до **40 %**.  
- Держите размеры штрих‑кода не больше необходимого; штрих‑код 1.5 in × 1.5 in добавляет примерно **15 KB** к PDF размером 2 MB.

## Заключение

Теперь у вас есть полностью готовый к продакшну рабочий процесс добавления штрих‑кодов GS1DotCode в PDF‑файлы на Java, извлечения этих штрих‑кодов как изображений и интеграции процесса в более крупные конвейеры управления документами. Не забывайте:

1. Проверять GS1‑полезные нагрузки перед кодированием.  
2. Выбирать размеры штрих‑кода, балансируя надёжность сканирования и ограничения макета.  
3. Комбинировать подписи‑штрих‑коды с криптографическими подписями для полной защиты.

Следующие шаги: изучить другие типы подписей, предлагаемые GroupDocs.Signature — QR‑коды, текстовые штампы и цифровые сертификаты, все они используют единый API.

---

## Часто задаваемые вопросы

**В: Что такое GS1DotCode и чем он отличается от QR‑кодов?**  
О: GS1DotCode — компактная 2‑D матрица точек, способная хранить до **3 116 символов** в меньшем пространстве, чем QR‑коды, что делает её идеальной для крошечных этикеток и высокоскоростной печати.

**В: Можно ли использовать бесплатную пробную версию в продакшн‑развёртываниях?**  
О: Пробная версия ограничена оценкой и добавляет водяные знаки в выходные файлы. Для продакшна требуется приобретённая или временная 30‑дневная лицензия.

**В: Как позиционировать штрих‑код на конкретной странице?**  
О: Установите `setPageNumber(pageIndex)` в объекте `BarcodeSignOptions`, затем скорректируйте `setLeft()` и `setTop()` для точного размещения.

**В: Поддерживает ли GroupDocs.Signature PDF‑файлы, защищённые паролем?**  
О: Да. Передайте пароль при создании объекта `Signature`: `new Signature("file.pdf", "password")`.

**В: Как проверить, что подпись‑штрих‑код была добавлена корректно?**  
`Signature.search()` ищет подписи в документе, возвращая коллекцию соответствующих объектов подписи. Используйте `Signature.search()` с `BarcodeSearchOptions`. Возвращённые объекты `BarcodeSignature` содержат закодированные данные и изображение для проверки.

**В: Какой минимальный размер штрих‑кода для надёжного сканирования?**  
О: Рекомендуется минимум **108 pt × 108 pt** (1.5 in × 1.5 in). Большие размеры повышают читаемость, особенно на принтерах с низким разрешением.

**В: Можно ли подписывать несколько PDF‑файлов одновременно?**  
О: Да. Создайте пул потоков и отдельный объект `Signature` для каждого потока; библиотека потокобезопасна, если каждый поток работает со своим документом.

**В: Есть ли ограничение на количество штрих‑кодов, которые можно встроить в один PDF?**  
О: Жёсткого ограничения нет, но каждый штрих‑код добавляет примерно **15 KB** данных. Для PDF более **100 MB** рекомендуется пакетная обработка для управления потреблением памяти.

**В: Работает ли библиотека на платформах, отличных от Windows?**  
О: GroupDocs.Signature for Java платформенно‑независима и работает на любой ОС с совместимой JRE, включая Linux и macOS.

---

**Последнее обновление:** 2026-08-25  
**Тестировано с:** GroupDocs.Signature 23.12 for Java  
**Автор:** GroupDocs

## Похожие руководства

- [Как проверить подписи‑штрих‑коды в Java с помощью GroupDocs.Signature](/signature/java/barcode-signatures/verify-barcode-signatures-groupdocs-signature-java/)  
- [Создание подписи‑штрих‑кода Java – обновление PDF‑штрих‑кодов](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)  
- [Добавление QR‑кода в PDF Java — полное руководство с GroupDocs.Signature](/signature/java/qr-code-signatures/qr-code-signatures-java-groupdocs/)