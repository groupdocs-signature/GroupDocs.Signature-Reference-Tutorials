---
"description": "Узнайте, как проверять QR-коды в документах с помощью GroupDocs.Signature для .NET. Полное руководство с примерами кода и рекомендациями по аутентификации документов."
"linktitle": "Проверить QR-код"
"second_title": "GroupDocs.Signature .NET API"
"title": "Проверка QR-кода в документах"
"url": "/ru/net/verify-operations/verify-qr-code/"
"weight": 12
---

## Введение

Безопасность документов — критически важный аспект современных бизнес-операций. QR-коды становятся всё более популярным способом встраивания информации в документы, подлинность которых можно проверить. GroupDocs.Signature для .NET предоставляет мощное и гибкое решение для проверки QR-кодов, встраиваемых в документы различных форматов.

Это подробное руководство проведет вас через процесс внедрения проверки QR-кода в ваши .NET-приложения, гарантируя сохранение целостности и подлинности ваших документов.

## Предпосылки

Перед внедрением функции проверки QR-кода убедитесь, что выполнены следующие предварительные условия:

1. GroupDocs.Signature для .NET: Загрузите и установите библиотеку с сайта [страница загрузки](https://releases.groupdocs.com/signature/net/).
2. Среда разработки: Visual Studio или любая совместимая среда разработки .NET.
3. Тестовый документ: документ, содержащий подписи QR-кодов для целей проверки.
4. Базовые знания: знакомство с программированием на языке C# и концепциями .NET Framework.

## Импорт пространств имен

Начните с импорта необходимых пространств имен для доступа к функциональности GroupDocs.Signature:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Пошаговый процесс проверки QR-кода

Выполните следующие подробные шаги для проверки QR-кодов в ваших документах:

### Шаг 1: Укажите путь к документу

```csharp
// Укажите путь к документу, содержащему подписи QR-кодов.
string filePath = "sample_multiple_signatures.docx";
```

Обязательно замените путь в примере на фактический путь к вашему документу.

### Шаг 2: Инициализация объекта подписи

```csharp
// Создайте экземпляр подписи, передав путь к документу
using (Signature signature = new Signature(filePath))
{
    // Код подтверждения будет реализован здесь.
}
```

Класс Signature является основной точкой входа для всех операций в API GroupDocs.Signature.

### Шаг 3: Настройте параметры проверки QR-кода

```csharp
// Определите параметры проверки QR-кода
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true, // Проверьте все страницы документа
    Text = "John",   // Текст для проверки в QR-коде
    MatchType = TextMatchType.Contains // Укажите критерии соответствия текста
};
```

Параметры проверки позволяют вам определить конкретные критерии для процесса проверки:
- `AllPages`: Установите значение true, чтобы проверить все страницы документа (поведение по умолчанию)
- `Text`: Текстовое содержимое, которое должно совпадать с QR-кодом.
- `MatchType`: Метод сопоставления текста (Содержит, Точно, Начинается с и т. д.)

### Шаг 4: Выполните процесс проверки

```csharp
// Выполнить проверку
VerificationResult result = signature.Verify(options);
```

Это выполнит процесс проверки на основе указанных вами параметров.

### Шаг 5: Результаты проверки процесса

```csharp
// Проверьте результат проверки и действуйте соответствующим образом.
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid QR code signature!");
    
    // Отображать информацию об успешных подписях
    foreach (QrCodeSignature signature in result.Succeeded)
    {
        Console.WriteLine($"Found valid QR Code signature with text: {signature.Text}");
        Console.WriteLine($"QR Code type: {signature.EncodeType.TypeName}");
        Console.WriteLine($"Location: Page {signature.PageNumber}, {signature.Left}x{signature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

Правильная обработка результатов проверки позволяет вашему приложению предпринимать соответствующие действия в зависимости от результатов проверки.

## Полный пример

Вот полный рабочий пример, демонстрирующий проверку QR-кода:

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
            
            // Инициализировать экземпляр подписи
            using (Signature signature = new Signature(filePath))
            {
                // Настройка параметров проверки
                QrCodeVerifyOptions options = new QrCodeVerifyOptions()
                {
                    AllPages = true,
                    Text = "John",
                    MatchType = TextMatchType.Contains
                };
                
                // Проверка подписей документов
                VerificationResult result = signature.Verify(options);
                
                // Результаты проверки процесса
                if (result.IsValid)
                {
                    Console.WriteLine($"Document {filePath} contains valid QR code signature!");
                    
                    foreach (QrCodeSignature qrSignature in result.Succeeded)
                    {
                        Console.WriteLine($"Found valid QR Code with text: {qrSignature.Text}");
                    }
                }
                else
                {
                    Console.WriteLine($"Document {filePath} failed verification process.");
                }
            }
        }
    }
}
```

## Расширенные возможности проверки

GroupDocs.Signature предоставляет дополнительные возможности для более сложных сценариев проверки:

### Проверка определенных типов QR-кодов

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    EncodeType = QrCodeTypes.QR,  // Проверяйте только стандартные QR-коды
    Text = "Confidential",
    MatchType = TextMatchType.Exact
};
```

### Проверка на определенных страницах

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = false,
    PageNumber = 2,  // Проверить только на странице 2
    Text = "Approved"
};
```

