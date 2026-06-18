---
categories:
- Java Development
date: '2026-06-11'
description: Узнайте, как подписать PDF с помощью Java, используя GroupDocs.Signature,
  добавить digital signature и timestamp. Пошаговое руководство с примерами кода и
  лучшими практиками.
keywords:
- how to sign pdf
- add digital signature pdf
- timestamp pdf signature
- java pdf signature library
- groupdocs signature java
lastmod: '2026-06-11'
linktitle: Добавить digital signature в PDF Java
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to sign PDF with Java using GroupDocs.Signature, add digital
    signature and timestamp. Step-by-step guide with code examples and best practices.
  headline: 'How to Sign PDF with Java: Add Digital Signature and Timestamp'
  type: TechArticle
- description: Learn how to sign PDF with Java using GroupDocs.Signature, add digital
    signature and timestamp. Step-by-step guide with code examples and best practices.
  name: 'How to Sign PDF with Java: Add Digital Signature and Timestamp'
  steps:
  - name: Import Required Classes
    text: The following imports give you access to signature configuration, positioning,
      and timestamp functionality.
  - name: Define Your File Paths
    text: Set up paths for your input PDF, certificate, and where you want the signed
      PDF saved. Keep the certificate file secure; it contains your private key.
  - name: Initialize the Signature Object
    text: Create a `Signature` instance pointing to the PDF you want to sign. This
      loads the PDF into memory and prepares it for signing.
  - name: Configure Signature Properties and Timestamp
    text: The `DigitalSignature` class represents the cryptographic seal that will
      be embedded in the PDF. You can also attach a timestamp from a trusted authority.
      * **ContactInfo** – e.g., `john.doe@company.com` * **Location** – e.g., `New
      York Office` * **Reason** – e.g., `Contract Approval` We use FreeTSA
  - name: Configure Digital Sign Options
    text: The `SignOptions` class ties together the certificate, signature properties,
      and visual placement. Alignment enums control where the signature appears.
  - name: Sign and Save the Document
    text: Execute the signing process and write the signed PDF to disk. The returned
      `SignResult` object tells you whether the operation succeeded and lists any
      warnings.
  type: HowTo
- questions:
  - answer: A digital signature uses cryptographic algorithms to verify identity and
      detect tampering, while an electronic signature can be as simple as a typed
      name.
    question: What's the difference between a digital signature and an electronic
      signature?
  - answer: Only for the timestamp service; the cryptographic signing itself runs
      locally.
    question: Do I need internet connectivity to sign PDFs?
  - answer: Any modification breaks the signature, and PDF viewers will display a
      warning indicating the document has been altered.
    question: Can signed PDFs be edited later?
  - answer: Most PDF readers verify automatically; programmatically, use GroupDocs.Signature's
      verification API to check status, signer details, and timestamp validity.
    question: How do I verify a signed PDF?
  - answer: The embedded timestamp proves the signature was created while the certificate
      was still valid, preserving legal standing.
    question: What happens if my certificate expires after I've signed documents?
  type: FAQPage
tags:
- pdf-signing
- digital-signatures
- java-security
- groupdocs
title: 'Как подписать PDF с помощью Java: добавить digital signature и timestamp'
type: docs
url: /ru/java/digital-signatures/digital-signature-timestamp-pdf-java-groupdocs/
weight: 1
---

# Как подписать PDF с помощью Java и временной метки

Когда‑ли вы когда‑нибудь отправляли важный документ и беспокоились, сможет ли кто‑то изменить его позже? Вы не одиноки. Независимо от того, создаёте ли вы корпоративную систему управления документами, платформу для подписания контрактов или просто хотите программно защищать свои PDF‑файлы, **how to sign PDF** с надёжной временной меткой — это решение. Добавление цифровой подписи не только доказывает, кто подписал файл, но и создаёт неизменяемую запись о *точном* времени подписи.

## Быстрые ответы
- **Какую библиотеку упрощает подпись PDF в Java?** GroupDocs.Signature for Java.  
- **Нужен ли мне доступ к интернету?** Only for the timestamp authority; the signing itself is offline.  
- **Можно ли использовать самоподписанный сертификат для тестирования?** Yes, generate one with `keytool`.  
- **Есть ли ограничение по размеру?** The library can sign PDFs up to 500 MB without loading the whole file into memory.  
- **Сколько форматов поддерживает GroupDocs?** Over 50 input and output formats, including DOCX, XLSX, PPTX, HTML, and images.

