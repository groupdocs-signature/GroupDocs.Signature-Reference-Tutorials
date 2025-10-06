---
"date": "2025-05-08"
"description": "Узнайте, как безопасно подписывать изображения DICOM с помощью GroupDocs.Signature для Java. Повысьте безопасность документов, встроив QR-коды и метаданные."
"title": "Подписывайте изображения DICOM с помощью QR-кодов и метаданных с помощью GroupDocs.Signature для Java"
"url": "/ru/java/image-signatures/sign-dicom-images-groupdocs-signature-java/"
"weight": 1
type: docs
---
# Как подписывать изображения DICOM с помощью QR-кодов и метаданных с помощью GroupDocs.Signature для Java

## Введение

В стремительно развивающейся сфере цифрового здравоохранения безопасное управление данными пациентов имеет первостепенное значение. Это руководство поможет вам внедрить надежное решение на основе GroupDocs.Signature для Java для подписи изображений DICOM (Digital Imaging and Communications in Medicine, цифровая визуализация и коммуникации в медицине) QR-кодами и метаданными. Эти функции обеспечивают подлинность, улучшают прослеживаемость и обеспечивают соблюдение нормативных требований за счет встраивания важной информации непосредственно в медицинские изображения.

### Что вы узнаете:
- Как интегрировать GroupDocs.Signature для Java в ваш проект.
- Процесс подписания DICOM-изображений QR-кодами.
- Добавление метаданных XMP для повышения безопасности документов.
- Извлечение, проверка и поиск подписей в файлах DICOM.
- Создание предпросмотров подписанных DICOM-изображений.

Давайте начнём! Прежде чем начать, убедитесь, что у вас есть всё необходимое для успешного освоения материала.

## Предпосылки

Для эффективной реализации функций GroupDocs.Signature убедитесь, что выполнены следующие предварительные условия:

### Необходимые библиотеки и зависимости
- **GroupDocs.Signature для Java**: Вам понадобится версия этой библиотеки 23.12 или более поздняя.

### Требования к настройке среды
- **Комплект разработчика Java (JDK)**: Убедитесь, что в вашей системе установлен JDK.
- **ИДЕ**: Используйте интегрированную среду разработки, например IntelliJ IDEA или Eclipse.

### Необходимые знания
Базовое понимание:
- Программирование на Java и принципы объектно-ориентированного программирования.
- Инструменты сборки Maven или Gradle для управления зависимостями.

## Настройка GroupDocs.Signature для Java

Чтобы начать работу с GroupDocs.Signature, необходимо добавить его как зависимость в свой проект. Вот как это можно сделать с помощью различных инструментов сборки:

