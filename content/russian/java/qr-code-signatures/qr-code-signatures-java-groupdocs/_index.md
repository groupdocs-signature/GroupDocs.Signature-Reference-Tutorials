---
"date": "2025-05-08"
"description": "Узнайте, как повысить безопасность документов, внедрив и проверив QR-коды в Java с помощью GroupDocs.Signature. Следуйте этому пошаговому руководству для безопасного процесса подписания."
"title": "Защитите свои документы&#58; реализуйте подписи QR-кодов в Java с помощью GroupDocs.Signature"
"url": "/ru/java/qr-code-signatures/qr-code-signatures-java-groupdocs/"
"weight": 1
---

# Защитите свои документы: реализуйте подписи QR-кодов в Java с помощью GroupDocs.Signature

В современном цифровом мире обеспечение безопасности таких документов, как контракты, счета-фактуры и конфиденциальная персональная информация, имеет решающее значение. Одним из инновационных подходов к повышению безопасности документов и упрощению процессов проверки является использование QR-кодов. Это руководство поможет вам реализовать и проверить QR-коды для ваших документов в Java с помощью GroupDocs.Signature.

## Что вы узнаете
- Как подписывать документы с помощью QR-кодов
- Проверка подписанных документов с помощью QR-кодов
- Поиск существующих подписей QR-кодов в документе
- Обновление и удаление подписей QR-кодов из ваших документов

Давайте настроим вашу среду и начнем!

### Предпосылки
Прежде чем начать, убедитесь, что у вас есть следующие предварительные условия:

#### Необходимые библиотеки и зависимости
Вам понадобится GroupDocs.Signature для Java. Вы можете подключить его через Maven или Gradle, либо скачать напрямую.

