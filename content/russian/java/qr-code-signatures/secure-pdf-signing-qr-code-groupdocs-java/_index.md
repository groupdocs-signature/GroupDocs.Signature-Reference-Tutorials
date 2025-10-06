---
"date": "2025-05-08"
"description": "Узнайте, как защитить PDF-файлы с помощью шифрования QR-кодов и цифровых подписей с помощью GroupDocs.Signature для Java. Эффективно повысьте безопасность своих документов."
"title": "Реализуйте безопасное подписание PDF-файлов с помощью шифрования QR-кода в Java с помощью GroupDocs.Signature"
"url": "/ru/java/qr-code-signatures/secure-pdf-signing-qr-code-groupdocs-java/"
"weight": 1
type: docs
---
# Как реализовать безопасное подписание PDF-файлов с шифрованием QR-кода в Java с помощью GroupDocs.Signature

В современную цифровую эпоху защита конфиденциальной информации в документах имеет первостепенное значение. Рост киберугроз сделал шифрование данных неотъемлемой частью управления документами. Это руководство поможет вам реализовать безопасное подписание PDF-файлов с помощью шифрования QR-кода с помощью GroupDocs.Signature для Java. К концу этой статьи вы будете готовы интегрировать надежные функции безопасности в свои приложения.

## Что вы узнаете:
- Понимание симметричного шифрования данных в Java
- Создание собственного класса подписи
- Настройка подписей QR-кода с пользовательскими данными и выравниванием
- Интеграция GroupDocs.Signature для безопасного подписания PDF-файлов

Готовы погрузиться? Давайте начнём!

## Предпосылки
Прежде чем начать, убедитесь, что у вас есть следующее:
- **Комплект разработчика Java (JDK):** Версия 8 или выше.
- **Maven или Gradle:** Для управления зависимостями. Выберите в зависимости от настроек вашего проекта.
- **Знание программирования на Java:** Базовые знания объектно-ориентированного программирования на Java.

## Настройка GroupDocs.Signature для Java
Чтобы начать использовать GroupDocs.Signature, вам необходимо добавить её в качестве зависимости к своему проекту. Эта библиотека предлагает мощные инструменты для управления цифровыми подписями и шифрованием документов.

### Настройка Maven
Добавьте следующую зависимость к вашему `pom.xml` файл:
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Настройка Gradle
Для пользователей Gradle включите это в свой `build.gradle` файл:
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### Прямая загрузка
Альтернативно, загрузите последнюю версию с сайта [GroupDocs.Signature для релизов Java](https://releases.groupdocs.com/signature/java/).

### Приобретение лицензии
Вы можете начать с бесплатной пробной версии GroupDocs.Signature, чтобы оценить её возможности. Для длительного использования рассмотрите возможность приобретения лицензии или подачи заявки на временную лицензию на сайте сервиса.

## Руководство по внедрению
Данное руководство разделено на основные разделы, охватывающие шифрование данных, создание пользовательских подписей и настройку подписи с помощью QR-кода.

### Шифрование данных с помощью симметричного алгоритма
Шифрование данных гарантирует их безопасность при передаче и хранении. Вот как настроить симметричное шифрование с помощью GroupDocs.Signature:

#### Настройка симметричного шифрования
1. **Импорт необходимых пакетов:**
   ```java
   import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
   import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
   import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
   ```
2. **Инициализируйте объект шифрования:**
   Используйте безопасный ключ и соль для шифрования. Заменить `"YOUR_SECURE_KEY"` с вашими собственными ключами.
   ```java
   String key = "YOUR_SECURE_KEY";
   String salt = "YOUR_SECURE_SALT";

   IDataEncryption encryption = new SymmetricEncryption(
       SymmetricAlgorithmType.Rijndael, 
       key, 
       salt
   );
   ```
   - **SymmetricAlgorithmType.Rijndael:** Это определяет тип используемого симметричного алгоритма.
   - **Ключ и соль:** Убедитесь, что они уникальны и безопасны для вашего приложения.

### Пользовательский класс подписи данных
Создание собственного класса позволяет эффективно управлять свойствами сигнатуры. Вот как это сделать:

#### Определение `DocumentSignatureData` Сорт
```java
class DocumentSignatureData {
    private String ID;
    private String Author;
    private Date Signed = new Date();
    private BigDecimal DataFactor = new BigDecimal(0.01);

    public String getID() { return ID; }
    public void setID(String value) { ID = value; }

    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }

    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }

    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```
- **Идентификатор, Автор, Подпись:** В этих полях хранятся метаданные подписи.
- **DataFactor:** Содержит числовое значение, соответствующее логике вашего приложения.

### Варианты подписи QR-кода
QR-коды — это компактный способ встраивания информации. Настройте их, используя пользовательские данные и шифрование:

#### Настройка подписей QR-кода
1. **Инициализировать `Signature` Объект:**
   ```java
   import com.groupdocs.signature.Signature;
   
   Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY");
   ```
2. **Настройте параметры QR-кода:**
   ```java
   import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
   import com.groupdocs.signature.options.sign.QrCodeSignOptions;
   import java.util.UUID;

   DocumentSignatureData documentSignature = new DocumentSignatureData();
   documentSignature.setID(UUID.randomUUID().toString());
   documentSignature.setAuthor(System.getenv("USERNAME"));
   documentSignature.setDataFactor(new BigDecimal("11.22"));

   QrCodeSignOptions options = new QrCodeSignOptions();
   options.setData(documentSignature);
   options.setEncodeType(QrCodeTypes.QR);
   options.setDataEncryption(encryption); // Использовать объект шифрования
   options.setHeight(100);
   options.setWidth(100);
   options.setVerticalAlignment(com.groupdocs.signature.domain.enums.VerticalAlignment.Bottom);
   options.setHorizontalAlignment(com.groupdocs.signature.domain.enums.HorizontalAlignment.Right);

   import com.groupdocs.signature.domain.Padding;
   Padding padding = new Padding();
   padding.setRight(10);
   padding.setBottom(10);
   options.setMargin(padding);
   ```
   - **Тип кодировки:** Задает формат QR-кода.
   - **Выравнивание и поля:** Настройте внешний вид QR-кода в документе.

### Пример использования
Чтобы подписать документ с настроенными вами параметрами:
```java
signature.sign("YOUR_OUTPUT_DIRECTORY/QRCodeEncryptedObject.pdf\