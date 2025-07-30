---
"description": "Интегрируйте подписи метаданных в PDF-документы с помощью GroupDocs.Signature для .NET. Узнайте, как встраивать информацию об авторе, временные метки и пользовательские данные для повышения аутентичности и отслеживаемости PDF-файлов."
"linktitle": "Подписать PDF с метаданными"
"second_title": "GroupDocs.Signature .NET API"
"title": "Добавление подписей метаданных в PDF-документы в C# .NET"
"url": "/ru/net/document-signing/sign-pdf-with-metadata/"
"weight": 11
---

## Введение

Документы в формате PDF (Portable Document Format) широко используются в различных отраслях благодаря своей согласованности и платформенной независимости. Обеспечение подлинности и прослеживаемости этих документов критически важно во многих профессиональных средах. Один из эффективных способов добиться этого — внедрение метаданных в сами PDF-файлы.

В этом подробном руководстве мы рассмотрим, как подписывать PDF-документы метаданными с помощью GroupDocs.Signature для .NET. Подписи метаданных позволяют добавлять в документ дополнительную информацию, например, сведения об авторе, метки времени создания, идентификаторы документа и пользовательские значения, без видимого изменения внешнего вида документа.

## Предпосылки

Прежде чем начать, убедитесь, что у вас есть следующее:

