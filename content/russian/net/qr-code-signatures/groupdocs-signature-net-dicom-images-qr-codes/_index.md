---
"date": "2025-05-07"
"description": "Узнайте, как подписывать изображения DICOM QR-кодами с помощью GroupDocs.Signature для .NET. Это руководство посвящено настройке, внедрению и проверке подписей QR-кодов в медицинской визуализации."
"title": "Как подписывать изображения DICOM с помощью QR-кодов с помощью GroupDocs.Signature для .NET&#58; подробное руководство"
"url": "/ru/net/qr-code-signatures/groupdocs-signature-net-dicom-images-qr-codes/"
"weight": 1
---

# Как подписывать изображения DICOM с помощью QR-кодов с помощью GroupDocs.Signature для .NET: подробное руководство

Ищете безопасный метод аутентификации файлов DICOM? Это подробное руководство покажет вам, как использовать GroupDocs.Signature для .NET для интеграции QR-кодов в изображения DICOM. Это руководство идеально подходит для медицинских работников, разработчиков и всех, кто работает с цифровыми медицинскими документами, и охватывает все этапы от настройки до внедрения.

## Что вы узнаете:
- Настройка среды разработки с помощью GroupDocs.Signature для .NET.
- Пошаговая инструкция по подписанию DICOM-изображений с помощью QR-кодов.
- Методы проверки и поиска подписей QR-кодов в файлах DICOM.
- Методы создания предварительных версий подписанных документов для целей проверки.
- Лучшие практики оптимизации производительности и эффективного управления ресурсами.

Начнем с предпосылок!

## Предпосылки

Чтобы использовать GroupDocs.Signature для .NET, убедитесь, что ваша среда готова. Вот что вам понадобится:

### Требуемые библиотеки и версии
- **GroupDocs.Signature для .NET**Обеспечьте совместимость с вашей платформой .NET.

### Требования к настройке среды
- Среда разработки на Windows или Linux.
- Установлена Visual Studio или другая совместимая с .NET IDE.

### Необходимые знания
- Базовые знания программирования на языке C#.
- Знакомство с файловым вводом/выводом в приложениях .NET.

## Настройка GroupDocs.Signature для .NET

Установите библиотеку GroupDocs.Signature любым удобным для вас способом:

**Использование .NET CLI:**
```bash
dotnet add package GroupDocs.Signature
```

**Менеджер пакетов:**
```powershell
Install-Package GroupDocs.Signature
```

**Пользовательский интерфейс менеджера пакетов NuGet:**
- Найдите «GroupDocs.Signature» и установите последнюю версию.

### Приобретение лицензии

Начните с бесплатной пробной версии, чтобы изучить возможности. Для длительного использования рассмотрите возможность приобретения временной или полной лицензии. [GroupDocs](https://purchase.groupdocs.com/buy).

После установки инициализируйте библиотеку:

```csharp
using GroupDocs.Signature;
// Инициализируйте объект Signature, используя путь к файлу DICOM.
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample.dicom");
```

## Руководство по внедрению

### Подписать изображение DICOM с помощью QR-кода

#### Обзор
Добавьте подписи с помощью QR-кодов для обеспечения подлинности и прослеживаемости медицинских документов.

**Шаг 1: Инициализация объекта подписи**

```csharp
string filePath = "YOUR_DOCUMENT_DIRECTORY\\sample.dicom";
using (Signature signature = new Signature(filePath))
{
    // Продолжайте операции по подписанию...
}
```

**Шаг 2: Создайте параметры подписи QR-кода**

Настройте такие свойства, как текст, размер и выравнивание.

```csharp
QrCodeSignOptions options = new QrCodeSignOptions("Patient #36363393. R: No-Issues")
{
    AllPages = true,
    Width = 100,
    Height = 100,
    VerticalAlignment = VerticalAlignment.Bottom,
    HorizontalAlignment = HorizontalAlignment.Right,
    Margin = new Padding() { Right = 5, Left = 5 }
};
```

**Шаг 3: Добавьте метаданные XMP**

Дополните документ дополнительными метаданными.

```csharp
DicomSaveOptions dicomSaveOptions = new DicomSaveOptions()
{
    XmpEntries = new List<DicomXmpEntry>() { new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4") }
};
```

**Шаг 4: Подпишите документ**

Выполните подписание и сохраните.

```csharp
SignResult signResult = signature.Sign("YOUR_OUTPUT_DIRECTORY\\SignedDicom", options, dicomSaveOptions);
```

### Получить информацию о документе

Извлекайте метаданные из подписанных файлов DICOM для обеспечения целостности данных.

**Обзор:**
Доступ к информации о документе и подписям метаданных XMP для проверки.

**Шаг 1: Извлечение информации о документе**

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    IDocumentInfo signedDocumentInfo = signature.GetDocumentInfo();
}
```

**Шаг 2: Итерация и печать данных XMP**

Отображение метаданных.

```csharp
foreach (var item in signedDocumentInfo.MetadataSignatures)
{
    Console.WriteLine(item.ToString());
}
```

### Проверка подписей DICOM

Проверка подлинности подписей QR-кодов на изображениях DICOM.

**Обзор:**
Убедитесь, что подписи являются правильными и подлинными.

**Шаг 1: Создайте QR-код. Проверьте параметры.**

Задайте параметры, соответствующие определенному тексту в QR-кодах.

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true,
    Text = "Patient #36363393",
    MatchType = TextMatchType.Contains
};
```

