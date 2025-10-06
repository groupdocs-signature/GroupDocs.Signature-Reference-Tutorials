---
"date": "2025-05-07"
"description": "Узнайте, как подписывать PDF-документы QR-кодами HIBC с помощью GroupDocs.Signature для .NET. В этом руководстве рассматриваются коды LIC и PAS, включая QR-код, Aztec Code и DataMatrix."
"title": "Как подписывать документы с помощью QR-кодов HIBC с помощью GroupDocs.Signature для .NET&#58; подробное руководство"
"url": "/ru/net/qr-code-signatures/sign-documents-hibc-qr-groupdocs-dotnet/"
"weight": 1
type: docs
---
# Как подписывать документы с помощью QR-кодов HIBC с помощью GroupDocs.Signature для .NET

## Введение

В современной динамичной бизнес-среде обеспечение подлинности и целостности документов имеет первостепенное значение. Работаете ли вы с фармацевтическими препаратами, изделиями медицинского назначения или логистикой, наличие безопасного метода подписания и отслеживания документов может сэкономить время и предотвратить ошибки. Войти **GroupDocs.Signature для .NET**— мощная библиотека, предназначенная для оптимизации процессов управления документами путем обеспечения бесшовной интеграции QR-кодов HIBC в ваши документы.

В этом руководстве мы рассмотрим, как использовать GroupDocs.Signature для .NET для подписи PDF-документов различными типами QR-кодов HIBC — LIC (лицензия) и PAS (система аутентификации продукта), включая QR-код, Aztec Code и DataMatrix. К концу обучения вы получите чёткое представление о реализации этих решений в своих .NET-приложениях.

**Что вы узнаете:**
- Как настроить GroupDocs.Signature для .NET
- Внедрение QR-кодов HIBC LIC, кодов Aztec и DataMatrix
- Добавление QR-кодов HIBC PAS, кодов Aztec и DataMatrix
- Практические варианты использования и возможности интеграции

Давайте рассмотрим предварительные условия, прежде чем приступить к реализации этих функций.

## Предпосылки

Прежде чем начать кодирование, убедитесь, что у вас есть следующее:

- **Окружение .NET**: Убедитесь, что в вашей системе установлен .NET (предпочтительно .NET Core или .NET 5/6+).
- **GroupDocs.Signature для .NET**: Эта библиотека станет нашим основным инструментом. Вы можете установить её через NuGet.
- **Базовые знания программирования**: Рекомендуется знакомство с C# и работой с файлами в .NET.

### Необходимые библиотеки

Чтобы использовать GroupDocs.Signature для .NET, вам необходимо добавить пакет одним из следующих методов:

**.NET CLI**
```bash
dotnet add package GroupDocs.Signature
```

**Менеджер пакетов**
```powershell
Install-Package GroupDocs.Signature
```

**Пользовательский интерфейс менеджера пакетов NuGet**
Найдите «GroupDocs.Signature» и установите последнюю версию.

### Приобретение лицензии

Для тестирования вы можете получить бесплатную пробную лицензию. Для длительного использования рассмотрите возможность приобретения подписки или запроса временной лицензии:

- **Бесплатная пробная версия**: Доступ [здесь](https://releases.groupdocs.com/signature/net/)
- **Временная лицензия**: Запрос на [эта ссылка](https://purchase.groupdocs.com/temporary-license/)

### Настройка среды

Настройте среду, убедившись, что ваш проект ориентирован на соответствующую версию .NET и имеет доступ к GroupDocs.Signature. Инициализируйте его в своем приложении, как показано ниже:

```csharp
using GroupDocs.Signature;
```

## Настройка GroupDocs.Signature для .NET

Чтобы начать использовать GroupDocs.Signature для .NET, вам необходимо установить библиотеку и настроить базовую конфигурацию в вашем проекте.

### Установка

Чтобы добавить GroupDocs.Signature в свой проект, используйте один из описанных выше способов. После установки убедитесь, что ваш проект настроен на его использование, указав ссылку на него в файлах кода.

### Инициализация лицензии

После получения лицензии инициализируйте ее следующим образом:

```csharp
SignatureConfig signConfig = new SignatureConfig();
signConfig.LicensePath = "path/to/your/license.lic";
Signature signature = new Signature("Sample.pdf", signConfig);
```

Эта настройка позволит вам получить доступ ко всем функциям GroupDocs.Signature без ограничений.

## Руководство по внедрению

Теперь давайте перейдем к реализации каждой функции с использованием QR-кодов HIBC с GroupDocs.Signature для .NET.

### Подписать документ с помощью QR-кода HIBC LIC

#### Обзор

Подписание документа QR-кодом HIBC LIC обеспечивает соответствие требованиям и отслеживаемость при лицензировании. В этом разделе вы узнаете, как создать QR-код и встроить его в PDF-документы.

#### Шаги реализации

##### Шаг 1: Настройте исходный и выходной пути

Определите, где находится исходный документ и где следует сохранить подписанный вывод:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICQR");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICQR.pdf");
```

##### Шаг 2: Создайте параметры подписи QR-кода

Настройте свой QR-код, используя определенный текст и настройки:

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcLic_QR_Options = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR)
    {
        Left = 1,
        Top = 1,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    // Подпишите документ, используя эти параметры.
    signature.Sign(destinFilePath, hibcLic_QR_Options);
}
```

**Объяснение**: 
- `QrCodeSignOptions` Настраивает внешний вид и содержание QR-кода. Здесь мы указываем тип QR-кода HIBC LIC и размещаем его в документе.
- `ReturnContent` если установлено значение true, можно получить визуализированное изображение подписанного документа.

#### Советы по устранению неполадок

- Убедитесь, что путь к документу указан правильно.
- Убедитесь, что GroupDocs.Signature имеет надлежащую лицензию для полной функциональности.

### Подписать документ с кодом HIBC LIC Aztec

#### Обзор

Код Aztec предлагает ещё одну форму кодирования, подходящую для хранения информации высокой плотности. В этом разделе рассматривается внедрение кода Aztec в документы с помощью GroupDocs.Signature.

#### Шаги реализации

##### Шаг 1: Настройка путей

Аналогично предыдущей функции определите пути к файлам:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICAztec");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICAztec.pdf");
```

##### Шаг 2: Настройте параметры кода Aztec

Настройте свой код Aztec с помощью GroupDocs.Signature:

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcLic_AZ_Options = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec)
    {
        Left = 1,
        Top = 200,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    signature.Sign(destinFilePath, hibcLic_AZ_Options);
}
```

