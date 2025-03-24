---
title: Получить информацию о документе
linktitle: Получить информацию о документе
second_title: GroupDocs.Signature .NET API
description: Улучшите управление документами в .NET с помощью GroupDocs.Signature. Получите информацию о документе шаг за шагом. Поддерживает различные форматы.
weight: 11
url: /ru/net/document-preview-operations/retrieve-document-information/
---
## Введение
В сфере цифровой документации первостепенное значение имеет обеспечение ее подлинности и целостности. GroupDocs.Signature для .NET предоставляет надежное решение для управления подписями документов в среде .NET. В этом руководстве мы углубимся в процесс получения информации о документе с помощью GroupDocs.Signature для .NET, разбивая каждый шаг для полного понимания.
## Предварительные условия
Прежде чем приступить к изучению руководства, убедитесь, что у вас есть следующие предварительные условия:
1.  Установка: Установите GroupDocs.Signature для .NET, загрузив его с сайта[здесь](https://releases.groupdocs.com/signature/net/).
2. Среда .NET: иметь практические знания .NET Framework.
3. Документ: подготовьте образец документа (например, «sample_multiple_signatures.docx») для целей тестирования.

## Импорт пространств имен
Прежде чем приступить к процессу получения подписи документа, импортируйте необходимые пространства имен:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```

## Шаг 1. Установите путь к файлу документа:
Определите путь к файлу документа, из которого вы хотите получить информацию.
```csharp
string filePath = "sample_multiple_signatures.docx";
```
## Шаг 2. Создание экземпляра объекта подписи:
 Создайте экземпляр`Signature` класс, передав путь к файлу документа.
```csharp
using (Signature signature = new Signature(filePath))
{

}
```
## Шаг 3. Получение информации о документе:
 Используйте`GetDocumentInfo()` метод для получения полной информации о документе.
```csharp
IDocumentInfo documentInfo = signature.GetDocumentInfo();
```
## Шаг 4. Отображение свойств документа:
Вывод различных свойств документа, таких как формат, расширение, размер, количество страниц и т. д.
```csharp
Console.WriteLine($"Document properties {Path.GetFileName(filePath)}:");
Console.WriteLine($" - format : {documentInfo.FileType.FileFormat}");
Console.WriteLine($" - extension : {documentInfo.FileType.Extension}");
Console.WriteLine($" - size : {documentInfo.Size}");
Console.WriteLine($" - page count : {documentInfo.PageCount}");
Console.WriteLine($" - Form Fields count : {documentInfo.FormFields.Count}");
Console.WriteLine($" - Text signatures count : {documentInfo.TextSignatures.Count}");
Console.WriteLine($" - Image signatures count : {documentInfo.ImageSignatures.Count}");
Console.WriteLine($" - Digital signatures count : {documentInfo.DigitalSignatures.Count}");
Console.WriteLine($" - Barcode signatures count : {documentInfo.BarcodeSignatures.Count}");
Console.WriteLine($" - QrCode signatures count : {documentInfo.QrCodeSignatures.Count}");
Console.WriteLine($" - FormField signatures count : {documentInfo.FormFieldSignatures.Count}");
foreach (PageInfo pageInfo in documentInfo.Pages)
{
   Console.WriteLine($" - page-{pageInfo.PageNumber} Width {pageInfo.Width}, Height {pageInfo.Height}");
}
```


## Заключение
GroupDocs.Signature для .NET предлагает мощный набор инструментов для беспрепятственного управления подписями документов в рамках .NET. Следуя инструкциям, описанным в этом руководстве, вы сможете эффективно получить полную информацию о своих документах, что позволит расширить возможности управления документами.

## Часто задаваемые вопросы
### Может ли GroupDocs.Signature для .NET обрабатывать документы нескольких форматов?
Да, GroupDocs.Signature поддерживает широкий спектр форматов документов, включая, помимо прочего, DOCX, PDF, PNG и JPEG.
### Доступна ли пробная версия GroupDocs.Signature для .NET?
 Да, вы можете получить доступ к пробной версии с[здесь](https://releases.groupdocs.com/).
### Предоставляет ли GroupDocs.Signature для .NET поддержку цифровых подписей?
Безусловно, GroupDocs.Signature предлагает надежную поддержку цифровых подписей, гарантируя подлинность и целостность документов.
### Где я могу найти дополнительную документацию и поддержку GroupDocs.Signature для .NET?
 Вы можете обратиться к подробной документации[здесь](https://tutorials.groupdocs.com/signature/net/) , а для получения поддержки посетите форум GroupDocs.[здесь](https://forum.groupdocs.com/c/signature/13).
### Можно ли получить временные лицензии на GroupDocs.Signature для .NET?
 Да, временные лицензии доступны для приобретения.[здесь](https://purchase.groupdocs.com/temporary-license/).