### Maven
Добавьте следующий фрагмент в свой `pom.xml` файл:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Грейдл
Включите это в свой `build.gradle` файл:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Прямая загрузка
Альтернативно, вы можете загрузить последнюю версию с сайта [GroupDocs.Signature для релизов Java](https://releases.groupdocs.com/signature/java/).

#### Этапы получения лицензии
1. **Бесплатная пробная версия**: Протестируйте функции с помощью бесплатной пробной версии с ограниченным временем.
2. **Временная лицензия**Получите временную лицензию, чтобы изучить все возможности.
3. **Покупка**: Если вам нужен долгосрочный доступ, приобретите подписку.

#### Базовая инициализация и настройка

Чтобы инициализировать GroupDocs.Signature, создайте экземпляр `Signature` сорт:
```java
import com.groupdocs.signature.Signature;

// Инициализируйте объект подписи, указав путь к вашему DICOM-файлу.
Signature signature = new Signature(filePath);
```

## Руководство по внедрению

### Подписание изображения DICOM с помощью QR-кода и метаданных

#### Обзор
Эта функция позволяет подписывать изображения DICOM с помощью QR-кода и добавлять метаданные XMP, повышая безопасность документов.

#### Шаг 1: Настройте параметры подписи QR-кода
```java
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.signatures.QrCodeSignOptions;

Padding padding = new Padding();
padding.setRight(5);
padding.setLeft(5);

QrCodeSignOptions options = new QrCodeSignOptions("Patient #36363393. R: No-Issues");
options.setAllPages(true);
options.setWidth(100);
options.setHeight(100);
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
options.setMargin(padding);
```
Здесь мы настраиваем внешний вид и положение QR-кода на DICOM-изображении.

#### Шаг 2: Добавьте метаданные XMP
```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomSaveOptions;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpEntry;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpType;

DicomSaveOptions dicomSaveOptions = new DicomSaveOptions();
List<DicomXmpEntry> xmpEntries = new ArrayList<>();
xmpEntries.add(new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4"));
dicomSaveOptions.setXmpEntries(xmpEntries);
```
Этот фрагмент добавляет метаданные в файл DICOM, встраивая дополнительную информацию о пациенте.

#### Шаг 3: Подпишите документ
```java
String outputFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/" + fileName;
signature.sign(outputFilePath, options, dicomSaveOptions);
```
The `sign` Метод записывает QR-код и метаданные в ваш DICOM-файл, сохраняя его в указанном месте.

### Получение информации о подписанном DICOM-изображении

#### Обзор
Извлекайте метаданные XMP из подписанного изображения DICOM для целей проверки или аудита.
```java
import com.groupdocs.signature.domain.IDocumentInfo;
import com.groupdocs.signature.domain.signatures.MetadataSignature;

IDocumentInfo documentInfo = signature.getDocumentInfo();
for (MetadataSignature item : documentInfo.getMetadataSignatures()) {
    System.out.println(item.toString());
}
```
Этот код извлекает и печатает все подписи метаданных, связанные с файлом DICOM.

### Проверка подписанного DICOM

#### Обзор
Убедитесь, что на подписанном DICOM-изображении присутствует QR-код, подтверждающий его подлинность.
```java
import com.groupdocs.signature.domain.VerificationResult;
import com.groupdocs.signature.options.verify.QrCodeVerifyOptions;
import com.groupdocs.signature.domain.enums.TextMatchType;

QrCodeVerifyOptions verifyOptions = new QrCodeVerifyOptions();
verifyOptions.setAllPages(true);
verifyOptions.setText("Patient #36363393");
verifyOptions.setMatchType(TextMatchType.Contains);

VerificationResult result = signature.verify(verifyOptions);
if (result.isValid()) {
    System.out.println(filePath + " has successfully verified signatures!");
} else {
    System.out.println(filePath + " failed verification process.");
}
```
Этот этап проверки гарантирует, что QR-код соответствует ожидаемым критериям, подтверждая целостность документа.

### Поиск подписей в подписанном DICOM

#### Обзор
Найдите все подписи QR-кодов на подписанном изображении DICOM, чтобы просмотреть или проверить их.
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import java.util.List;

List<QrCodeSignature> signatures = signature.search(QrCodeSignature.class);
for (QrCodeSignature qrCodeSignature : signatures) {
    System.out.println("QRCode signature found at page " +
        qrCodeSignature.getPageNumber() + ": " +
        qrCodeSignature.getEncodeType().getTypeName() + ": " +
        qrCodeSignature.getText());
}
```
Эта функция полезна для сканирования всех подписей QR-кодов в документе, обеспечивая полную видимость.

### Создание предварительного просмотра подписанного DICOM

#### Обзор
Создавайте предварительные просмотры для каждой страницы подписанного DICOM-изображения, что позволяет проводить быстрый визуальный осмотр, не открывая весь файл.
```java
import com.groupdocs.signature.options.PreviewOptions;
import java.io.File;
import java.io.FileOutputStream;
import java.nio.file.Paths;

PreviewOptions previewOption = new PreviewOptions(pageNumber -> {
    try {
        String pageFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/image-" + pageNumber + ".jpg";
        return new FileOutputStream(Paths.get(pageFilePath).toFile());
    } catch (Exception e) {
        throw new RuntimeException(e.getMessage());
    }
});

signature.generatePreview(previewOption);
```
Этот фрагмент создает предварительные просмотры изображений для каждой страницы, что может быть полезно для быстрой проверки или распространения.

## Практические применения

GroupDocs.Signature для Java предлагает несколько реальных приложений:
- **Медицинская визуализация**: Безопасно подписывайте и управляйте DICOM-изображениями пациентов с помощью QR-кодов и метаданных.
- **Управление юридическими документами**: Повышение подлинности документов и соответствия требованиям судопроизводства.
- **Финансовые услуги**: Внедрите защищенные электронные подписи для конфиденциальных финансовых документов.