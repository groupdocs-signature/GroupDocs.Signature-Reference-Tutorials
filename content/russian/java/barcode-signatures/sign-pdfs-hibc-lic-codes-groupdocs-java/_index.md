---
categories:
- Document Signing
- Healthcare Integration
date: '2026-05-16'
description: Узнайте, как создать data matrix PDF и добавить QR code PDF с помощью
  GroupDocs.Signature for Java. Пошаговое руководство по подписанию медицинских документов.
keywords:
- create data matrix pdf
- add qr code pdf
- HIBC barcode Java
lastmod: '2026-05-16'
linktitle: Руководство по HIBC PDF Signing Java
schemas:
- author: GroupDocs
  dateModified: '2026-05-16'
  description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  headline: Create Data Matrix PDF with HIBC Barcode in Java
  type: TechArticle
- description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  name: Create Data Matrix PDF with HIBC Barcode in Java
  steps:
  - name: '**Import the required classes** – these give you access to the signature
      engine and Data Matrix options.'
    text: '**Import the required classes** – these give you access to the signature
      engine and Data Matrix options.'
  - name: '**Instantiate the `Signature` object** with absolute paths for source and
      destination files.'
    text: '**Instantiate the `Signature` object** with absolute paths for source and
      destination files.'
  - name: '**Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`,
      and define placement coordinates. `QrCodeTypes` enumerates the supported barcode
      formats for HIBC signatures.'
    text: '**Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`,
      and define placement coordinates. `QrCodeTypes` enumerates the supported barcode
      formats for HIBC signatures.'
  - name: '**Apply the signature** to the PDF.'
    text: '**Apply the signature** to the PDF.'
  - name: '**Dispose of resources** to free file handles and avoid memory leaks.'
    text: '**Dispose of resources** to free file handles and avoid memory leaks.'
  - name: '**Import QR‑specific classes**'
    text: '**Import QR‑specific classes**'
  - name: '**Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.'
    text: '**Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.'
  - name: '**Sign the document**'
    text: '**Sign the document**'
  type: HowTo
- questions:
  - answer: Yes, it also supports DOCX, XLSX, PPTX, PNG, JPEG, and TIFF with the same
      barcode‑signing API.
    question: Can GroupDocs.Signature sign file types other than PDF?
  - answer: Verify that your HIBC string follows the exact HIBCC syntax, use the online
      validator, and ensure you’re using the correct `QrCodeTypes` constant for the
      chosen format.
    question: How do I troubleshoot “Invalid barcode content” errors?
  - answer: QR ≈ 4,296 alphanumeric characters, Aztec ≈ 3,832 numeric / 3,067 alphanumeric,
      Data Matrix ≈ 3,116 numeric / 2,335 alphanumeric. Keep codes under 200 characters
      for optimal scan reliability.
    question: What is the maximum data capacity for each HIBC format?
  - answer: Absolutely. Create separate `QrCodeSignOptions` objects with different
      positions and call `signature.sign()` for each. Just ensure they don’t overlap.
    question: Is it possible to embed multiple barcode types in one PDF?
  - answer: No. After the JAR is on the classpath and the license is activated, all
      operations are performed locally.
    question: Do I need an internet connection for signing at runtime?
  type: FAQPage
tags:
- java
- pdf-signing
- hibc
- healthcare
- barcode
- pharmaceutical
title: Создать Data Matrix PDF с HIBC Barcode в Java
type: docs
url: /ru/java/barcode-signatures/sign-pdfs-hibc-lic-codes-groupdocs-java/
weight: 1
---

# Создать PDF с Data Matrix и штрих‑кодом HIBC на Java

Если вы разрабатываете программное обеспечение для фармацевтической или медицинской логистики, вы, вероятно, столкнулись со стеной бумажного отслеживания, потерянными подписями и кошмарами аудитов. **Создание PDF с Data Matrix**, в котором встроен штрих‑код HIBC LIC, решает эти проблемы, предоставляя вам защищённый от подделки, машинно‑читаемый след, который выдерживает печать, сканирование и регуляторный контроль. В этом руководстве вы увидите, как именно **добавить поддержку QR‑кода в PDF**, а также форматы Aztec и Data Matrix, используя GroupDocs.Signature для Java.

