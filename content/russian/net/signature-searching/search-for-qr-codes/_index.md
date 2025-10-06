---
"description": "Узнайте, как эффективно искать QR-коды в документах с помощью GroupDocs.Signature для .NET с помощью этого подробного пошагового руководства и примеров кода."
"linktitle": "Поиск QR-кодов"
"second_title": "GroupDocs.Signature .NET API"
"title": "Поиск подписей QR-кодов в документах"
"url": "/ru/net/signature-searching/search-for-qr-codes/"
"weight": 15
type: docs
---
## Введение

В современной экосистеме цифровых документов QR-коды стали бесценным инструментом для встраивания информации, аутентификации и повышения безопасности документов. GroupDocs.Signature для .NET предоставляет разработчикам мощный API для поиска и извлечения QR-кодов из документов различных форматов, обеспечивая расширенные возможности анализа и проверки документов в приложениях .NET.

Это подробное руководство проведет вас через процесс внедрения функции поиска по QR-коду с использованием GroupDocs.Signature для .NET, предоставляя понятные объяснения, пошаговые инструкции и практические примеры кода, которые вы сможете интегрировать в свои собственные приложения.

## Предпосылки

Прежде чем приступить к поиску подписи QR-кода, убедитесь, что у вас выполнены следующие предварительные условия:

1. GroupDocs.Signature для .NET SDK: Загрузите и установите SDK с сайта [страница загрузки](https://releases.groupdocs.com/signature/net/).

2. Среда разработки: настройте среду разработки .NET, например Visual Studio, с установленным .NET Framework или .NET Core.

3. Базовые знания: знакомство с программированием на языке C# и концепциями разработки .NET.

4. Образцы документов: Подготовьте тестовые документы, содержащие QR-коды для проверки и тестирования.

## Импорт пространств имен

Начните с импорта необходимых пространств имен для доступа к функциональности GroupDocs.Signature:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;
```

Теперь давайте разберем процесс поиска QR-кодов на понятные и простые шаги:

## Шаг 1: Определите путь к документу

Сначала укажите путь к документу, содержащему QR-коды, которые вы хотите найти:

```csharp
string filePath = "sample_multiple_signatures.docx";
```

## Шаг 2: Инициализация объекта подписи

Создайте экземпляр `Signature` класс, передавая путь к документу:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Здесь будет добавлен код поиска QR-кода.
}
```

## Шаг 3: Поиск подписей QR-кода

Используйте `Search` метод с соответствующим типом подписи для поиска QR-кодов в документе:

```csharp
// Поиск подписей QR-кодов в документе
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

## Шаг 4: Обработка и отображение результатов

Просмотрите найденные подписи QR-кодов и получите доступ к их свойствам:

```csharp
// Отображать информацию о найденных QR-кодах
Console.WriteLine($"\nSource document contains {signatures.Count} QR code signature(s):");

foreach (var qrCodeSignature in signatures)
{
    Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
    Console.WriteLine($"Content: {qrCodeSignature.Text}");
    Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
    Console.WriteLine();
}
```

## Полный пример

Вот подробный рабочий пример, демонстрирующий весь процесс поиска QR-кодов в документе:

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;

namespace QrCodeSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // Путь к документу — обновите, указав путь к файлу
            string filePath = "sample_multiple_signatures.docx";
            
            // Инициализировать экземпляр подписи
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // Поиск подписей QR-кода в документе
                    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
                    
                    // Показать результаты поиска
                    Console.WriteLine($"\nSource document ['{filePath}'] contains {signatures.Count} QR code signature(s):");
                    
                    foreach (var qrCodeSignature in signatures)
                    {
                        Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
                        Console.WriteLine($"Content: {qrCodeSignature.Text}");
                        Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
                        Console.WriteLine();
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

## Расширенные методы поиска QR-кодов

### Поиск по определенным критериям

Для более целевого поиска вы можете использовать `QrCodeSearchOptions` чтобы настроить критерии поиска:

```csharp
// Создайте параметры поиска QR-кода с определенными критериями
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    // Искать только на определенных страницах
    AllPages = false,
    PageNumber = 1,
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } },
    
    // Фильтр по содержимому QR-кода
    Text = "Invoice",
    MatchType = TextMatchType.Contains,
    
    // Фильтр по определенным типам QR-кодов
    EncodeType = QrCodeTypes.QR,
    
    // Определите конкретную область для поиска
    Rectangle = new Rectangle(100, 100, 400, 400)
};

// Поиск с конкретными параметрами
List<QrCodeSignature> filteredSignatures = signature.Search<QrCodeSignature>(options);
```

### Обработка данных QR-кода

Вы можете реализовать индивидуальную обработку данных QR-кода в соответствии с требованиями вашего приложения:

```csharp
foreach (var qrCode in signatures)
{
    // Извлечение и обработка данных QR-кода на основе его содержания
    string qrContent = qrCode.Text;
    
    if (qrContent.StartsWith("URL:"))
    {
        // URL-данные процесса
        string url = qrContent.Substring(4);
        Console.WriteLine($"Found URL in QR code: {url}");
    }
    else if (qrContent.StartsWith("CONTACT:"))
    {
        // Обработка контактной информации
        string contact = qrContent.Substring(8);
        Console.WriteLine($"Found contact information in QR code: {contact}");
    }
    else if (qrContent.StartsWith("INVOICE:"))
    {
        // Обработка информации о счетах-фактурах
        string invoiceData = qrContent.Substring(8);
        Console.WriteLine($"Found invoice information in QR code: {invoiceData}");
        
        // Анализ и проверка данных счетов-фактур
        if (ValidateInvoiceData(invoiceData))
        {
            Console.WriteLine("Invoice data is valid!");
        }
        else
        {
            Console.WriteLine("Warning: Invalid invoice data detected!");
        }
    }
}

