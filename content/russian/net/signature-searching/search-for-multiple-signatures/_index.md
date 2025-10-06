---
"description": "Узнайте, как искать несколько типов подписей в документах с помощью GroupDocs.Signature для .NET. Подробное руководство с примерами кода для повышения безопасности документов."
"linktitle": "Поиск нескольких подписей"
"second_title": "GroupDocs.Signature .NET API"
"title": "Поиск нескольких типов подписей в документах"
"url": "/ru/net/signature-searching/search-for-multiple-signatures/"
"weight": 14
type: docs
---
## Введение

В современных системах управления документами возможность поиска и проверки нескольких типов подписей в одном документе становится всё более важной. Организации часто используют различные типы подписей, такие как цифровые подписи, текстовые подписи, штрихкоды, QR-коды и другие, для повышения безопасности документов и оптимизации процессов проверки. GroupDocs.Signature для .NET предоставляет мощную платформу, позволяющую разработчикам реализовывать комплексный поиск подписей в документах различных форматов.

В этом руководстве вы узнаете о процессе поиска нескольких типов подписей в документах с использованием GroupDocs.Signature для .NET, а также получите подробные объяснения и практические примеры кода.

## Предпосылки

Прежде чем приступать к реализации функции поиска по нескольким сигнатурам, убедитесь, что выполнены следующие предварительные условия:

1. Среда разработки: Visual Studio или любая предпочитаемая среда разработки .NET, установленная в вашей системе.
  
2. GroupDocs.Signature для .NET: Загрузите и установите библиотеку GroupDocs.Signature для .NET с сайта [здесь](https://releases.groupdocs.com/signature/net/).

3. Базовые знания C#: знакомство с языком программирования C# и концепциями .NET Framework.

4. Образцы документов: подготовьте тестовые документы, содержащие различные типы подписей для целей тестирования.

## Импорт пространств имен

Начните с импорта необходимых пространств имен для доступа к функциональности GroupDocs.Signature:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Теперь давайте разобьем процесс поиска нескольких типов подписей на понятные и выполнимые шаги:

## Шаг 1: Загрузите документ

Сначала загрузите документ, содержащий подписи, которые вы хотите найти:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Здесь будет добавлен код поиска мультиподписи.
}
```

## Шаг 2: Определите параметры поиска для различных типов подписей

Создайте параметры поиска для каждого типа подписи, который вы хотите найти:

```csharp
// Определить параметры поиска для текстовых подписей
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,  // Поиск на всех страницах
    Text = "Signature",  // Необязательно: текст для поиска
    MatchType = TextMatchType.Contains  // Критерии соответствия
};

// Определить параметры поиска для цифровых подписей
DigitalSearchOptions digitalOptions = new DigitalSearchOptions
{
    AllPages = true
};

// Определить параметры поиска для подписей штрих-кода
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
{
    AllPages = true,
    Text = "123456",  // Дополнительно: текст штрихкода для сопоставления
    MatchType = TextMatchType.Exact  // Критерии соответствия
};

// Определите параметры поиска для подписей QR-кода
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
{
    AllPages = true,
    Text = "John",  // Необязательно: текст QR-кода для сопоставления
    MatchType = TextMatchType.Contains  // Критерии соответствия
};

// Определить параметры поиска для сигнатур метаданных
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```

## Шаг 3: Добавьте параметры в коллекцию

Добавить все параметры поиска в коллекцию:

```csharp
// Создайте список для хранения всех вариантов поиска
List<SearchOptions> searchOptions = new List<SearchOptions>
{
    textOptions,
    digitalOptions,
    barcodeOptions,
    qrCodeOptions,
    metadataOptions
};
```

## Шаг 4: Выполните поиск и обработайте результаты

Выполните поиск, используя комбинированные параметры поиска, и обработайте результаты:

```csharp
// Поиск всех типов подписей с использованием заданных параметров
SearchResult result = signature.Search(searchOptions);

