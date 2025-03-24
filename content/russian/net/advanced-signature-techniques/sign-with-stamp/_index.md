---
title: Подписание с помощью штампа с использованием GroupDocs.Signature
linktitle: Подписание печатью
second_title: GroupDocs.Signature .NET API
description: Узнайте, как легко добавлять штампы в документы .NET с помощью GroupDocs.Signature для .NET. Повысьте безопасность документов.
weight: 16
url: /ru/net/advanced-signature-techniques/sign-with-stamp/
---
## Введение
В этом руководстве мы покажем вам процесс подписания документа с помощью штампа с помощью GroupDocs.Signature для .NET. Следуя этим пошаговым инструкциям, вы сможете легко поставить подпись-штамп в свои документы.
## Предварительные условия
Прежде чем мы начнем, убедитесь, что у вас есть следующие предварительные условия:
1.  GroupDocs.Signature для .NET SDK: загрузите и установите SDK из[Веб-сайт](https://releases.groupdocs.com/signature/net/).
2. Среда разработки: убедитесь, что у вас настроена подходящая среда разработки для разработки .NET.
3. Документ для подписи: подготовьте документ (например, PDF), который вы хотите подписать печатью.

## Импорт пространств имен
Начните с импорта необходимых пространств имен в ваш проект:
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Шаг 1. Загрузите документ
```csharp
string filePath = "sample.pdf";
using (Signature signature = new Signature(filePath))
{
    // Ваш код находится здесь
}
```
## Шаг 2. Установите параметры штампа
```csharp
StampSignOptions options = new StampSignOptions()
{
    Left = 50,
    Top = 150,                    
    Width = 200,
    Height = 200
};
```
## Шаг 3. Настройте внешний вид штампа
```csharp
StampLine outerLine = new StampLine();
outerLine.Text = " * European Union ";
outerLine.TextRepeatType = StampTextRepeatType.FullTextRepeat;
outerLine.Font.Size = 12;
outerLine.Height = 22;
outerLine.TextBottomIntent = 6;
outerLine.TextColor = Color.WhiteSmoke;
outerLine.BackgroundColor = Color.DarkSlateBlue;
options.OuterLines.Add(outerLine);
StampLine innerLine = new StampLine();
innerLine.Text = "John Smith";
innerLine.TextColor = Color.MediumVioletRed;
innerLine.Font.Size = 20;
innerLine.Font.Bold = true;
innerLine.Height = 40;
options.InnerLines.Add(innerLine);
```
## Шаг 4: Подпишите документ
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithStamp", fileName);
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## Заключение
Добавление подписей штампов в документы с помощью GroupDocs.Signature для .NET — это простой процесс, как показано в этом руководстве. С помощью предоставленных шагов вы можете легко повысить безопасность и подлинность ваших документов.
## Часто задаваемые вопросы
### Могу ли я настроить внешний вид штампа-подписи?
Да, вы можете настроить различные аспекты, такие как текст, шрифт, цвет и расположение подписи штампа, в соответствии с вашими требованиями.
### Поддерживает ли GroupDocs.Signature подписание документов нескольких форматов?
Да, GroupDocs.Signature поддерживает широкий спектр форматов документов, включая PDF, Microsoft Word, Excel, PowerPoint и другие.
### Доступна ли пробная версия для GroupDocs.Signature?
 Да, вы можете получить доступ к бесплатной пробной версии на сайте[Веб-сайт](https://releases.groupdocs.com/).
### Могу ли я добавить несколько подписей в один документ?
Конечно, GroupDocs.Signature позволяет добавлять в один документ несколько подписей, включая печати, текст, изображения и цифровые подписи.
### Где я могу найти поддержку, если у меня возникнут какие-либо проблемы во время реализации?
 Вы можете найти поддержку и помощь на форуме сообщества GroupDocs.Signature.[здесь](https://forum.groupdocs.com/c/signature/13).