## Почему цифровые подписи важны (и почему вам нужны временные метки)

Загрузите ваш PDF, примените криптографическую печать и внедрите надёжную временную метку — этот двухшаговый процесс гарантирует аутентификацию, целостность и неотказуемость. Временная метка доказывает, что подпись существовала в конкретный момент, даже если сертификат подписи позже истечёт или будет отозван.

## Как подписать PDF с помощью Java?

Загрузите ваш PDF с помощью `new Signature("input.pdf")`, настройте объект `DigitalSignature`, прикрепите временную метку от надёжного удостоверяющего центра и вызовите `sign()` — вся операция завершается в нескольких строках кода. GroupDocs.Signature автоматически обрабатывает разбор сертификата, вычисление хеша и получение временной метки, позволяя вам сосредоточиться на бизнес‑логике, а не на криптографии.

## Настройка GroupDocs.Signature для Java

### Методы интеграции

Выберите любой используемый вами инструмент сборки:

**Для пользователей Maven:**  
Add this dependency to your `pom.xml`:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Для пользователей Gradle:**  
Add this to your `build.gradle`:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Прямое скачивание (если предпочитаете):**  
Перейдите к [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) и скачайте JAR‑файл. Добавьте его в classpath вашего проекта вручную. Смотрите [GroupDocs.Signature Documentation](https://docs.groupdocs.com/signature/java/) для подробного справочника API. Для самой последней сборки смотрите [Latest Version & Releases](https://releases.groupdocs.com/signature/java/).

Совет: используйте Maven или Gradle, если возможно — это значительно упрощает управление зависимостями и их обновление в дальнейшем.

### Получение лицензии

GroupDocs предлагает несколько вариантов, в зависимости от стадии вашего проекта:

1. **Free Trial** – Идеально для оценки. [Download Trial Version](https://releases.groupdocs.com/signature/java/) и протестируйте все функции.  
2. **Temporary License** – Нужен полный доступ для разработки без водяного знака пробной версии? Получите 30‑дневную временную лицензию.  
3. **Commercial License** – Для использования в продакшене, [Buy License](https://purchase.groupdocs.com/buy). Цены зависят от типа развертывания.

Нужна помощь? Посетите [GroupDocs Forum](https://forum.groupdocs.com/c/signature/).

### Базовая инициализация

Класс `Signature` — это объект верхнего уровня в GroupDocs.Signature, представляющий один PDF‑файл в памяти. После создания все операции чтения и записи проходят через этот объект.

```java
import com.groupdocs.signature.Signature;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
final Signature signature = new Signature(filePath);
```

Просто, не правда ли? Вы указываете ему ваш PDF‑файл, и всё готово. Объект `Signature` — ваш основной интерфейс для всех операций подписи.

## Как добавить цифровую подпись в PDF на Java: пошагово

Загрузите ваш PDF, настройте параметры подписи, прикрепите временную метку и сохраните подписанный документ — всё в понятном последовательном процессе.

### Шаг 1: Импортировать необходимые классы

Следующие импорты дают вам доступ к настройкам подписи, позиционированию и функционалу временных меток.

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.signatures.PdfDigitalSignature;
import com.groupdocs.signature.domain.structs.TimeStamp;
import com.groupdocs.signature.options.sign.DigitalSignOptions;
```

### Шаг 2: Определить пути к файлам

Установите пути к входному PDF, сертификату и месту, где будет сохранён подписанный PDF. Храните файл сертификата в безопасности; он содержит ваш закрытый ключ.

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
String certificatePath = "YOUR_DOCUMENT_DIRECTORY/certificate.pfx";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/digitallySignedTimeStamp.pdf";
```

### Шаг 3: Инициализировать объект Signature

Создайте экземпляр `Signature`, указывающий на PDF, который нужно подписать. Это загружает PDF в память и подготавливает его к подписи.

```java
final Signature signature = new Signature(filePath);
```

### Шаг 4: Настроить свойства подписи и временную метку

Класс `DigitalSignature` представляет криптографическую печать, которая будет внедрена в PDF. Вы также можете прикрепить временную метку от надёжного удостоверяющего центра.

```java
PdfDigitalSignature pdfDigitalSignature = new PdfDigitalSignature();
pdfDigitalSignature.setContactInfo("Contact Information");
pdfDigitalSignature.setLocation("Location Info");
pdfDigitalSignature.setReason("Signing Reason");

// Configure the TimeStamp with URL, User Id, and Password
TimeStamp timeStamp = new TimeStamp("https://freetsa.org/tsr", "User Id", "Password");
pdfDigitalSignature.setTimeStamp(timeStamp);
```

* **ContactInfo** – например, `john.doe@company.com`  
* **Location** – например, `New York Office`  
* **Reason** – например, `Contract Approval`

Для демонстрации мы используем FreeTSA (бесплатный центр временных меток). В продакшене выбирайте коммерческий TSA для гарантированной доступности и юридической силы.

### Шаг 5: Настроить параметры цифровой подписи

Класс `SignOptions` связывает сертификат, свойства подписи и визуальное размещение. Перечисления выравнивания определяют, где будет отображаться подпись.

```java
DigitalSignOptions options = new DigitalSignOptions(certificatePath);
options.setPassword("YourCertificatePassword"); // Certificate password
options.setSignature(pdfDigitalSignature); // Attach the PdfDigitalSignature object

// Specify signature alignment (where it appears on the page)
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
```

### Шаг 6: Подписать и сохранить документ

Выполните процесс подписи и запишите подписанный PDF на диск. Возвращаемый объект `SignResult` сообщает, успешно ли завершилась операция, и перечисляет любые предупреждения.

```java
try {
    SignResult signResult = signature.sign(outputFilePath, options);
    System.out.println("Document signed successfully!");
    System.out.println("Output: " + outputFilePath);
} catch (Exception e) {
    throw new RuntimeException("Error during signing process: " + e.getMessage());
}
```

## Распространённые ошибки, которых следует избегать

### 1. Проблемы с сертификатом

**Problem:** Ошибки «Invalid certificate».  
**Fix:** Проверьте пароль с помощью `keytool -list -v -keystore your.pfx`.

```bash
keytool -list -v -keystore certificate.pfx -storetype PKCS12
```

### 2. Тайм‑ауты сервиса временных меток

**Problem:** Сетевые тайм‑ауты при обращении к TSA.  
**Fix:** Проверьте соединение (`curl -I https://freetsa.org/tsr`), добавьте логику повторных попыток или настройте резервный TSA.

```java
new File(outputFilePath).getParentFile().mkdirs();
```

### 3. Проблемы с правами доступа к файлам

**Problem:** «Access denied» при сохранении.  
**Fix:** Убедитесь, что каталог вывода существует и приложение имеет права на запись.

```bash
keytool -genkeypair -alias mykey -keyalg RSA -keysize 2048 -storetype PKCS12 -keystore certificate.pfx -validity 365
```

### 4. Проблемы с памятью при работе с большими PDF

**Problem:** `OutOfMemoryError` для больших файлов.  
**Fix:** Увеличьте размер кучи JVM (`-Xmx4g`) или обрабатывайте файлы пакетами.

### 5. Неправильное размещение подписи

**Problem:** Подпись перекрывает существующее содержание.  
**Fix:** Сначала протестируйте настройки выравнивания; для пиксель‑точного размещения используйте опции на основе координат.

## Советы по управлению сертификатами

### Получение сертификата для разработки

Создайте самоподписанный сертификат с помощью `keytool` в Java для целей тестирования.

```java
   String certPassword = System.getenv("CERT_PASSWORD");
   ```

### Лучшие практики работы с сертификатами

1. **Никогда не встраивайте пароли в код** – используйте переменные окружения.  
2. **Обновляйте сертификаты** до их истечения.  
3. **Храните закрытые ключи** в защищённом оборудовании (HSM) для приложений с высоким уровнем безопасности.  
4. **Создавайте резервные копии сертификатов** в защищённом месте.  
5. **Проверяйте сертификаты** перед подписью, чтобы обнаружить просроченные или отозванные.

## Лучшие практики безопасности

### 1. Защищать закрытые ключи

Храните сертификаты вне каталога проекта, используйте конфигурации, специфичные для окружения, и рассматривайте возможность применения HSM для корпоративных развертываний.

### 2. Проверять входные PDF

Проверьте наличие повреждений, существующих подписей, ограничения по размеру и соответствие содержимого перед подписью.

### 3. Реализовать аудит‑логирование

Записывайте каждую операцию подписи с временной меткой, пользователем, именем документа и статусом.

```java
try {
    SignResult result = signature.sign(outputFilePath, options);
    logger.info("Document signed: " + filePath + " by " + signerEmail);
} catch (Exception e) {
    logger.error("Signing failed: " + filePath + " - " + e.getMessage());
    // Handle appropriately
}
```

### 4. Использовать надёжные центры временных меток

Никогда не полагайтесь на локальное системное время; всегда запрашивайте временную метку у TSA, совместимого с RFC 3161.

### 5. Реализовать обработку ошибок

Отлавливайте исключения, не раскрывая конфиденциальные детали.

```java
try {
    signature.sign(outputFilePath, options);
} catch (Exception e) {
    // Log detailed error internally
    logger.error("Signing error: " + e.getMessage(), e);
    // Return generic error to client
    throw new ApplicationException("Unable to sign document. Please try again.");
}
```

## Практические примеры использования и приложения

### 1. Системы управления контрактами

Сотрудники подписывают NDA и соглашения в электронном виде; временные метки точно фиксируют момент принятия каждого контракта.

### 2. Обработка финансовых документов

Пакетно подписывайте счета-фактуры и заказы, обеспечивая неизменяемый аудит‑трейл для регуляторов.

### 3. Проверка образовательных удостоверений

Университеты выпускают защищённые от подделки транскрипты, которые можно мгновенно проверить через ссылку с QR‑кодом.

### 4. Управление лицензиями программного обеспечения

Создавайте лицензионные сертификаты с цифровой подписью и временной меткой, чтобы предотвратить подделку.

### 5. Соответствие нормативным требованиям (FDA 21 CFR Part 11 и др.)

Компании, производящие медицинские устройства, подписывают SOP и отчёты валидации; временные метки удовлетворяют требования неотказуемости.

## Соображения производительности и оптимизация

### Управление памятью

Обрабатывайте большие PDF‑файлы пакетами, своевременно закрывайте объекты `Signature` и увеличивайте размер кучи при необходимости.

### Оптимизация сети для временных меток

Пулите HTTP‑соединения, реализуйте повторные попытки с экспоненциальным откатом и кэшируйте временные метки для быстрых последовательных подписаний.

### Лучшие практики пакетной обработки

```java
// Pseudo‑code: process a list of PDFs in parallel, limiting to 5 concurrent TSA calls
```
*Избегайте создания слишком большого количества потоков; 5‑10 одновременных подписаний обеспечивают баланс между пропускной способностью и нагрузкой на TSA.*

### Оптимизация ввода‑вывода диска

Используйте SSD для временных файлов, минимизируйте циклы чтения/записи и удаляйте временные артефакты после каждой подписи.

## Руководство по устранению неполадок

### Ошибка: «Invalid Certificate Password»

**Solution:** Проверьте пароль с помощью `keytool -list -keystore your.pfx`.

```java
ExecutorService executor = Executors.newFixedThreadPool(5);
List<Future<SignResult>> futures = new ArrayList<>();

for (String pdfPath : pdfPaths) {
    futures.add(executor.submit(() -> {
        try (Signature sig = new Signature(pdfPath)) {
            return sig.sign(outputPath, options);
        }
    }));
}

// Wait for all to complete
for (Future<SignResult> future : futures) {
    SignResult result = future.get();
    // Process result
}

executor.shutdown();
```

### Ошибка: «Timestamp Authority Not Responding»

**Solution:** Проверьте URL TSA, правила брандмауэра и добавьте логику резервного TSA.

```bash
keytool -list -v -keystore certificate.pfx -storetype PKCS12
```

### Ошибка: «PDF is Already Signed»

**Solution:** Сначала обнаружьте существующие подписи; либо добавьте контр‑подпись, либо подпишите свежую копию.

### Ошибка: «Access Denied» при сохранении

**Solution:** Убедитесь, что каталог вывода существует, приложение имеет права на запись и ни один другой процесс не блокирует файл.

```java
TimeStamp timeStamp;
try {
    timeStamp = new TimeStamp("https://freetsa.org/tsr", "", "");
} catch (Exception e) {
    // Fallback to alternative TSA
    timeStamp = new TimeStamp("https://alternate-tsa.com/tsr", "", "");
}
```

### Ошибка: OutOfMemoryError

**Solution:** Увеличьте размер кучи JVM, обрабатывайте PDF‑файлы небольшими партиями или переключитесь на потоковые API для очень больших файлов.

## Заключение и дальнейшие шаги

Вы узнали, **how to sign PDF** файлы с помощью Java, как добавить надёжную временную метку и как справляться с распространёнными проблемами. Далее изучайте:
1. Добавление нескольких полей подписи для многопользовательских соглашений.  
2. Проверка подписей программно с помощью GroupDocs.Signature.  
3. Настройка внешнего вида подписи (изображения, текст, позиционирование).  
4. Создание надёжного сервиса пакетного подписания с очередями и мониторингом.

## Часто задаваемые вопросы

**Q:** В чём разница между цифровой подписью и электронной подписью?  
**A:** Цифровая подпись использует криптографические алгоритмы для проверки личности и обнаружения подделки, тогда как электронная подпись может быть простой печатной подписью.

**Q:** Нужен ли мне доступ к интернету для подписания PDF?  
**A:** Только для сервиса временных меток; сама криптографическая подпись выполняется локально.

**Q:** Можно ли позже редактировать подписанные PDF?  
**A:** Любое изменение нарушает подпись, и PDF‑просмотрщики отобразят предупреждение о том, что документ был изменён.

**Q:** Как проверить подписанный PDF?  
**A:** Большинство PDF‑просмотрщиков проверяют автоматически; программно используйте API проверки GroupDocs.Signature для проверки статуса, данных подписанта и валидности временной метки.

**Q:** Что происходит, если мой сертификат истекает после того, как я подписал документы?  
**A:** Встроенная временная метка доказывает, что подпись была создана, пока сертификат ещё был действителен, сохраняя юридическую силу.

**Q:** Можно ли использовать это с облачным хранилищем (S3, Azure Blob и т.д.)?  
**A:** Да — скачайте PDF во временное место, подпишите его, затем загрузите подписанную версию обратно в облако.

**Q:** Есть ли ограничения по размеру файлов?  
**A:** Библиотека работает с PDF до 500 МБ без полной загрузки файла в память; для больших файлов может потребоваться потоковая обработка.

**Q:** Сколько стоит GroupDocs.Signature для коммерческого использования?  
**A:** Цены зависят от типа развертывания; свяжитесь с отделом продаж GroupDocs для актуальных тарифов. Бесплатные пробные версии и временные лицензии доступны для оценки.

**Q:** Работает ли это на серверах Linux?  
**A:** Да. GroupDocs.Signature for Java независим от платформы и работает на любой ОС с установленным JRE.

**Last Updated:** 2026-06-11  
**Tested With:** GroupDocs.Signature 23.9 for Java  
**Author:** GroupDocs

```java
File outputFile = new File(outputFilePath);
outputFile.getParentFile().mkdirs(); // Create directories if needed

if (!outputFile.canWrite() && outputFile.exists()) {
    throw new IOException("Cannot write to " + outputFilePath);
}
```

## Связанные руководства

- [Как проверить цифровые сертификаты в Java — Полное руководство с примерами кода](/signature/java/digital-signatures/java-certificate-verification-groupdocs-signature/)
- [Как программно подписать PDF в Java с помощью GroupDocs.Signature](/signature/java/digital-signatures/sign-pdfs-groupdocs-signature-java/)
- [Добавить изображение подписи в PDF на Java с GroupDocs](/signature/java/image-signatures/sign-pdf-image-signature-groupdocs-java/)