## Быстрые ответы
- **Какая библиотека обрабатывает штрих‑коды HIBC в Java?** GroupDocs.Signature for Java.  
- **Какой формат штрих‑кода самый компактный?** Data Matrix — идеален для небольших этикеток.  
- **Можно ли добавить и QR, и Data Matrix в один PDF?** Да, просто создайте отдельные `QrCodeSignOptions`.  
- **Нужен ли интернет при выполнении?** Нет, библиотека полностью работает офлайн после установки.  
- **Какая версия Java рекомендуется?** Java 11+ для производительности уровня продакшн.

## Что такое подпись PDF штрих‑кодом HIBC?
Класс `Signature` в GroupDocs.Signature для Java представляет PDF‑документ и предоставляет методы для встраивания штрих‑кодов HIBC в виде цифровых подписей. Подписывая PDF штрих‑кодом HIBC, вы создаёте проверяемую, защищённую от подделки запись, которую можно сканировать в любой точке цепочки поставок.

## Почему использовать Data Matrix и QR‑коды вместе?
GroupDocs.Signature поддерживает **более 50 форматов ввода и вывода** и может обрабатывать PDF‑файлы со сотнями страниц без загрузки всего файла в память. Использование Data Matrix для плотных, небольших этикеток и QR для более просторных документов обеспечивает оптимальный баланс читаемости, ёмкости данных (до 4 296 символов для QR) и эффективности использования печатного пространства.

## Предварительные требования
- **JDK 11 или выше** (Java 8 работает, но рекомендуется Java 11+ для оптимальной производительности).  
- **IDE**, например IntelliJ IDEA, Eclipse или VS Code с Java‑расширениями.  
- **Maven или Gradle** для управления зависимостями (примеры ниже).  
- **Пример PDF** (например, `sample.pdf`) для тестирования реализации.  
- **Действующая лицензия GroupDocs.Signature** (бесплатная пробная версия для разработки, платная лицензия для продакшн).

## Настройка GroupDocs.Signature для Java

### Конфигурация Maven
Добавьте зависимость в ваш `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Конфигурация Gradle
Для проектов Gradle добавьте следующее в ваш `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Вариант прямой загрузки
Вы также можете загрузить JAR‑файл напрямую с [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) и вручную добавить его в classpath вашего проекта. Этот подход хорошо работает в средах с ограниченным доступом к сети.

### Получение лицензии
Запросите бесплатную пробную или временную лицензию у GroupDocs, чтобы убрать водяные знаки и разблокировать все функции. Для продакшн‑развёртываний требуется приобретённая лицензия.

### Базовая инициализация
Класс `Signature` является точкой входа для всех операций подписи. Он загружает PDF, применяет штрих‑код и записывает подписанный файл.

```java
import com.groupdocs.signature.Signature;

class InitializeSignature {
    public static void main(String[] args) {
        Signature signature = new Signature("sample.pdf");
        // Proceed with signing operations...
    }
}
```

## Как создать PDF с Data Matrix и штрих‑кодом HIBC?
Загрузите ваш исходный PDF, настройте объект `QrCodeSignOptions` для формата Data Matrix и вызовите `sign()` — это всё, что нужно для встраивания соответствующего штрих‑кода HIBC Data Matrix. Ниже приведены шаги с точным кодом. `QrCodeSignOptions` определяет параметры подписи штрих‑кода, такие как тип, содержимое, размер и позиция.

1. **Импортировать необходимые классы** — они дают доступ к движку подписи и параметрам Data Matrix.  

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
```

2. **Создать объект `Signature`** с абсолютными путями к исходному и целевому файлам.  

```java
String sourceFilePath = "YOUR_DOCUMENT_DIRECTORY";
String destinFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithHIBCLICQR.pdf";

final Signature signature = new Signature(sourceFilePath);
```

3. **Настроить параметры Data Matrix** — задать строку HIBC, выбрать `QrCodeTypes.HIBCLICDataMatrix` и определить координаты размещения. `QrCodeTypes` перечисляет поддерживаемые форматы штрих‑кодов для подписей HIBC.  

```java
QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR);
hibcLic_QR.setLeft(1); // Set the position from left
hibcLic_QR.setTop(1);   // Set the position from top
hibcLic_QR.setReturnContent(true); // Return content after signing
hibcLic_QR.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

4. **Применить подпись** к PDF.  

```java
signature.sign(destinFilePath, hibcLic_QR);
```

5. **Освободить ресурсы**, чтобы закрыть файловые дескрипторы и избежать утечек памяти.  

```java
finally {
    if (signature != null) signature.dispose();
}
```

### Полный рабочий пример
Вот полный процесс в одном блоке (заполнители представляют точный код, который вы вставите из предыдущих фрагментов):

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;