**Maven**
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Грейдл**
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**Прямая загрузка**
Загрузите последнюю версию с сайта [GroupDocs.Signature для релизов Java](https://releases.groupdocs.com/signature/java/).

#### Требования к настройке среды
- Убедитесь, что у вас установлен Java Development Kit (JDK) 8 или выше.
- Используйте IDE, например IntelliJ IDEA, Eclipse или NetBeans.

#### Необходимые знания
Приветствуется базовое понимание программирования на Java и обработки документов.

## Настройка GroupDocs.Signature для Java
Чтобы использовать GroupDocs.Signature в своем проекте, выполните следующие действия:
1. **Установка**: Выберите Maven, Gradle или прямую загрузку в зависимости от ваших настроек.
2. **Приобретение лицензии**:
   - Начните с бесплатной пробной версии, доступной на [Сайт GroupDocs](https://releases.groupdocs.com/signature/java/).
   - Рассмотрите возможность получения временной лицензии для расширенного тестирования и разработки от [здесь](https://purchase.groupdocs.com/temporary-license/).
3. **Базовая инициализация**: 
    Вот как инициализировать GroupDocs.Signature:

    ```java
    Signature signature = new Signature("YOUR_DOCUMENT_PATH");
    ```

Это подготовит вас к внедрению подписей с помощью QR-кодов.

## Руководство по внедрению

### Подпишите документ с помощью QR-кода
#### Обзор
Подписание документа с помощью QR-кода подразумевает встраивание уникального кода, представляющего вашу цифровую подпись. Этот процесс защищает документ и позволяет легко проверить его подлинность в дальнейшем.

##### Шаг 1: Настройте параметры подписи
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

Signature signature = new Signature("YOUR_DOCUMENT_PATH");
QrCodeSignOptions signOptions = new QrCodeSignOptions("John Smith", com.groupdocs.signature.domain.qrcodes.QrCodeTypes.QR);

signOptions.setVerticalAlignment(VerticalAlignment.Top);
signOptions.setHorizontalAlignment(HorizontalAlignment.Center);
signOptions.setWidth(100);
signOptions.setHeight(40);
```
**Объяснение**: `QrCodeSignOptions` Настроено для создания QR-кода с заданным текстом и выравниванием. При необходимости отрегулируйте ширину и высоту.

##### Шаг 2: Настройте внешний вид подписи
```java
import java.awt.Color;

signOptions.setForeColor(Color.RED); // Установить цвет QR-кода
com.groupdocs.signature.domain.SignatureFont signatureFont = new com.groupdocs.signature.domain.SignatureFont();
signatureFont.setSize(12);
signatureFont.setFamilyName("Comic Sans MS");
signOptions.setFont(signatureFont);
```
**Объяснение**: Настройка шрифта и цвета улучшает визуальную идентификацию.

##### Шаг 3: Подпишите документ
```java
import java.util.ArrayList;
import java.util.List;

List<String> signatureIds = new ArrayList<>();
List<com.groupdocs.signature.domain.BaseSignature> signedSignatures = signature.sign("YOUR_OUTPUT_PATH", signOptions).getSucceeded();

for (com.groupdocs.signature.domain.BaseSignature temp : signedSignatures) {
    signatureIds.add(temp.getSignatureId());
}
```
**Объяснение**: На этом этапе документ подписывается, а идентификаторы подписей сохраняются для дальнейшего использования.

### Подтвердите документ с помощью QR-кода подписи
#### Обзор
Верификация гарантирует, что документ подписан законно. Вот как можно проверить подпись QR-кода в документе.

##### Шаг 1: Настройте параметры проверки
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.verify.QrCodeVerifyOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeVerifyOptions verifyOptions = new QrCodeVerifyOptions();

verifyOptions.setEncodeType(QrCodeTypes.QR);
verifyOptions.setText("John Smith"); // Текст для подтверждения
verifyOptions.setAllPages(false); 
verifyOptions.setPageNumber(1);
```
**Объяснение**Параметры проверки указывают, какой тип QR-кода и текст следует искать, гарантируя, что подпись соответствует вашим ожиданиям.

##### Шаг 2: Выполните проверку
```java
boolean isValid = signature2.verify(verifyOptions).isValid();
System.out.println("Is Signature Valid? " + isValid);
```
**Объяснение**: проверяет, содержит ли документ действительный QR-код, соответствующий вашим критериям.

### Поиск документа для подписи QR-кодом
#### Обзор
Иногда необходимо найти существующие подписи в документе. Вот как можно найти их с помощью GroupDocs.Signature.

##### Шаг 1: Настройте параметры поиска
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import com.groupdocs.signature.options.search.QrCodeSearchOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeSearchOptions searchOptions = new QrCodeSearchOptions();
searchOptions.setAllPages(true);
```
**Объяснение**: Это настроит инструмент для сканирования всех страниц на наличие подписей QR-кодов.

##### Шаг 2: Выполнение поиска
```java
List<QrCodeSignature> signatures = signature2.search(QrCodeSignature.class, searchOptions);

for (QrCodeSignature qrSignature : signatures) {
    System.out.println("Found Signature ID: " + qrSignature.getSignatureId());
}
```
**Объяснение**: Это позволит извлечь все подписи QR-кодов, найденные в документе.

### Обновление QR-кода подписи документа
#### Обзор
Обновление подписи подразумевает изменение её свойств, таких как положение или размер. Вот как это сделать:

##### Шаг 1: Подготовка подписей для обновления
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import java.io.ByteArrayOutputStream;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
List<QrCodeSignature> signaturesToUpdate = new ArrayList<>();

// Предположим, что «signatures» — это список объектов QrCodeSignature, полученный в результате поиска
for (QrCodeSignature qrSignature : signatures) {
    qrSignature.setLeft(qrSignature.getLeft() + 100);
    qrSignature.setTop(qrSignature.getTop() + 100);
    qrSignature.setWidth(200);
    qrSignature.setHeight(50);
    signaturesToUpdate.add(qrSignature);
}
```
**Объяснение**: Это позволяет изменить положение и размер каждой подписи.

##### Шаг 2: Обновите документ
```java
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
signature2.update(outputStream, signaturesToUpdate);
```
**Объяснение**: Документ обновлен с использованием измененных подписей QR-кода.

### Удалить QR-код подписи документа по идентификатору
#### Обзор
Удаление подписи может потребоваться, если она больше не нужна или была добавлена по ошибке. Вот как можно удалить её, используя её уникальный идентификатор.

##### Шаг 1: Определите подписи, которые нужно удалить
```java
import com.groupdocs.signature.domain.SignatureCollection;
import java.util.Arrays;

SignatureCollection signaturesToDelete = signature2.search(QrCodeSignature.class);
Arrays.stream(signaturesToDelete).forEach(signature -> {
    if (signature.getSignatureId().equals("YOUR_SIGNATURE_ID")) {
        signature.delete();
    }
});
```
**Объяснение**: Эта функция находит и удаляет подпись QR-кода по ее уникальному идентификатору.

## Заключение
Это руководство поможет вам защитить документы с помощью QR-кодов в Java с помощью GroupDocs.Signature. Выполнив эти шаги, вы сможете обеспечить надёжную подпись документов и легко проверить их подлинность.