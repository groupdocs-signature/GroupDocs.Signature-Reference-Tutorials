---
title: Удалить подпись по идентификатору
linktitle: Удалить подпись по идентификатору
second_title: GroupDocs.Signature .NET API
description: Узнайте, как удалить подпись по идентификатору в документах .NET с помощью библиотеки GroupDocs.Signature. Простое пошаговое руководство.
type: docs
weight: 11
url: /ru/net/delete-operations/delete-signature-by-id/
---
## Введение
В этом руководстве мы рассмотрим, как удалить подпись по ее идентификатору с помощью GroupDocs.Signature для .NET. GroupDocs.Signature для .NET — это мощная библиотека, которая позволяет разработчикам добавлять, удалять или проверять цифровые подписи в различных форматах документов с помощью приложений .NET.
## Предварительные условия
Прежде чем мы начнем, убедитесь, что у вас есть следующие предварительные условия:
1.  GroupDocs.Signature для библиотеки .NET: загрузите и установите библиотеку с сайта[здесь](https://releases.groupdocs.com/signature/net/).
2. .NET Framework: убедитесь, что в вашей системе установлена .NET Framework.
3. Документ с подписью: подготовьте документ (например, DOCX, PDF) с подписью, которую вы хотите удалить.

## Импортировать пространства имен
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Шаг 1. Определите пути к файлам
Сначала укажите путь к файлу документа, содержащего подпись, и путь к выходному файлу, в котором будет сохранен измененный документ.
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteById", fileName);
```
## Шаг 2. Скопируйте документ
 Поскольку`Delete` метод изменяет документ на месте, лучше всего создать копию исходного документа.
```csharp
File.Copy(filePath, outputFilePath, true);
```
## Шаг 3. Удаление подписи по идентификатору
 Инициализируйте`Signature` объект с путем к файлу документа и используйте`Delete` метод удаления подписи по ее идентификатору.
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    string id = @"eff64a14-dad9-47b0-88e5-2ee4e3604e71";
    bool result = signature.Delete(id);
    if (result)
    {
        Console.WriteLine($"Signature with Id# '{id}' was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature with id# '{id}' was not found!");
    }
}
```

## Заключение
В этом руководстве мы узнали, как удалить подпись по ее идентификатору с помощью GroupDocs.Signature для .NET. Эта библиотека предоставляет удобный способ программного управления цифровыми подписями в различных форматах документов.
## Часто задаваемые вопросы
### Могу ли я удалить несколько подписей одновременно?
 Да, вы можете удалить несколько подписей, перебирая их идентификаторы и вызывая метод`Delete` метод для каждого идентификатора.
### Совместим ли GroupDocs.Signature для .NET со всеми форматами документов?
GroupDocs.Signature для .NET поддерживает широкий спектр форматов документов, включая PDF, DOCX, XLSX и другие.
### Могу ли я настроить внешний вид подписи?
Да, вы можете настроить внешний вид подписи, включая ее положение, размер, шрифт и цвет.
### Доступна ли пробная версия?
 Да, вы можете скачать бесплатную пробную версию с сайта[здесь](https://releases.groupdocs.com/).
### Где я могу найти помощь или поддержку по GroupDocs.Signature для .NET?
 Вы можете посетить форум поддержки[здесь](https://forum.groupdocs.com/c/signature/13) для оказания помощи.