### Использование регулярных выражений для проверки

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    Text = "INV-\\d{6}",  // Сопоставьте номера счетов-фактур (например, INV-123456)
    MatchType = TextMatchType.Regex
};
```

## Лучшие практики проверки QR-кода

1. Всегда проверяйте входные данные: убедитесь, что пути к документам и критерии проверки действительны перед обработкой.
2. Реализуйте обработку ошибок: используйте блоки try-catch для обработки потенциальных исключений во время проверки.
3. Подумайте о производительности: для больших документов рассмотрите возможность проверки отдельных страниц, а не всего документа.
4. Регистрируйте результаты проверки: ведите журналы процессов проверки для целей аудита.
5. Протестируйте различные форматы документов: убедитесь, что ваша проверка работает со всеми требуемыми форматами документов.

## Заключение

Проверка QR-кодов в документах — важный аспект обеспечения подлинности и целостности документов. GroupDocs.Signature для .NET предоставляет комплексный и удобный API для реализации проверки QR-кодов в ваших .NET-приложениях.

Следуя этому руководству, вы узнали, как:
- Настройте и инициализируйте процесс проверки
- Укажите различные критерии проверки
- Обработка и интерпретация результатов проверки
- Реализуйте расширенные возможности проверки

Эти знания позволят вам повысить безопасность и надежность ваших систем управления документами.

## Часто задаваемые вопросы

### Может ли GroupDocs.Signature верифицировать несколько QR-кодов в одном документе?
Да, GroupDocs.Signature может верифицировать несколько QR-кодов в одном документе. Результаты проверки будут включать все совпадающие QR-коды.

### Какие форматы документов поддерживаются для проверки QR-кода?
GroupDocs.Signature поддерживает широкий спектр форматов документов, включая PDF, Word (DOC, DOCX), Excel (XLS, XLSX), PowerPoint (PPT, PPTX), изображения и другие.

### Могу ли я проверить QR-коды с помощью определенного шифрования или форматирования?
Да, GroupDocs.Signature предоставляет возможности проверки QR-кодов с использованием определенных типов кодировки и шаблонов форматирования содержимого.

### Можно ли проверить QR-коды, созданные сторонними приложениями?
Да, GroupDocs.Signature может проверять стандартные QR-коды, генерируемые большинством приложений, при условии, что они соответствуют стандартным форматам QR-кодов.

### Как обрабатывать QR-коды, содержащие двоичные данные вместо текста?
GroupDocs.Signature предоставляет возможности для проверки QR-кодов с помощью двоичных данных через `BinaryData` свойство вариантов проверки.

### Связанные ресурсы
* [Справочник API GroupDocs.Signature](https://reference.groupdocs.com/signature/net/)
* [GroupDocs.Signature Загрузки](https://releases.groupdocs.com/signature/net/)
* [Примеры кода на GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Документация](https://docs.groupdocs.com/signature/net/)
* [Страница продукта](https://products.groupdocs.com/signature/net/)
* [Статьи блога](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Форум поддержки](https://forum.groupdocs.com/c/signature/13)
* [Временная лицензия](https://purchase.groupdocs.com/temporary-license/)