// Проверьте, были ли найдены подписи
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
    
    // Перебрать найденные сигнатуры
    foreach (var foundSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}, ID: {foundSignature.SignatureId}");
        
        // Типы подписей, специфичные для процесса
        if (foundSignature is TextSignature textSignature)
        {
            Console.WriteLine($"Text: '{textSignature.Text}'");
        }
        else if (foundSignature is BarcodeSignature barcodeSignature)
        {
            Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
        }
        else if (foundSignature is QrCodeSignature qrCodeSignature)
        {
            Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
        }
        else if (foundSignature is DigitalSignature digitalSignature)
        {
            Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
        }
        else if (foundSignature is MetadataSignature metadataSignature)
        {
            Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
        }
    }
}
else
{
    Console.WriteLine("No signatures were found in the document.");
}
```

## Полный пример

Вот полный рабочий пример, демонстрирующий поиск нескольких типов подписей в документе:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace MultiSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // Путь к документу
            string filePath = "sample_multiple_signatures.docx";
            
            // Инициализировать экземпляр подписи
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // Определить параметры поиска для текстовых подписей
                    TextSearchOptions textOptions = new TextSearchOptions
                    {
                        AllPages = true,
                        MatchType = TextMatchType.Contains
                    };

                    // Определить параметры поиска для цифровых подписей
                    DigitalSearchOptions digitalOptions = new DigitalSearchOptions
                    {
                        AllPages = true
                    };

                    // Определить параметры поиска для подписей штрих-кода
                    BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
                    {
                        AllPages = true
                    };

                    // Определите параметры поиска для подписей QR-кода
                    QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
                    {
                        AllPages = true
                    };

                    // Определить параметры поиска для сигнатур метаданных
                    MetadataSearchOptions metadataOptions = new MetadataSearchOptions();

                    // Создайте список для хранения всех вариантов поиска
                    List<SearchOptions> searchOptions = new List<SearchOptions>
                    {
                        textOptions,
                        digitalOptions,
                        barcodeOptions,
                        qrCodeOptions,
                        metadataOptions
                    };

                    // Поиск всех типов подписей
                    SearchResult result = signature.Search(searchOptions);

                    // Проверьте, были ли найдены подписи
                    if (result.Signatures.Count > 0)
                    {
                        Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
                        
                        // Обработка результатов по типу подписи
                        foreach (var foundSignature in result.Signatures)
                        {
                            Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}");
                            
                            // Типы подписей, специфичные для процесса
                            switch (foundSignature.SignatureType)
                            {
                                case SignatureType.Text:
                                    var textSignature = foundSignature as TextSignature;
                                    Console.WriteLine($"Text: '{textSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Barcode:
                                    var barcodeSignature = foundSignature as BarcodeSignature;
                                    Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.QrCode:
                                    var qrCodeSignature = foundSignature as QrCodeSignature;
                                    Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Digital:
                                    var digitalSignature = foundSignature as DigitalSignature;
                                    Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
                                    break;
                                    
                                case SignatureType.Metadata:
                                    var metadataSignature = foundSignature as MetadataSignature;
                                    Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
                                    break;
                            }
                            
                            Console.WriteLine(); // Добавить перенос строки между подписями
                        }
                    }
                    else
                    {
                        Console.WriteLine("No signatures were found in the document.");
                    }
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"Error occurred: {ex.Message}");
                }
            }
            
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## Расширенные методы поиска по нескольким сигнатурам

### Фильтрация результатов поиска

Вы можете реализовать расширенную фильтрацию, чтобы сузить результаты поиска:

```csharp
// Фильтровать результаты по номеру страницы
var signaturesOnFirstPage = result.Signatures.FindAll(s => s.PageNumber == 1);

// Фильтровать результаты по типу подписи
var digitalSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.Digital);
var qrCodeSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.QrCode);

// Фильтровать текстовые подписи, содержащие определенный контент
var approvalSignatures = result.Signatures
    .FindAll(s => s is TextSignature && ((TextSignature)s).Text.Contains("Approved"));
