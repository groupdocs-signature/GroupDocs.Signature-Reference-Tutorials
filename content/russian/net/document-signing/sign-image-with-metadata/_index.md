---
"description": "Узнайте, как подписывать и встраивать метаданные в изображения с помощью GroupDocs.Signature для .NET. Добавляйте информацию об авторе, временные метки и пользовательские данные для повышения аутентичности и отслеживаемости изображений."
"linktitle": "Подписать изображение с метаданными"
"second_title": "GroupDocs.Signature .NET API"
"title": "Подпись изображений с помощью метаданных в C# .NET"
"url": "/ru/net/document-signing/sign-image-with-metadata/"
"weight": 10
type: docs
---
## Введение

Подписание цифровых изображений с использованием метаданных становится всё более важным для подтверждения подлинности, права собственности и прослеживаемости. GroupDocs.Signature для .NET — это мощное и в то же время простое в использовании решение для добавления подписей метаданных к изображениям различных форматов. Это руководство подробно описывает весь процесс подписания изображений с использованием метаданных на C#.

Сигнатуры метаданных позволяют встраивать ценную информацию непосредственно в файлы изображений, например, информацию об авторе, временные метки создания, уникальные идентификаторы и многое другое. Эта информация становится частью самого файла изображения, обеспечивая надежный метод отслеживания и проверки подлинности изображений.

## Предпосылки

Прежде чем приступить к выполнению этого руководства, убедитесь, что у вас есть следующее:

1. [GroupDocs.Signature для .NET](https://releases.groupdocs.com/signature/net/) - Загрузите и установите библиотеку
2. Среда разработки — Visual Studio или любая совместимая IDE с поддержкой .NET
3. Файл изображения — пример файла изображения в поддерживаемом формате (PNG, JPG, TIFF и т. д.)
4. Базовые знания программирования на C# — знакомство с концепциями программирования на C#

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

Определите пути к исходному изображению и место сохранения подписанного выходного файла:

```csharp
// Укажите путь к исходному файлу изображения.
string filePath = "sample.png";

// Определите выходной каталог и имя файла для подписанного изображения.
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignImageWithMetadata", "SignedWithMetadata.png");

// Убедитесь, что выходной каталог существует
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## Шаг 2: Инициализация объекта подписи

Создайте экземпляр класса Signature с исходным файлом изображения:

```csharp
using (Signature signature = new Signature(filePath))
{
    // Остальной код будет здесь.
}
```

## Шаг 3: Создание и настройка подписей метаданных

Затем определите метаданные, которые вы хотите встроить в изображение. GroupDocs.Signature поддерживает различные типы метаданных:

```csharp
// Инициализировать идентификатор метаданных (специфичный для формата изображения)
ushort imgsMetadataId = 41996;

// Создать объект параметров метаданных
MetadataSignOptions options = new MetadataSignOptions();

// Добавить различные типы подписей метаданных
options
    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes"))  // Строковое значение
    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Значение даты и времени
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Целочисленное значение
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Двойная ценность
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Десятичное значение
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Плавающее значение
```

## Шаг 4: Подпишите изображение с помощью метаданных

Примените подписи метаданных к изображению и сохраните результат:

```csharp
// Подпишите документ и сохраните его в выходном файле.
SignResult result = signature.Sign(outputFilePath, options);

// Показать сообщение об успешном завершении
Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed image saved at: {outputFilePath}");
```

## Полный пример

Вот полный пример кода, объединяющий все шаги:

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignImageWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Укажите пути к файлам
            string filePath = "sample.png";            
            string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
            
            // Убедитесь, что выходной каталог существует
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // Подпишите изображение метаданными
            using (Signature signature = new Signature(filePath))
            {
                // Инициализировать идентификатор метаданных (специфичный для формата изображения)
                ushort imgsMetadataId = 41996;
                
                // Создать параметры метаданных
                MetadataSignOptions options = new MetadataSignOptions();
                
                // Добавьте различные типы подписей метаданных
                options
                    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes")) // Строковое значение
                    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Значение даты и времени
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Целочисленное значение
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Двойная ценность
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Десятичное значение
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Плавающее значение
                
                // Подписать документ и сохранить в файл
                SignResult result = signature.Sign(outputFilePath, options);
                
                // Показать результаты
                Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## Расширенные методы подписи метаданных

### Работа с пользовательскими метаданными

Вы также можете создавать пользовательские поля метаданных с определенными идентификаторами:

```csharp
// Создайте пользовательские метаданные с определенным идентификатором
options.Add(new ImageMetadataSignature(42000, "CustomValue"));
```

### Проверка подписей метаданных

После подписания вы можете захотеть проверить подписи метаданных:

```csharp
// Создать варианты проверки
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// Поиск сигнатур метаданных
SearchResult result = signature.Search(searchOptions);

// Показать найденные подписи
Console.WriteLine($"Found {result.Signatures.Count} metadata signatures:");
foreach(var metadataSignature in result.Signatures)
{
    Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value}");
}
```

## Заключение

В этом руководстве вы узнали, как подписывать изображения метаданными с помощью GroupDocs.Signature для .NET. Встраивание метаданных в изображения — отличный способ повысить аутентичность изображений, добавить важную информацию и оптимизировать процессы управления документами. Этот процесс прост, но эффективен и позволяет настраивать его в соответствии с вашими конкретными требованиями.

Метаданные, встроенные в файл изображения, можно использовать для различных целей, таких как защита авторских прав, отслеживание происхождения изображения, добавление описательной информации и организация цифровой цепочки поставок. Внедряя подписи метаданных, вы можете гарантировать сохранение целостности и подлинности ваших изображений на протяжении всего их жизненного цикла.

## Часто задаваемые вопросы

### Могу ли я добавлять метаданные к существующим подписанным изображениям?

Да, вы можете добавлять дополнительные метаданные к изображениям, которые уже содержат сигнатуры метаданных. Существующие метаданные будут сохранены, а новые метаданные будут добавлены соответствующим образом.

### Какие форматы изображений поддерживаются для подписи метаданных?

GroupDocs.Signature для .NET поддерживает подпись метаданных для различных форматов изображений, включая PNG, JPEG, TIFF, BMP, GIF и другие. Полный список см. в [официальная документация](https://docs.groupdocs.com/signature/net/).

### Можно ли зашифровать метаданные в изображениях?

Да, GroupDocs.Signature предоставляет возможности шифрования метаданных для повышения безопасности. Вы можете использовать возможности шифрования, предоставляемые библиотекой, для защиты конфиденциальных метаданных.

### Могу ли я программно проверить подлинность подписанных изображений?

Конечно. Вы можете использовать методы проверки в GroupDocs.Signature для проверки подписей метаданных и подтверждения подлинности подписанных изображений.

### Существует ли ограничение на размер файла при подписании изображений метаданными?

Сама библиотека не накладывает ограничений на размер файла, но для очень больших файлов может потребоваться больше времени на обработку и памяти. При работе с очень большими изображениями рекомендуется учитывать системные ресурсы.

### Как я могу получить временную лицензию для целей тестирования?

Вы можете получить [временная лицензия](https://purchase.groupdocs.com/temporary-license/) для тестирования GroupDocs.Signature перед совершением покупки.

### Где я могу найти дополнительные ресурсы и поддержку?

- [Справочник API](https://reference.groupdocs.com/signature/net/)
- [Загрузки](https://releases.groupdocs.com/signature/net/)
- [Примеры](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [Документация](https://docs.groupdocs.com/signature/net/)
- [Страница продукта](https://products.groupdocs.com/signature/net/)
- [Блог](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [Форум поддержки](https://forum.groupdocs.com/c/signature/13)