public class HibcQrSigning {
    public static void main(String[] args) {
        String sourceFilePath = "sample.pdf";
        String destinFilePath = "output/SignWithHIBCLICQR.pdf";
        
        Signature signature = null;
        try {
            signature = new Signature(sourceFilePath);
            
            QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions(
                "A123PROD30917/75#422011907#GP293", 
                QrCodeTypes.HIBCLICQR
            );
            hibcLic_QR.setLeft(1);
            hibcLic_QR.setTop(1);
            hibcLic_QR.setReturnContent(true);
            hibcLic_QR.setReturnContentType(FileType.PNG);
            
            signature.sign(destinFilePath, hibcLic_QR);
            System.out.println("PDF signed successfully with HIBC QR code");
            
        } catch (Exception e) {
            System.err.println("Error signing PDF: " + e.getMessage());
            e.printStackTrace();
        } finally {
            if (signature != null) signature.dispose();
        }
    }
}
```

#### Прямой ответ (40–70 слов)
Чтобы **создать PDF с Data Matrix**, создайте объект `Signature` с вашим исходным PDF, задайте `QrCodeSignOptions` как `QrCodeTypes.HIBCLICDataMatrix` и укажите правильно отформатированную строку HIBC, затем вызовите `signature.sign(outputPath, options)`. Библиотека записывает подписанный PDF в указанный путь, сохраняет макет и встраивает штрих‑код как защищённую от подделки подпись.

## Как добавить QR‑код в PDF с помощью GroupDocs.Signature?
Загрузите PDF, настройте `QrCodeSignOptions` для формата QR и вызовите `sign()`. Этот двухстрочный шаблон работает с PDF любого размера и автоматически масштабирует изображение QR для оптимальной читаемости. `QrCodeSignOptions` конфигурирует подпись штрих‑кода QR, включая его содержимое и визуальные свойства. Он позиционирует код согласно заданным координатам, гарантируя отсутствие наложения на существующее содержимое и сохраняет возможность сканирования после печати.

1. **Импортировать классы, специфичные для QR**  

```java
QrCodeSignOptions hibcLic_AZ = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec);
hibcLic_AZ.setLeft(1); // Set the position from left
hibcLic_AZ.setTop(200); // Set the position from top
hibcLic_AZ.setReturnContent(true); // Return content after signing
hibcLic_AZ.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

2. **Создать и настроить параметры QR** — обратите внимание на использование `QrCodeTypes.HIBCLICQR`.  

```java
signature.sign(destinFilePath, hibcLic_AZ);
```

3. **Подписать документ**  

```java
QrCodeSignOptions hibcLic_DM = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix);
hibcLic_DM.setLeft(1); // Set the position from left
hibcLic_DM.setTop(400); // Set the position from top
hibcLic_DM.setReturnContent(true); // Return content after signing
hibcLic_DM.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

> **Прямой ответ:** Используйте `QrCodeTypes.HIBCLICQR` в `QrCodeSignOptions`, задайте строку содержимого HIBC, позиционируйте код с помощью `setLeft()` и `setTop()`, затем вызовите `signature.sign(outputPath, options)`. QR‑штрих‑код встраивается мгновенно, готовый к захвату смартфоном или сканером.

## Распространённые ошибки, которых следует избегать

### 1. Забвение освобождения ресурсов
**Неправильно:**  
```java
Signature signature = new Signature("sample.pdf");
signature.sign(destinFilePath, options);
// Oops, no dispose() call
```  

**Исправление:** Оберните использование `Signature` в блок try‑with‑resources или явно вызовите `close()` в finally‑блоке.

### 2. Использование неверных строк формата HIBC
**Неправильно:** Использование общих строк, например “12345”.  
**Исправление:** Следуйте стандарту HIBCC (например, `A123PROD30917/75#422011907#GP293`). Проверьте с помощью [HIBCC online validator](https://www.hibcc.org/).

### 3. Жёсткое кодирование путей к файлам
**Неправильно:**  
```java
String sourceFilePath = "C:/Users/John/Documents/test.pdf";
```  

**Исправление:** Сохраняйте пути в файле конфигурации или переменной окружения и считывайте их во время выполнения.

### 4. Игнорирование конфликтов позиции штрих‑кода
Размещайте штрих‑коды вдали от существующего текста или подписей. Используйте координаты PDF (начало в левом нижнем углу) и проверяйте на печатном образце.