```

### Проверка нескольких подписей

Реализуйте логику проверки для различных типов подписей:

```csharp
bool ValidateAllSignatures(SearchResult result)
{
    bool isDocumentValid = true;
    
    // Проверьте, имеет ли документ действительную цифровую подпись.
    bool hasValidDigitalSignature = result.Signatures
        .Any(s => s is DigitalSignature && ((DigitalSignature)s).IsValid);
    
    if (!hasValidDigitalSignature)
    {
        Console.WriteLine("Warning: Document does not contain a valid digital signature");
        isDocumentValid = false;
    }
    
    // Проверьте, есть ли в документе требуемый QR-код.
    bool hasRequiredQRCode = result.Signatures
        .Any(s => s is QrCodeSignature && ((QrCodeSignature)s).Text.Contains("Auth-Code"));
    
    if (!hasRequiredQRCode)
    {
        Console.WriteLine("Warning: Document does not contain the required authentication QR code");
        isDocumentValid = false;
    }
    
    return isDocumentValid;
}
```

### Поиск с пользовательской обработкой

Вы можете определить собственную логику обработки для операций поиска:

```csharp
// Создавайте параметры поиска с помощью пользовательской обработки
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,
    
    // Определить пользовательскую обработку с помощью делегата
    ProcessCompleted = (signature) =>
    {
        // Пользовательская логика проверки — принимаются только подписи на указанных страницах
        TextSignature textSignature = signature as TextSignature;
        return textSignature != null && (textSignature.PageNumber == 1 || textSignature.PageNumber == 2);
    }
};
```

## Заключение

В этом подробном руководстве мы рассмотрели, как искать подписи разных типов в документах с помощью GroupDocs.Signature для .NET. Теперь вы обладаете знаниями для реализации надежной функции поиска подписей в своих приложениях .NET: от настройки параметров поиска для различных типов подписей до обработки и проверки результатов.

Возможность одновременного поиска нескольких типов подписей улучшает процессы проверки документов, усиливает меры безопасности и оптимизирует рабочие процессы проверки документов. GroupDocs.Signature предоставляет мощную и гибкую платформу для работы с различными типами подписей в документах разных форматов, что делает её отличным выбором для приложений обработки документов.

## Часто задаваемые вопросы

### Можно ли искать подписи в документах, защищенных паролем?

Да, GroupDocs.Signature поддерживает поиск подписей в документах, защищённых паролем. Вы можете указать пароль при инициализации. `Signature` объект:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Поиск подписей
}
```

### Какие форматы документов поддерживаются для поиска по подписи?

GroupDocs.Signature поддерживает широкий спектр форматов документов, включая PDF, документы Microsoft Office (Word, Excel, PowerPoint), форматы OpenOffice, изображения и многое другое.

### Можно ли ограничить поиск определенными страницами документа?

Да, у каждого типа параметра поиска есть свойства, позволяющие указать, на каких страницах выполнять поиск:

```csharp
TextSearchOptions options = new TextSearchOptions
{
    AllPages = false,  // Не искать на всех страницах
    PageNumber = 1,    // Искать только на странице 1
    
    // Или укажите несколько страниц
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } }
};
```

### Как оптимизировать производительность поиска в больших документах?

Для больших документов вы можете оптимизировать производительность следующими способами:

1. Ограничение поиска определенными страницами или диапазонами страниц
2. Использование более конкретных критериев поиска для уменьшения количества потенциальных совпадений
3. Реализация пагинации при отображении результатов
4. Поиск по одному типу подписи за раз, если вам не нужны одновременные результаты

### Можно ли расширить GroupDocs.Signature для поддержки пользовательских типов подписей?

Хотя GroupDocs.Signature обеспечивает встроенную поддержку распространенных типов подписей, вы можете расширить его функциональность следующими способами:

1. Создание классов пользовательских параметров поиска, полученных из `SearchOptions`
2. Реализация пользовательской логики обработки с использованием `ProcessCompleted` делегат
3. Разработка классов-оболочек, объединяющих множественные поиски по сигнатурам с расширенной бизнес-логикой

## Смотрите также

* [Справочник API](https://reference.groupdocs.com/signature/net/)
* [Примеры кода на GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Документация по продукту](https://docs.groupdocs.com/signature/net/)
* [Страница продукта](https://products.groupdocs.com/signature/net/)
* [Загрузить последнюю версию](https://releases.groupdocs.com/signature/net/)
* [Статьи блога](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Бесплатный форум поддержки](https://forum.groupdocs.com/c/signature/13)
* [Временная лицензия](https://purchase.groupdocs.com/temporary-license/)