---
title: Подписать изображение с метаданными
linktitle: Подписать изображение с метаданными
second_title: GroupDocs.Signature .NET API
description: Узнайте, как подписывать изображения метаданными в .NET с помощью GroupDocs.Signature. Простое, эффективное и настраиваемое решение для подписи метаданных.
weight: 10
url: /ru/net/document-signing/sign-image-with-metadata/
---

# Подписать изображение с метаданными

## Введение
GroupDocs.Signature для .NET позволяет разработчикам эффективно подписывать изображения метаданными. Это руководство шаг за шагом проведет вас через этот процесс.
## Предварительные условия
Прежде чем начать, убедитесь, что у вас есть следующее:
1. GroupDocs.Signature для .NET: установите пакет GroupDocs.Signature в свой проект .NET. Вы можете скачать его с[здесь](https://releases.groupdocs.com/signature/net/).   
2. Файл изображения: подготовьте файл изображения, который вы хотите подписать метаданными.

## Импортировать пространства имен
Обязательно импортируйте необходимые пространства имен в свой код C#:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Шаг 1. Загрузите файл изображения
Сначала укажите путь к файлу вашего изображения и выходной каталог для подписанного изображения с метаданными:
```csharp
string filePath = "sample.png";            
string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
```
## Шаг 2. Создайте подписи метаданных
Затем создайте различные подписи метаданных и добавьте их в коллекцию подписей параметров:
```csharp
using (Signature signature = new Signature(filePath))
{
    ushort imgsMetadataId = 41996;
    MetadataSignOptions options = new MetadataSignOptions();
    options
        .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Scherlock Holmes")) // Строковое значение
        .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // Значение даты и времени
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // Целое значение
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // Двойное значение
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // Десятичное значение
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // Плавающее значение
    
    // подписать документ в файл
    SignResult result = signature.Sign(outputFilePath, options);
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## Заключение
В этом руководстве вы узнали, как подписать изображение метаданными с помощью GroupDocs.Signature для .NET. Выполнив эти шаги, вы сможете легко включать подписи метаданных в свои приложения .NET.

## Часто задаваемые вопросы
### Могу ли я подписать несколько изображений метаданными с помощью GroupDocs.Signature для .NET?
Да, вы можете подписать несколько изображений метаданными, просматривая каждый файл изображения и применяя подписи метаданных.
### Доступна ли пробная версия GroupDocs.Signature для .NET?
 Да, вы можете скачать пробную версию с сайта[здесь](https://releases.groupdocs.com/).
### Поддерживает ли GroupDocs.Signature для .NET другие форматы файлов, кроме изображений?
Да, GroupDocs.Signature поддерживает различные форматы файлов, включая PDF, Word, Excel и другие.
### Могу ли я настроить внешний вид подписи метаданных?
Да, вы можете настроить внешний вид подписи метаданных, например размер шрифта, цвет и положение.
### Где я могу получить поддержку GroupDocs.Signature для .NET?
 Вы можете получить поддержку на форуме GroupDocs.Signature.[здесь](https://forum.groupdocs.com/c/signature/13).