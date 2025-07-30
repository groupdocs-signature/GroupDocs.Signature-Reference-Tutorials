---
"description": "Защитите и улучшите электронные таблицы Excel, внедрив подписи метаданных с помощью GroupDocs.Signature для .NET. Добавляйте информацию об авторе, временные метки и пользовательские данные для улучшения отслеживания и проверки подлинности документов."
"linktitle": "Подписать электронную таблицу с метаданными"
"second_title": "GroupDocs.Signature .NET API"
"title": "Добавление подписей метаданных в электронные таблицы Excel в C# .NET"
"url": "/ru/net/document-signing/sign-spreadsheet-with-metadata/"
"weight": 13
---

## Введение

Электронные таблицы Excel часто содержат критически важные бизнес-данные, финансовую информацию и важные расчёты. Обеспечение их подлинности, отслеживание происхождения и защита целостности критически важны во многих профессиональных средах. Одним из эффективных способов повышения безопасности и прослеживаемости электронных таблиц является внедрение подписей метаданных.

Это подробное руководство познакомит вас с процессом подписания таблиц Excel метаданными с помощью GroupDocs.Signature для .NET. Добавляя подписи метаданных, вы можете встраивать ценную информацию, такую как сведения об авторе, метки времени создания, идентификаторы документов и другие пользовательские свойства, непосредственно в структуру файла электронной таблицы.

## Предпосылки

Прежде чем приступить к выполнению этого руководства, убедитесь, что у вас есть следующее:

