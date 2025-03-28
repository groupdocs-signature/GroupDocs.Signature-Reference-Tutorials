---
title: Подписать презентацию с метаданными
linktitle: Подписать презентацию с метаданными
second_title: GroupDocs.Signature .NET API
description: Узнайте, как подписывать файлы презентаций метаданными с помощью GroupDocs.Signature для .NET. Повысьте целостность документа и добавьте ценную информацию.
weight: 12
url: /ru/net/document-signing/sign-presentation-with-metadata/
---

# Подписать презентацию с метаданными

## Введение
В этом руководстве мы научимся подписывать файл презентации (PPTX) с метаданными с помощью библиотеки GroupDocs.Signature для .NET. Подписание презентаций с помощью метаданных добавляет в документ ценную информацию, такую как имя автора, дата создания, идентификатор документа, идентификатор подписи и различные числовые значения.
## Предварительные условия
Прежде чем мы начнем, убедитесь, что у вас есть следующее:
1.  GroupDocs.Signature для библиотеки .NET: загрузите и установите библиотеку с сайта[здесь](https://releases.groupdocs.com/signature/net/).
2. Среда разработки: убедитесь, что у вас настроена среда разработки .NET.
3. Файл презентации: подготовьте образец файла презентации (формат PPTX), готовый к подписанию.
4. Базовое понимание C#: Знакомство с языком программирования C# будет полезным.

## Импортировать пространства имен
Прежде чем углубиться в код, давайте импортируем необходимые пространства имен:
```csharp
using System;
using System.IO;
    using GroupDocs.Signature;
    using GroupDocs.Signature.Domain;
    using GroupDocs.Signature.Options;
```
## Шаг 1. Загрузите файл презентации
```csharp
string filePath = "sample.pptx";
```
 Заменять`"sample.pptx"` с путем к файлу презентации.
## Шаг 2. Укажите путь к выходному файлу
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPresentationWithMetadata", "SignedWithMetadata.pptx");
```
Укажите каталог, в котором вы хотите сохранить подписанный файл презентации, а также имя файла.
## Шаг 3. Инициализация объекта подписи
```csharp
using (Signature signature = new Signature(filePath))
```
Инициализируйте объект Signature, указав путь к файлу презентации.
## Шаг 4. Определите параметры подписи метаданных
```csharp
MetadataSignOptions options = new MetadataSignOptions();
```
Создайте экземпляр MetadataSignOptions, чтобы определить параметры подписи метаданных.
## Шаг 5. Создайте подписи метаданных
```csharp
PresentationMetadataSignature[] signatures = new PresentationMetadataSignature[]
{
    new PresentationMetadataSignature("Author", "Mr.Scherlock Holmes"),
    new PresentationMetadataSignature("CreatedOn", DateTime.Now),
    new PresentationMetadataSignature("DocumentId", 123456),
    new PresentationMetadataSignature("SignatureId", 123.456D),
    new PresentationMetadataSignature("Amount", 123.456M),
    new PresentationMetadataSignature("Total", 123.456F)
};
```
Создайте массив объектов PresentationMetadataSignature, каждый из которых представляет подпись метаданных. Вы можете добавлять различные типы метаданных, включая строку, дату и время, целое число, двойное число, десятичное число и число с плавающей запятой.
## Шаг 6. Добавьте подписи в параметры
```csharp
options.Signatures.AddRange(signatures);
```
Добавьте созданные подписи метаданных в объект MetadataSignOptions.
## Шаг 7: Подпишите документ
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
Подпишите файл презентации метаданными, используя указанные параметры, и сохраните подписанный файл в выходном пути.
## Шаг 8: Отображение результата
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
Отображение сообщения об успехе вместе с количеством примененных подписей и путем сохранения подписанного файла.

## Заключение
В этом руководстве мы научились подписывать файл презентации метаданными с помощью библиотеки GroupDocs.Signature для .NET. Добавление подписей метаданных повышает целостность документа и предоставляет ценную информацию о его содержимом.

## Часто задаваемые вопросы
### Могу ли я подписывать метаданные других форматов документов, кроме PPTX, с помощью GroupDocs.Signature для .NET?
Да, GroupDocs.Signature поддерживает различные форматы документов, включая Word, Excel, PDF и другие, для подписи с использованием метаданных.
### Совместим ли GroupDocs.Signature для .NET с .NET Core?
Да, библиотека совместима как с .NET Framework, так и с .NET Core.
### Могу ли я настроить внешний вид подписей метаданных?
Да, вы можете настроить внешний вид, положение и другие свойства подписей метаданных в соответствии с вашими требованиями.
### Обеспечивает ли GroupDocs.Signature для .NET шифрование подписанных документов?
Да, GroupDocs.Signature предлагает варианты шифрования для защиты подписанных документов от несанкционированного доступа.
### Доступна ли пробная версия для тестирования перед покупкой?
 Да, вы можете воспользоваться бесплатной пробной версией GroupDocs.Signature для .NET на сайте[здесь](https://releases.groupdocs.com/).