1. [GroupDocs.Signature для .NET](https://releases.groupdocs.com/signature/net/) - Загрузите и установите библиотеку
2. Среда разработки — Visual Studio или любая другая .NET-совместимая IDE
3. PDF-документ — пример PDF-файла для подписания
4. Базовые знания C# — знакомство с языком программирования C#

## Импорт пространств имен

Начните с импорта необходимых пространств имен для доступа к функциональности GroupDocs.Signature:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## Шаг 1: Настройте пути к файлам

Сначала определите путь к вашему PDF-документу и укажите, где вы хотите сохранить подписанный вывод:

```csharp
// Укажите путь к вашему PDF-документу
string filePath = "sample.pdf";

// Определить выходной каталог и путь к файлу
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignPdfWithMetadata", "SignedWithMetadata.pdf");

// Убедитесь, что выходной каталог существует
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Шаг 2: Инициализация объекта подписи

Создайте экземпляр класса Signature с исходным PDF-документом:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Код для подписания будет здесь.
}
```

## Шаг 3: Определите параметры метаданных

Создайте и настройте параметры метаданных, добавив различные типы подписей метаданных:

```csharp
// Создать объект параметров метаданных
MetadataSignOptions options = new MetadataSignOptions();

// Добавляйте различные типы метаданных с помощью гибкого интерфейса.
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Строковое значение
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // Значение DateTime
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Целочисленное значение
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Двойная ценность
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Десятичное значение
    .Add(new PdfMetadataSignature("Total", 123.456F));              // Плавающее значение
```

## Шаг 4: Подпишите PDF-файл с помощью метаданных

Примените подписи метаданных к PDF-документу и сохраните результат:

```csharp
// Подпишите документ и сохраните его в выходной папке.
SignResult result = signature.Sign(outputFilePath, options);

// Показать сообщение об успешном завершении
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed document saved at: {outputFilePath}");
```

## Полный пример

Вот полный пример кода, объединяющий все шаги:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignPdfWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Укажите пути к файлам
            string filePath = "sample.pdf";
            string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
            
            // Убедитесь, что выходной каталог существует
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Подписать PDF-файл с метаданными
            using (Signature signature = new Signature(filePath))
            {
                // Создать объект параметров метаданных
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Добавьте различные типы подписей метаданных
                options
                    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Строковое значение
                    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // Значение DateTime
                    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Целочисленное значение
                    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Двойная ценность
                    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Десятичное значение
                    .Add(new PdfMetadataSignature("Total", 123.456F));              // Плавающее значение
                
                // Подписать документ и сохранить в файл
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Показать результаты
                Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Расширенные операции с метаданными PDF

### Добавление пользовательских метаданных с поддержкой пространства имен

Документы PDF поддерживают пользовательские метаданные с поддержкой пространства имен XML:

```csharp
// Добавить пользовательские метаданные с пространством имен
options.Add(new PdfMetadataSignature("CustomProperty", "Custom Value")
{
    NamespaceUri = "http://your-namespace.com/schema"
});
```

### Поиск метаданных в подписанных PDF-файлах

После подписания вы можете проверить или извлечь метаданные:

```csharp
// Создайте параметры поиска для метаданных
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// Поиск сигнатур метаданных
SearchResult searchResult = signature.Search(searchOptions);

// Показать найденные подписи
Console.WriteLine($"Found {searchResult.Signatures.Count} metadata signatures:");
foreach (var foundSignature in searchResult.Signatures)
{
    MetadataSignature metadataSignature = foundSignature as MetadataSignature;
    if (metadataSignature != null)
    {
        Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value} ({metadataSignature.Value.GetType().Name})");
    }
}
```

### Работа со стандартными метаданными PDF

Документы PDF имеют стандартные поля метаданных, к которым можно получить доступ и которые можно изменять:

```csharp
// Установить стандартные поля метаданных PDF
options
    .Add(new PdfMetadataSignature("Title", "Important Contract"))
    .Add(new PdfMetadataSignature("Subject", "Legal Agreement"))
    .Add(new PdfMetadataSignature("Keywords", "contract, agreement, legal, binding"))
    .Add(new PdfMetadataSignature("Creator", "Legal Department"))
    .Add(new PdfMetadataSignature("Producer", "GroupDocs.Signature"));
```

## Заключение

В этом руководстве вы узнали, как подписывать PDF-документы метаданными с помощью GroupDocs.Signature для .NET. Внедрение метаданных в PDF-файлы — отличный способ повысить аутентичность документов, добавить важную информацию и оптимизировать процессы управления документами.

Метаданные подписей в PDF-файлах особенно ценны в бизнес-средах, где отслеживаемость и проверка подлинности документов имеют решающее значение. Встроенные метаданные могут включать информацию о происхождении документа, авторе, времени создания, версии и настраиваемых свойствах, относящихся к рабочему процессу вашей организации.

Внедряя подписи метаданных с помощью GroupDocs.Signature, вы можете гарантировать, что ваши PDF-документы сохранят свою целостность и предоставят проверяемую информацию на протяжении всего их жизненного цикла.

## Часто задаваемые вопросы

### Могу ли я изменить существующие метаданные в PDF-документе?

Да, вы можете изменять существующие метаданные в PDF-документах. При применении новых сигнатур метаданных с теми же именами, что и у существующих, значения будут обновлены соответствующим образом.

### Видны ли подписи метаданных в PDF-документах конечному пользователю?

Сигнатуры метаданных не видны в самом содержимом документа. Однако их можно просмотреть через панель свойств документа в программах для просмотра PDF-файлов, таких как Adobe Acrobat, или с помощью специализированных инструментов для просмотра метаданных.

### Могу ли я зашифровать или защитить метаданные в PDF-файлах?

GroupDocs.Signature предоставляет возможности защиты документов, включая шифрование. Вы можете применить шифрование на уровне документа для защиты всего PDF-файла, включая его метаданные.

### Существует ли ограничение на объем метаданных, которые я могу добавить в PDF-файл?

Хотя спецификация PDF не устанавливает строгих ограничений, добавление чрезмерного количества метаданных может увеличить размер файла. Рекомендуется включать в метаданные только релевантную и необходимую информацию.

### Можно ли программно проверить, был ли PDF-файл подделан после добавления метаданных?

Да, GroupDocs.Signature предоставляет возможности проверки, которые помогают определить, был ли документ изменен после подписания, включая изменения метаданных.

### Где я могу найти дополнительные ресурсы и поддержку?

- [Справочник API](https://reference.groupdocs.com/signature/net/)
- [Загрузки](https://releases.groupdocs.com/signature/net/)
- [Примеры](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Документация](https://docs.groupdocs.com/signature/net/)
- [Страница продукта](https://products.groupdocs.com/signature/net/)
- [Блог](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Форум поддержки](https://forum.groupdocs.com/c/signature/13)
- [Временная лицензия](https://purchase.groupdocs.com/temporary-license/)