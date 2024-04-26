---
title: Подписание PDF с метаданными
linktitle: Подписание PDF с метаданными
second_title: GroupDocs.Signature .NET API
description: Узнайте, как подписывать PDF-документы с метаданными с помощью GroupDocs.Signature для .NET. Легко улучшите отслеживаемость и подлинность документов.
type: docs
weight: 11
url: /ru/net/document-signing/sign-pdf-with-metadata/
---
## Введение
В этом руководстве мы научимся подписывать PDF-документ с метаданными с помощью GroupDocs.Signature для .NET. Добавление метаданных в PDF-файл может предоставить дополнительную информацию о документе, например авторство, дату создания, идентификатор документа и т. д.
## Предварительные условия
Прежде чем мы начнем, убедитесь, что у вас есть следующее:
1.  GroupDocs.Signature для .NET: его можно загрузить с сайта[здесь](https://releases.groupdocs.com/signature/net/).
2. PDF-документ: подготовьте образец PDF-файла для подписания.
3. Базовые знания программирования на C#. Для понимания примеров кода необходимо знание синтаксиса C#.
## Импортировать пространства имен
Сначала убедитесь, что вы импортировали необходимые пространства имен для доступа к необходимым классам и методам:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Шаг 1. Загрузите PDF-документ
Загрузите PDF-документ, который хотите подписать:
```csharp
string filePath = "sample.pdf";
```
## Шаг 2. Укажите путь к выходному файлу
Определите путь к выходному файлу, в котором будет сохранен подписанный PDF-файл с метаданными:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
```
## Шаг 3. Создайте экземпляр подписи
Инициализируйте экземпляр подписи, указав путь к PDF-документу:
```csharp
using (Signature signature = new Signature(filePath))
{
    // Здесь будет находиться код, связанный с подписью.
}
```
## Шаг 4. Определите параметры метаданных
Создайте MetadataSignOptions и добавьте поля метаданных с соответствующими значениями:
```csharp
MetadataSignOptions options = new MetadataSignOptions();
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // Строковое значение
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // Значения даты и времени
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // Целое значение
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // Двойное значение
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // Десятичное значение
    .Add(new PdfMetadataSignature("Total", 123.456F));              // Плавающее значение
```
## Шаг 5: Подпишите документ
Подпишите PDF-документ с указанными параметрами метаданных и сохраните подписанный документ:
```csharp
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Заключение
В этом руководстве мы рассмотрели, как подписать PDF-документ с метаданными с помощью GroupDocs.Signature для .NET. Следуя пошаговому руководству, вы можете легко добавлять в PDF-файлы информацию о метаданных, такую как авторство, дата создания и т. д., повышая их полезность и отслеживаемость.
## Часто задаваемые вопросы
### Могу ли я добавить собственные поля метаданных в свои PDF-документы?
Да, вы можете добавить настраиваемые поля метаданных, указав имя поля и соответствующее ему значение с помощью GroupDocs.Signature для .NET.
### Совместим ли GroupDocs.Signature для .NET со всеми версиями .NET Framework?
GroupDocs.Signature для .NET совместим с различными версиями .NET Framework, обеспечивая гибкость и простоту интеграции.
### Поддерживает ли GroupDocs.Signature подписание других форматов документов, кроме PDF?
Да, GroupDocs.Signature поддерживает широкий спектр форматов документов, включая Word, Excel, PowerPoint и другие.
### Могу ли я подписать несколько документов одновременно с помощью GroupDocs.Signature для .NET?
Да, вы можете подписывать несколько документов одновременно, перебирая список файлов и программно применяя процесс подписи.
### Доступна ли техническая поддержка для пользователей GroupDocs.Signature?
 Да, GroupDocs предоставляет специальную техническую поддержку через свои форумы. Вы можете получить доступ к форуму поддержки[здесь](https://forum.groupdocs.com/c/signature/13).