**Объяснение**: 
- The `QrCodeSignOptions` здесь снова используется, но с типом кода Aztec.
- Позиционирование (`Top`, `Left`) и настройки поиска контента аналогичны QR-кодам.

#### Советы по устранению неполадок

- Убедитесь, что пути к файлам указаны верно.
- Убедитесь, что версия GroupDocs.Signature поддерживает типы Aztec Code.

### Подписать документ с помощью HIBC LIC DataMatrix

#### Обзор

Код DataMatrix предоставляет ещё один надёжный метод хранения данных. В этом разделе показано, как интегрировать DataMatrix в PDF-документы.

#### Шаги реализации

##### Шаг 1: Задайте пути к файлам

Как и прежде, укажите, где находятся ваши файлы:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICDataMatrix");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICDataMatrix.pdf");
```

##### Шаг 2: Создайте параметры подписи DataMatrix

Настройте и примените код DataMatrix:

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcLic_DM_Options = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix)
    {
        Left = 1,
        Top = 400,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    signature.Sign(destinFilePath, hibcLic_DM_Options);
}
```

**Объяснение**: 
- `QrCodeSignOptions` используется для настройки внешнего вида и содержимого кода DataMatrix.
- Позиционирование (`Top`, `Left`) и настройки поиска следуют той же схеме, что и предыдущие коды.

#### Советы по устранению неполадок

- Убедитесь, что все пути к файлам указаны правильно.
- Убедитесь, что GroupDocs.Signature поддерживает типы кодов DataMatrix в вашей версии.

### Подписать документ с помощью QR-кода HIBC PAS

#### Обзор

Подписание документов QR-кодом HIBC PAS улучшает отслеживание и контроль продукции. В этом разделе описывается, как встроить QR-код PAS в PDF-файлы с помощью GroupDocs.Signature.

#### Шаги реализации

##### Шаг 1: Настройте исходный и выходной пути

Определите, где находится исходный документ и где следует сохранить подписанный вывод:

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCPASQR");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCPASQR.pdf");
```

##### Шаг 2: Создайте параметры подписи QR-кода

Настройте свой QR-код PAS, используя определенный текст и настройки:

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcPas_QR_Options = new QrCodeSignOptions("PAS123456789012", QrCodeTypes.HIBCPASQR)
    {
        Left = 1,
        Top = 500,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    // Подпишите документ, используя эти параметры.
    signature.Sign(destinFilePath, hibcPas_QR_Options);
}
```

**Объяснение**: 
- `QrCodeSignOptions` настроен для типа QR-кода HIBC PAS и размещен на документе.
- `ReturnContent` при значении true извлекает визуализированное изображение подписанного документа.

#### Советы по устранению неполадок

- Убедитесь, что все пути указаны правильно.
- Убедитесь, что GroupDocs.Signature поддерживает типы QR-кодов PAS в вашей версии.

### Заключение

Следуя этому руководству, вы сможете эффективно интегрировать QR-коды HIBC LIC и PAS в PDF-документы с помощью GroupDocs.Signature для .NET. Этот процесс повышает безопасность документов, отслеживаемость и соответствие требованиям в различных отраслях. Для получения дополнительной информации о настройке и расширенных функциях см. [Документация GroupDocs](https://docs.groupdocs.com/signature/net/).