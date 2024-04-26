---
title: Подписание с несколькими вариантами
linktitle: Подписание с несколькими вариантами
second_title: GroupDocs.Signature .NET API
description: Узнайте, как подписывать документы с несколькими вариантами, используя GroupDocs.Signature для .NET. Повысьте безопасность документов с помощью текста, штрих-кода, QR-кода, цифровых изображений и изображений.
type: docs
weight: 14
url: /ru/net/advanced-signature-techniques/sign-with-multiple-options/
---
## Введение
В этом руководстве мы рассмотрим, как подписать документ, используя несколько вариантов подписи, с помощью библиотеки GroupDocs.Signature для .NET. Подписание документов с использованием различных параметров, таких как текст, штрих-код, QR-код, цифровые подписи, изображения и подписи метаданных, может обеспечить универсальность и повысить безопасность документов.
## Предварительные условия
Прежде чем приступить к работе, убедитесь, что у вас есть следующие предварительные условия:
1.  GroupDocs.Signature для библиотеки .NET: загрузите и установите библиотеку GroupDocs.Signature для .NET с сайта[здесь](https://releases.groupdocs.com/signature/net/).
2. Среда разработки: настройте среду разработки с установленной .NET Framework.
3. Документ для подписи: подготовьте документ (например, sample.docx), который вы хотите подписать.
4. Сертификаты и изображения. Подготовьте все необходимые сертификаты и изображения для цифровых и графических подписей.

## Импортировать пространства имен
Сначала импортируйте необходимые пространства имен для использования библиотеки GroupDocs.Signature в вашем .NET-приложении:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Шаг 1. Загрузите документ
```csharp
string filePath = "sample.docx";
string outputFilePath = Path.Combine("Your Document Directory", "SignWithMultiple", "SignWithMultiple.docx");
using (Signature signature = new Signature(filePath))
{
    // Ваш код продолжается...
}
```
## Шаг 2. Определите параметры подписи
Определите несколько вариантов подписи разных типов и настроек, таких как текст, штрих-код, QR-код, цифровые подписи, изображения и подписи метаданных:
```csharp
TextSignOptions textOptions = new TextSignOptions("Text signature")
{
    VerticalAlignment = VerticalAlignment.Top,
    HorizontalAlignment = HorizontalAlignment.Left
};
BarcodeSignOptions barcodeOptions = new BarcodeSignOptions("123456")
{
    EncodeType = BarcodeTypes.Code128,
    Left = 0,
    Top = 150,
    Height = 50,
    Width = 200
};
// Определите другие параметры подписи (например, QR-код, цифровую подпись, изображение, метаданные)...
```
## Шаг 3. Создайте список вариантов подписи.
Определите список параметров подписи, содержащий все ранее определенные параметры:
```csharp
List<SignOptions> listOptions = new List<SignOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
// Добавьте в список другие варианты подписи...
```
## Шаг 4: Подпишите документ
Подпишите документ списком вариантов подписи и сохраните подписанный документ:
```csharp
SignResult result = signature.Sign(outputFilePath, listOptions);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Заключение
Подписание документов с несколькими вариантами с помощью GroupDocs.Signature для .NET обеспечивает надежное решение для повышения безопасности и универсальности документов. Следуя шагам, описанным в этом руководстве, вы сможете легко интегрировать различные типы подписей в свои приложения .NET.
## Часто задаваемые вопросы
### Могу ли я использовать собственные изображения для цифровых подписей?
Да, вы можете указать собственные изображения для цифровых подписей с помощью библиотеки GroupDocs.Signature.
### Совместим ли GroupDocs.Signature с различными форматами документов?
Да, GroupDocs.Signature поддерживает различные форматы документов, включая DOCX, PDF, PPTX и другие.
### Могу ли я настроить внешний вид текстовых подписей?
Конечно, вы можете настроить внешний вид текстовых подписей, включая размер, цвет и стиль шрифта.
### Обеспечивает ли GroupDocs.Signature шифрование цифровых подписей?
Да, GroupDocs.Signature предлагает варианты шифрования цифровых подписей для обеспечения безопасности документов.
### Доступна ли пробная версия GroupDocs.Signature для .NET?
 Да, вы можете загрузить бесплатную пробную версию GroupDocs.Signature для .NET с сайта[здесь](https://releases.groupdocs.com/).