### 5. Не тестировать на реальных сканерах
Распечатайте подписанный PDF и отсканируйте его на том же оборудовании, которое используется в вашем рабочем процессе. Проверьте читаемость при разных качествах печати.

## Практические применения в здравоохранении

| Сценарий | Рекомендуемый штрих‑код | Почему подходит |
|----------|------------------------|-----------------|
| **Фармацевтическое распределение** | QR Code | Большая ёмкость данных, широко сканируется смартфонами. |
| **Управление запасами** | Data Matrix | Небольшой размер, идеален для плотных этикеток на полках. |
| **Регуляторное соответствие (FDA 21 CFR Part 11)** | QR + Data Matrix | Двойной формат обеспечивает избыточность и возможность аудита. |
| **Отслеживание медицинских устройств** | Aztec Code | Компактный размер подходит для упаковки с ограниченным пространством. |

## Соображения по производительности и лучшие практики

### Шаблон пакетной обработки
```java
List<String> filesToSign = getFileList();
for (String filePath : filesToSign) {
    Signature signature = null;
    try {
        signature = new Signature(filePath);
        // Sign and save
    } finally {
        if (signature != null) signature.dispose();
    }
}
```

- Создавайте новый экземпляр `Signature` для каждого файла, чтобы снизить использование памяти.  
- Используйте фиксированный пул потоков (`Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() - 1)`) для параллельной обработки, но следите за размером кучи, так как каждый `Signature` держит весь PDF в памяти.

### Обновляйте библиотеки
Выпуски GroupDocs повышают скорость обработки до **20 %** и добавляют новые функции соответствия HIBC. Планируйте проверку зависимостей каждый квартал.

### Кеширование шаблонов
Загрузите PDF‑шаблон один раз, клонируйте его для каждого варианта штрих‑кода и подпишите клоны. Это уменьшает ввод‑вывод и ускоряет рабочие процессы с высоким объёмом.

## Часто задаваемые вопросы

**Q: Может ли GroupDocs.Signature подписывать типы файлов, отличные от PDF?**  
A: Да, он также поддерживает DOCX, XLSX, PPTX, PNG, JPEG и TIFF с тем же API подписи штрих‑кода.

**Q: Как решить ошибки «Invalid barcode content»?**  
A: Убедитесь, что ваша строка HIBC соответствует точному синтаксису HIBCC, используйте онлайн‑валидатор и проверьте, что вы используете правильную константу `QrCodeTypes` для выбранного формата.

**Q: Какова максимальная ёмкость данных для каждого формата HIBC?**  
A: QR ≈ 4 296 буквенно‑цифровых символов, Aztec ≈ 3 832 числовых / 3 067 буквенно‑цифровых, Data Matrix ≈ 3 116 числовых / 2 335 буквенно‑цифровых. Держите коды менее 200 символов для оптимальной надёжности сканирования.

**Q: Можно ли встроить несколько типов штрих‑кодов в один PDF?**  
A: Конечно. Создайте отдельные объекты `QrCodeSignOptions` с разными позициями и вызовите `signature.sign()` для каждого. Просто убедитесь, что они не перекрываются.

**Q: Нужен ли интернет для подписи во время выполнения?**  
A: Нет. После того как JAR находится в classpath и лицензия активирована, все операции выполняются локально.

## Дополнительные ресурсы

- [Документация GroupDocs.Signature для Java](https://docs.groupdocs.com/signature/java/)  
- [Руководство по API](https://reference.groupdocs.com/signature/java/)  
- [Последние загрузки релизов](https://releases.groupdocs.com/signature/java/)  
- [Купить лицензию](https://purchase.groupdocs.com/buy)  
- [Получить бесплатную пробную версию](https://releases.groupdocs.com/signature/java/)  
- [Запросить временную лицензию](https://purchase.groupdocs.com/temporary-license/)  
- [Форум GroupDocs](https://forum.groupdocs.com/c/signature/)

---

**Последнее обновление:** 2026-05-16  
**Тестировано с:** GroupDocs.Signature 23.12 for Java  
**Автор:** GroupDocs  

```java
signature.sign(destinFilePath, hibcLic_DM);
```

## Связанные руководства

- [Создать подпись штрих‑кода в PDF на Java – Руководство GroupDocs](/signature/java/barcode-signatures/create-sign-pdfs-groupdocs-barcode-java/)
- [Создать подпись штрих‑кода в Java – Обновление штрих‑кодов PDF](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [Как читать QR‑код из PDF с помощью Java и GroupDocs.Signature](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)