1. [GroupDocs.Signature для .NET](https://releases.groupdocs.com/signature/net/) - Загрузите и установите библиотеку
2. Среда разработки — Visual Studio или любая другая .NET-совместимая IDE
3. Таблица Excel — пример файла электронной таблицы (XLSX, XLS и т. д.)
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

Определите пути к исходной электронной таблице и место сохранения подписанных выходных данных:

```csharp
// Укажите путь к вашему файлу Excel
string filePath = "sample.xlsx";

// Определите выходной каталог и имя файла для подписанной электронной таблицы.
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");

// Убедитесь, что выходной каталог существует
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Шаг 2: Инициализация объекта подписи

Создайте экземпляр класса Signature с исходным файлом электронной таблицы:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Остальной код будет здесь.
}
```

## Шаг 3: Создание и настройка подписей метаданных

Затем определите параметры метаданных и создайте массив подписей метаданных электронной таблицы:

```csharp
// Создать объект параметров метаданных
MetadataSignOptions options = new MetadataSignOptions();

// Создайте массив подписей метаданных электронной таблицы с различными типами данных.
SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // Строковое значение
    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // Значение DateTime
    new SpreadsheetMetadataSignature("DocumentId", 123456),           // Целочисленное значение
    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // Двойная ценность
    new SpreadsheetMetadataSignature("Amount", 123.456M),             // Десятичное значение
    new SpreadsheetMetadataSignature("Total", 123.456F)               // Плавающее значение
};

// Добавить сбор подписей в опции
options.Signatures.AddRange(signatures);
```

## Шаг 4: Подпишите электронную таблицу с метаданными

Примените подписи метаданных к электронной таблице и сохраните результат:

```csharp
// Подпишите документ и сохраните его в выходном файле.
SignResult result = signature.Sign(outputFilePath, options);

// Показать сообщение об успешном завершении
Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed spreadsheet saved at: {outputFilePath}");
```

## Полный пример

Вот полный пример кода, объединяющий все шаги:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignSpreadsheetWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Укажите пути к файлам
            string filePath = "sample.xlsx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");
            
            // Убедитесь, что выходной каталог существует
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Подпишите электронную таблицу с метаданными
            using (Signature signature = new Signature(filePath))
            {
                // Создать объект параметров метаданных
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Создайте массив подписей метаданных электронной таблицы с различными типами данных.
                SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
                {
                    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // Строковое значение
                    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // Значение DateTime
                    new SpreadsheetMetadataSignature("DocumentId", 123456),           // Целочисленное значение
                    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // Двойная ценность
                    new SpreadsheetMetadataSignature("Amount", 123.456M),             // Десятичное значение
                    new SpreadsheetMetadataSignature("Total", 123.456F)               // Плавающее значение
                };
                
                // Добавить сбор подписей в опции
                options.Signatures.AddRange(signatures);
                
                // Подписать документ и сохранить в файл
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Показать результаты
                Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Расширенные методы работы с метаданными электронных таблиц

### Работа с пользовательскими и встроенными свойствами электронных таблиц

Таблицы Excel имеют как встроенные, так и настраиваемые свойства, доступ к которым можно получить через диалоговое окно свойств файла. GroupDocs.Signature позволяет работать с обоими:

```csharp
// Добавить встроенные свойства
signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Company", "Sherlock Holmes Consulting"),
    new SpreadsheetMetadataSignature("Category", "Financial"),
    new SpreadsheetMetadataSignature("Keywords", "budget,forecast,analysis"),
    new SpreadsheetMetadataSignature("Comments", "This spreadsheet contains confidential information"),
    new SpreadsheetMetadataSignature("Manager", "John Watson")
};
options.Signatures.AddRange(signatures);

// Добавить пользовательские свойства
options.Signatures.Add(new SpreadsheetMetadataSignature("Department", "Finance"));
options.Signatures.Add(new SpreadsheetMetadataSignature("SecurityLevel", "Confidential"));
```

### Поиск метаданных в подписанных электронных таблицах

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

### Обновление существующих метаданных

Вы можете обновить существующие метаданные в электронных таблицах, используя те же имена свойств:

```csharp
// Обновить существующие метаданные
options.Signatures.Add(new SpreadsheetMetadataSignature("Author", "Updated Author Name"));
```

## Заключение

В этом подробном руководстве вы узнали, как подписывать таблицы Excel метаданными с помощью GroupDocs.Signature для .NET. Внедрение метаданных в файлы электронных таблиц улучшает отслеживаемость документов, предоставляет ценный контекст и помогает установить их подлинность.

Сигнатуры метаданных в электронных таблицах особенно полезны в бизнес-средах, где важны происхождение документа, авторство и отслеживание версий. Встроенные метаданные могут включать информацию об авторе, времени создания, идентификаторах документа и настраиваемых свойствах, соответствующих потребностям вашей организации.

Внедрив подписи метаданных с помощью GroupDocs.Signature, вы можете гарантировать, что ваши таблицы Excel сохранят свою целостность и предоставят проверяемую информацию на протяжении всего их жизненного цикла.

## Часто задаваемые вопросы

### Можно ли добавлять метаданные в электронные таблицы, в которых уже определены некоторые свойства?

Да, вы можете добавлять новые метаданные или обновлять существующие в электронных таблицах. GroupDocs.Signature выполнит интеграцию, добавляя новые свойства или обновляя существующие с теми же именами.

### Какие форматы электронных таблиц поддерживаются для подписания метаданных?

GroupDocs.Signature для .NET поддерживает подписание метаданных для различных форматов электронных таблиц, включая XLSX, XLS, XLSM, ODS и другие. Полный список см. в [официальная документация](https://docs.groupdocs.com/signature/net/).

### Видны ли пользователям подписи метаданных в электронных таблицах?

Сигнатуры метаданных не видны в самом содержимом электронной таблицы. Однако их можно просмотреть через панель свойств документа в Excel или других совместимых приложениях.

### Можно ли программно проверить, была ли подделана электронная таблица после добавления метаданных?

Да, GroupDocs.Signature предоставляет возможности проверки, которые помогают определить, был ли документ изменен после подписания, включая изменения метаданных.

### Влияет ли добавление метаданных на функциональность электронных таблиц?

Добавление метаданных минимально влияет на размер файла и не влияет на функциональность электронных таблиц. Это простой способ улучшить свойства документа, не затрагивая вычисления, формулы и другие функции Excel.

### Где я могу найти дополнительные ресурсы и поддержку?

- [Справочник API](https://reference.groupdocs.com/signature/net/)
- [Загрузки](https://releases.groupdocs.com/signature/net/)
- [Примеры](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Документация](https://docs.groupdocs.com/signature/net/)
- [Страница продукта](https://products.groupdocs.com/signature/net/)
- [Блог](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Форум поддержки](https://forum.groupdocs.com/c/signature/13)
- [Временная лицензия](https://purchase.groupdocs.com/temporary-license/)