---
"date": "2025-05-08"
"description": "Узнайте, как реализовать подпись QR-кода Java с помощью GroupDocs.Signature. Повысьте безопасность документов, настройте параметры подписи и применяйте пользовательское шифрование в своих приложениях Java."
"title": "Руководство по подписанию QR-кода Java&#58; защитите свои документы с помощью GroupDocs.Signature"
"url": "/ru/java/qr-code-signatures/java-qr-code-signing-groupdocs-signature/"
"weight": 1
type: docs
---
# Реализация подписи QR-кода Java с помощью GroupDocs.Signature для Java

## Введение

Повысьте безопасность своих цифровых документов, встроив QR-коды в приложения Java. GroupDocs.Signature для Java позволяет эффективно гарантировать подлинность и отслеживаемость документов. Это руководство поможет вам создать собственные подписи данных, настроить параметры подписи QR-кодов и защитить документы с помощью надежного шифрования.

**Что вы узнаете:**
- Как создать пользовательский класс подписи данных с помощью GroupDocs.Signature
- Настройка параметров подписи QR-кода в приложениях Java
- Подписание документов с помощью QR-кодов и применение пользовательского шифрования

Давайте углубимся в предварительные требования и начнем интегрировать эту функциональность в ваши проекты!

## Предпосылки

Прежде чем начать, убедитесь, что в вашей среде разработки установлены необходимые библиотеки и зависимости.

### Требуемые библиотеки и версии

Чтобы реализовать GroupDocs.Signature для Java, включите следующую зависимость:

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
implementation 'com.groupdocs:groupdocs-signation:23.12'
```

Вы также можете загрузить последнюю версию непосредственно с сайта [GroupDocs.Signature для релизов Java](https://releases.groupdocs.com/signature/java/).

### Требования к настройке среды

- Убедитесь, что у вас установлен рабочий комплект разработки Java (JDK).
- Настройте интегрированную среду разработки (IDE), например IntelliJ IDEA или Eclipse.

### Необходимые знания

- Базовые знания программирования на Java и концепций объектно-ориентированного программирования.
- Знакомство с обработкой зависимостей с помощью Maven или Gradle.

## Настройка GroupDocs.Signature для Java

Для начала настройте GroupDocs.Signature в своем проекте, следуя инструкциям по установке выше, чтобы включить его в конфигурацию сборки.

### Этапы получения лицензии

GroupDocs предлагает различные варианты лицензирования:
- **Бесплатная пробная версия**: Протестируйте все функции без ограничений.
- **Временная лицензия**: Получите лицензию для целей оценки.
- **Покупка**: Приобретите полную лицензию для коммерческого использования.

После загрузки инициализируйте GroupDocs.Signature следующим образом:

```java
import com.groupdocs.signature.Signature;

class InitializeGroupDocs {
    public static void main(String[] args) {
        Signature signature = new Signature("path/to/your/document");
        // Теперь вы можете начать использовать объект подписи для работы с документами.
    }
}
```

## Руководство по внедрению

Давайте разобьем процесс внедрения на управляемые этапы, сосредоточившись на ключевых функциях.

### Пользовательский класс подписи данных

#### Обзор
Создайте собственный класс для хранения данных подписи, таких как идентификатор, автор, дата подписания и другие данные. Это гарантирует, что все необходимые метаданные будут включены в ваши подписи.

#### Пошаговая реализация

**Определить класс DocumentSignatureData**

```java
import com.groupdocs.signature.domain.extensions.serialization.FormatAttribute;
import java.util.Date;
import java.math.BigDecimal;

class DocumentSignatureData {
    @FormatAttribute(propertyName = "SignID")
    public String ID; // Уникальный идентификатор подписи
    
    public String getID() { return ID; }
    public void setID(String value) { ID = value; }
    
    @FormatAttribute(propertyName = "SAuth")
    public final String Author; // Автор документа
    
    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }
    
    @FormatAttribute(propertyName = "SDate", propertyFormat = "yyyy-MM-dd")
    public final Date Signed = new Date(); // Дата и время подписания
    
    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }
    
    @FormatAttribute(propertyName = "SDFact", propertyFormat = "N2")
    public final BigDecimal DataFactor = new BigDecimal(0.01); // Дополнительный фактор данных для подписи
    
    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```

**Объяснение:**
- **Атрибут Формата**: Аннотирует свойства для настройки сериализации.
- **Характеристики**: Соберите основные данные, такие как уникальный идентификатор, имя автора, дату подписания и фактор данных.

### Конфигурация параметров подписи QR-кода

#### Обзор
Настройте параметры подписи QR-кода, чтобы определить, как ваши QR-коды будут отображаться в документах, включая размер, выравнивание и отступы.

#### Пошаговая реализация

**Определите класс QrCodeSignOptionsConfig**

```java
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

class QrCodeSignOptionsConfig {
    public static QrCodeSignOptions setupQrCodeSignOptions(DocumentSignatureData documentSignature) {
        QrCodeSignOptions options = new QrCodeSignOptions();
        
        // Сериализовать пользовательский объект данных в QR-код
        options.setData(documentSignature);
        
        // Укажите тип QR-кода
        options.setEncodeType(QrCodeTypes.QR);
        
        // Настройте отступы для выравнивания
        Padding padding = new Padding();
        padding.setRight(10); // Правый отступ в пикселях
        padding.setBottom(10); // Нижний отступ в пикселях
        options.setMargin(padding);
        
        // Определите размер и положение QR-кода
        options.setHeight(100);
        options.setWidth(100);
        options.setVerticalAlignment(VerticalAlignment.Bottom);
        options.setHorizontalAlignment(HorizontalAlignment.Right);
        
        return options;
    }
}
```

**Объяснение:**
- **QrCodeSignOptions**: управляет отображением QR-кода, включая его размер и положение.
- **Прокладка**Изменяет выравнивание в документе.

### Подписание документов с помощью QR-кода и пользовательского шифрования

#### Обзор
Комбинируйте QR-коды и шифрование для безопасной подписи документов. Это гарантирует целостность и конфиденциальность данных.

#### Пошаговая реализация

**Подписать документ с помощью QR-кода**

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.exception.GroupDocsSignatureException;

import java.util.UUID;

class SignDocumentWithQRCode {
    public static void signDocument(String filePath, String outputFilePath) throws Exception {
        try {
            Signature signature = new Signature(filePath);

            // Пользовательская стратегия шифрования XOR
            IDataEncryption encryption = new CustomXOREncryption();

            // Настройте пользовательский объект данных подписи документа
            DocumentSignatureData documentSignature = new DocumentSignatureData();
            documentSignature.setID(UUID.randomUUID().toString());
            documentSignature.setAuthor(System.getenv("USERNAME"));
            documentSignature.setSigned(new Date());
            documentSignature.setDataFactor(new BigDecimal("11.22"));

            // Настройка параметров QR-кода
            QrCodeSignOptions options = QrCodeSignOptionsConfig.setupQrCodeSignOptions(documentSignature);

            // Применить шифрование к данным в QR-коде
            options.setDataEncryption(encryption);

            // Подпишите и сохраните документ
            signature.sign(outputFilePath, options);
        } catch (Exception e) {
            throw new GroupDocsSignatureException(e.getMessage());
        }
    }
}
```

**Объяснение:**
- **CustomXOREncryption**: реализует специальную стратегию шифрования для защиты данных QR-кода.
- **UUID**: Генерирует уникальный идентификатор для каждой подписи.