**Шаг 2: Проверка подписей**

Проверьте, соответствуют ли подписи критериям.

```csharp
VerificationResult result = signature.Verify(options);

if (result.IsValid)
{
    Console.WriteLine($"DICOM {filePath} has {result.Succeeded.Count} successfully verified signatures!");
}
```

### Поиск подписей в DICOM

Найдите подписи QR-кодов на подписанных изображениях DICOM.

**Обзор:**
Эффективно находите все подписи QR-кодов для управления подлинностью документов.

**Шаг 1: Поиск подписей QR-кода**

```csharp
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

**Шаг 2: Повторите и распечатайте данные подписи**

Просмотрите сведения о каждой найденной подписи.

```csharp
foreach (var QrCodeSignature in signatures)
{
    Console.WriteLine($"QRCode signature found at page {QrCodeSignature.PageNumber} with type {QrCodeSignature.EncodeType.TypeName} and text {QrCodeSignature.Text}");
}
```

### Создать предварительный просмотр подписанного DICOM

Создайте визуальные превью для проверки.

**Обзор:**
Создавайте предварительные просмотры изображений для проверки контента без специализированного программного обеспечения.

**Шаг 1: Определение методов потока**

Настройте методы управления потоком файлов во время создания предварительного просмотра.

```csharp
Stream CreatePageStream(PreviewPageData pageData)
{
    string imageFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignDicomImageAdvanced", $"preview-{pageData.PageNumber}.jpg");
    var folder = Path.GetDirectoryName(imageFilePath);
    if (!Directory.Exists(folder))
    {
        Directory.CreateDirectory(folder);
    }
    return new FileStream(imageFilePath, FileMode.Create);
}

void ReleasePageStream(PreviewPageData pageData, Stream pageStream)
{
    pageStream.Dispose();
}
```

**Шаг 2: Создание превью**

Выполните процесс создания предварительного просмотра.

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    PreviewOptions previewOption = new PreviewOptions(CreatePageStream, ReleasePageStream)
    {
        PreviewFormat = PreviewOptions.PreviewFormats.PNG,
    };

    signature.GeneratePreview(previewOption);
}
```

## Практические применения

1. **Управление медицинскими записями**: Аутентификация записей пациентов с помощью подписей QR-кодов для обеспечения соответствия требованиям.
2. **Аудиторские следы в системах здравоохранения**: Отслеживайте изменения документов и проверяйте их подлинность с помощью QR-кодов.
3. **Безопасный обмен данными**: Обеспечьте безопасный обмен медицинскими изображениями с помощью внедрения цифровых подписей.
4. **Проверка соответствия**: Регулярно проверяйте целостность файлов DICOM на предмет соответствия требованиям законодательства.
5. **Интеграция с системами электронных медицинских карт**: Простая интеграция подписанных файлов DICOM в системы электронных медицинских карт (ЭМК) для оптимизации операций.