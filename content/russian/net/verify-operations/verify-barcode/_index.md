---
"description": "Реализуйте надежную проверку штрихкодов в приложениях .NET с помощью GroupDocs.Signature. Полные примеры кода и рекомендации по обеспечению подлинности документов."
"linktitle": "Проверить штрих-код"
"second_title": "GroupDocs.Signature .NET API"
"title": "Проверка подписей штрих-кодов в документах"
"url": "/ru/net/verify-operations/verify-barcode/"
"weight": 10
---

## Введение

Штрихкоды стали неотъемлемой частью современных систем управления документами, обеспечивая быстрый доступ к закодированной информации и одновременно выполняя функцию безопасности. GroupDocs.Signature для .NET предоставляет мощный API для проверки подписей штрихкодов в документах, гарантируя их подлинность и целостность.

В этом подробном руководстве рассматривается процесс реализации проверки штрихкодов в приложениях .NET с помощью GroupDocs.Signature. Работаете ли вы с деловыми документами, сертификатами, контрактами или любыми другими типами документов, использующими штрихкоды для аутентификации, это руководство поможет вам реализовать надежную функцию проверки.

## Предпосылки

Перед внедрением функции проверки штрихкода убедитесь, что выполнены следующие предварительные условия:

1. GroupDocs.Signature для .NET: Загрузите и установите библиотеку с сайта [страница загрузки](https://releases.groupdocs.com/signature/net/).
2. Среда разработки .NET: Visual Studio или любая совместимая среда разработки .NET.
3. Базовые знания: знакомство с программированием на языке C# и концепциями .NET Framework.
4. Тестовый документ: документ, содержащий штрих-кодовые подписи для целей проверки.

## Импорт требуемых пространств имен

Начните с импорта необходимых пространств имен для доступа к функциональности GroupDocs.Signature:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Давайте разделим процесс проверки штрихкода на понятные и выполнимые шаги:

## Шаг 1: Укажите путь к документу

```csharp
// Путь к документу, содержащему штрих-кодовые подписи
string filePath = "sample_multiple_signatures.docx";
```

Обязательно замените путь в примере на фактический путь к документу, содержащему подписи штрихкодов.

## Шаг 2: Инициализация объекта подписи

```csharp
// Создайте экземпляр класса Signature, передав путь к документу
using (Signature signature = new Signature(filePath))
{
    // Код подтверждения будет реализован здесь.
}
```

Класс Signature является основной точкой входа для всех операций в API GroupDocs.Signature.

## Шаг 3: Настройте параметры проверки штрихкода

```csharp
// Определить параметры проверки штрих-кода
BarcodeVerifyOptions options = new BarcodeVerifyOptions()
{
    AllPages = true,           // Проверьте все страницы документа
    Text = "12345",            // Текст, который должен совпадать со штрихкодом
    MatchType = TextMatchType.Contains // Укажите критерии соответствия текста
};
```

Параметры проверки позволяют вам определить конкретные критерии для процесса проверки:
- `AllPages`: Установите значение true, чтобы проверить все страницы документа.
- `Text`: Текстовое содержимое, которое должно совпадать со штрихкодом.
- `MatchType`: Метод сопоставления текста (Contains, Exact, StartsWith, EndsWith)

## Шаг 4: Выполните процесс проверки

```csharp
// Выполнить проверку
VerificationResult result = signature.Verify(options);
```

Это выполнит процесс проверки на основе указанных вами параметров.

## Шаг 5: Результаты проверки процесса

```csharp
// Проверьте результат проверки и действуйте соответствующим образом.
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid barcode signatures!");
    
    // Отображать информацию об успешных подписях
    foreach (BarcodeSignature barcodeSignature in result.Succeeded)
    {
        Console.WriteLine($"\nFound valid barcode signature:");
        Console.WriteLine($"Text: {barcodeSignature.Text}");
        Console.WriteLine($"Type: {barcodeSignature.EncodeType.TypeName}");
        Console.WriteLine($"Location: Page {barcodeSignature.PageNumber}, {barcodeSignature.Left}x{barcodeSignature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

Этот код проверяет, была ли проверка успешной, и предоставляет подробную информацию о проверенных подписях штрих-кода.

## Полный пример

Вот полный рабочий пример, демонстрирующий проверку штрихкода:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace GroupDocs.Signature.Examples
{
    class Program
    {
        static void Main(string[] args)
        {
            // Путь к документу
            string filePath = "sample_multiple_signatures.docx";
            
            try
            {
                // Инициализировать экземпляр подписи
                using (Signature signature = new Signature(filePath))
                {
                    // Настройка параметров проверки
                    BarcodeVerifyOptions options = new BarcodeVerifyOptions()
                    {
                        AllPages = true,
                        Text = "12345",
                        MatchType = TextMatchType.Contains
                    };
                    
                    // Проверка подписей документов
                    VerificationResult result = signature.Verify(options);
                    
                    // Результаты проверки процесса
                    if (result.IsValid)
                    {
                        Console.WriteLine($"Document {filePath} contains valid barcode signatures!");
                        
                        foreach (BarcodeSignature item in result.Succeeded)
                        {
                            Console.WriteLine($"\nValid signature found with text: {item.Text}");
                            Console.WriteLine($"Barcode type: {item.EncodeType.TypeName}");
                            Console.WriteLine($"Page: {item.PageNumber}");
                        }
                    }
                    else
                    {
                        Console.WriteLine($"\nDocument {filePath} failed verification process.");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
            }
        }
    }
}
```

## Расширенные сценарии проверки

GroupDocs.Signature предоставляет дополнительные возможности для более сложных сценариев проверки:

### Проверка определенных типов штрихкодов

Если вы знаете, какой именно тип штрихкода вас интересует, вы можете ограничить проверку этим типом:

```csharp
BarcodeVerifyOptions options = new BarcodeVerifyOptions()
{
    EncodeType = BarcodeTypes.Code128,  // Проверять только штрихкоды Code128
    Text = "PROD-12345",
    MatchType = TextMatchType.Exact
};
```

### Проверка штрихкодов на определенных страницах

Для многостраничных документов вы можете ограничить проверку определенными страницами:

```csharp
BarcodeVerifyOptions options = new BarcodeVerifyOptions()
{
    AllPages = false,
    PageNumber = 2,  // Проверить только на странице 2
    Text = "INV-2023"
};
```

### Использование регулярных выражений для проверки

Для более гибкого сопоставления с шаблонами вы можете использовать регулярные выражения:

```csharp
BarcodeVerifyOptions options = new BarcodeVerifyOptions()
{
    Text = "INV-\\d{4}-\\d{2}",  // Сопоставьте номера счетов-фактур, например INV-2023-01
    MatchType = TextMatchType.Regex
};
```

### Одновременная проверка нескольких типов штрихкодов

Вы можете создать несколько вариантов проверки для проверки различных типов штрихкодов:

```csharp
// Создайте список вариантов проверки
List<VerifyOptions> listOptions = new List<VerifyOptions>();

// Добавить проверку QR-кода
listOptions.Add(new BarcodeVerifyOptions()
{
    EncodeType = BarcodeTypes.QR,
    Text = "Security"
});

// Добавить проверку Code128
listOptions.Add(new BarcodeVerifyOptions()
{
    EncodeType = BarcodeTypes.Code128,
    Text = "12345"
});

// Подтвердите с помощью нескольких вариантов
VerificationResult result = signature.Verify(listOptions);
```

## Лучшие практики проверки штрих-кодов

1. Обработка ошибок: всегда реализуйте правильную обработку ошибок, чтобы корректно справляться с непредвиденными ситуациями.
2. Оптимизация производительности: для больших документов рассмотрите возможность проверки отдельных страниц, а не всего документа.
3. Ведение журнала: Внедрите ведение журнала для отслеживания попыток проверки и результатов в целях аудита.
4. Вопросы безопасности: Храните критерии проверки в надежном месте, особенно если они являются частью вашей инфраструктуры безопасности.
5. Тестирование: Тестовая проверка с использованием различных форматов документов и типов штрихкодов для обеспечения совместимости.

## Устранение распространенных проблем

### Штрихкод не обнаружен
- Убедитесь, что штрих-код четко виден в документе.
- Проверьте, поддерживается ли тип штрихкода в GroupDocs.Signature.
- Убедитесь, что штрих-код не искажен и не поврежден.

### Ошибки проверки
- Подтвердите правильность критериев проверки (текст, тип штрихкода)
- Проверьте, подходит ли MatchType для вашего варианта использования.
- Убедитесь, что документ не был изменен с момента нанесения штрих-кода.

### Проблемы с производительностью
- Оптимизируйте проверку, нацелившись на определенные страницы, где ожидаются штрихкоды.
- Ограничьте проверку определенными типами штрихкодов, если они известны заранее.

## Заключение

Проверка штрихкодов — важнейший инструмент обеспечения подлинности и целостности документов в современных системах управления документами. GroupDocs.Signature для .NET предоставляет комплексный и простой в использовании API для реализации надежной функции проверки штрихкодов в ваших приложениях .NET.

Следуя этому пошаговому руководству, вы узнали, как:
- Настройте и инициализируйте процесс проверки
- Укажите различные критерии проверки
- Обработка и интерпретация результатов проверки
- Реализуйте расширенные сценарии проверки

Эти возможности позволяют создавать безопасные и надежные системы обработки документов, способные проверять подлинность штрихкодов в документах различных форматов.

## Часто задаваемые вопросы

### Какие форматы документов поддерживаются для проверки штрих-кода?
GroupDocs.Signature поддерживает широкий спектр форматов документов, включая PDF, документы Word (DOC, DOCX), электронные таблицы Excel (XLS, XLSX), презентации PowerPoint (PPT, PPTX), изображения и многое другое.

### Может ли GroupDocs.Signature проверять несколько штрихкодов в одном документе?
Да, GroupDocs.Signature может проверить несколько штрихкодов в одном документе. Результаты проверки будут включать все совпадающие штрихкоды.

### Какие типы штрихкодов поддерживаются для проверки?
GroupDocs.Signature поддерживает множество типов штрихкодов, включая Code39, Code128, EAN13, EAN8, QR Code, DataMatrix, PDF417 и многие другие.

### Могу ли я проверить штрих-коды в документах, защищенных паролем?
Да, GroupDocs.Signature предоставляет возможность указывать пароли документов при открытии защищенных документов для проверки.

### Можно ли проверить штрих-коды, содержащие двоичные данные вместо текста?
Да, GroupDocs.Signature предоставляет возможности проверки штрихкодов с помощью двоичных данных через `BinaryData` свойство вариантов проверки.

### Связанные ресурсы
* [Справочник API GroupDocs.Signature](https://reference.groupdocs.com/signature/net/)
* [GroupDocs.Signature Загрузки](https://releases.groupdocs.com/signature/net/)
* [Примеры кода на GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Документация](https://docs.groupdocs.com/signature/net/)
* [Страница продукта](https://products.groupdocs.com/signature/net/)
* [Статьи блога](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Форум поддержки](https://forum.groupdocs.com/c/signature/13)
* [Временная лицензия](https://purchase.groupdocs.com/temporary-license/)