// Пример метода проверки
static bool ValidateInvoiceData(string data)
{
    // Реализуйте свою логику проверки
    return !string.IsNullOrEmpty(data) && data.Contains("ID") && data.Contains("Amount");
}
```

### Реализация проверки безопасности

QR-коды часто используются для аутентификации. Вот как реализовать базовую проверку безопасности:

```csharp
// Проверьте, содержит ли документ действительный QR-код аутентификации.
bool hasValidAuthQrCode = false;

foreach (var qrCode in signatures)
{
    if (qrCode.Text.StartsWith("AUTH:"))
    {
        string authCode = qrCode.Text.Substring(5);
        
        // Проверить код аутентификации (например, по базе данных или предопределенному списку)
        if (VerifyAuthCode(authCode))
        {
            hasValidAuthQrCode = true;
            Console.WriteLine("Document contains valid authentication QR code!");
            break;
        }
    }
}

if (!hasValidAuthQrCode)
{
    Console.WriteLine("Warning: Document does not contain a valid authentication QR code!");
}

// Пример метода проверки
static bool VerifyAuthCode(string code)
{
    // Реализуйте свою логику проверки
    // Это может быть поиск в базе данных, вызов API или сравнение с предопределенными значениями.
    return code == "A7B82C3D" || code == "X9Y8Z7W6";
}
```

### Извлечение изображений QR-кода

Вы можете извлекать изображения QR-кодов из документов для дальнейшей обработки или отображения:

```csharp
// Сохранить изображения QR-кода на диск
foreach (var qrCode in signatures)
{
    if (qrCode.Content != null)
    {
        // Создайте уникальное имя файла на основе номера страницы и положения
        string outputPath = $"QrCode_P{qrCode.PageNumber}_X{qrCode.Left}_Y{qrCode.Top}.png";
        
        // Сохраните данные изображения
        File.WriteAllBytes(outputPath, qrCode.Content);
        Console.WriteLine($"Saved QR code image to {outputPath}");
    }
}
```

## Заключение

В этом подробном руководстве мы рассмотрели, как искать QR-коды в документах с помощью GroupDocs.Signature для .NET. Теперь вы знаете, как реализовать надёжную обработку QR-кодов в своих приложениях .NET, от базового поиска до продвинутых методов. API GroupDocs.Signature предоставляет мощную и гибкую платформу для работы с различными типами подписей, включая QR-коды, в документах разных форматов.

Используя эти возможности, вы можете улучшить процессы проверки документов, внедрить системы аутентификации и извлечь ценную информацию, встроенную в QR-коды, — и все это в ваших приложениях .NET.

## Часто задаваемые вопросы

### Какие форматы QR-кодов поддерживает GroupDocs.Signature?

GroupDocs.Signature поддерживает различные форматы QR-кодов, включая стандартный QR-код, Micro QR-код и другие распространённые стандарты QR-кодов. Доступ к нужному формату можно получить через `EncodeType` собственность `QrCodeSignature` объект.

### Могу ли я искать QR-коды в документах, защищенных паролем?

Да, GroupDocs.Signature поддерживает поиск QR-кодов в защищенных паролем документах, предоставляя пароль при инициализации `Signature` объект:

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Поиск QR-кодов
}
```

### Как отфильтровать QR-коды по их содержанию?

Вы можете фильтровать QR-коды по их содержанию, используя `Text` и `MatchType` свойства `QrCodeSearchOptions`:

```csharp
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    Text = "Invoice",
    MatchType = TextMatchType.Contains // Другие варианты: Exact, StartsWith, EndsWith
};
```

### Может ли GroupDocs.Signature обнаруживать поврежденные или частично видимые QR-коды?

GroupDocs.Signature может обнаруживать частично видимые QR-коды, но сильно повреждённые QR-коды могут быть не распознаны. Точность обнаружения зависит от качества и видимости QR-кода в документе.

### Какие форматы документов поддерживаются для поиска по QR-коду?

GroupDocs.Signature поддерживает поиск QR-кодов в различных форматах документов, включая PDF, документы Microsoft Office (Word, Excel, PowerPoint), изображения (JPEG, PNG, TIFF) и многие другие.

## Смотрите также

* [Справочник API](https://reference.groupdocs.com/signature/net/)
* [Примеры кода на GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Документация по продукту](https://docs.groupdocs.com/signature/net/)
* [Страница продукта](https://products.groupdocs.com/signature/net/)
* [Загрузить последнюю версию](https://releases.groupdocs.com/signature/net/)
* [Статьи блога](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Бесплатный форум поддержки](https://forum.groupdocs.com/c/signature/13)
* [Временная лицензия](https://purchase.groupdocs.com/temporary-license/)