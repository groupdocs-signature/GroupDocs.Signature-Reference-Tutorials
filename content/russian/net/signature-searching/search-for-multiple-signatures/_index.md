---
title: Поиск нескольких подписей
linktitle: Поиск нескольких подписей
second_title: GroupDocs.Signature .NET API
description: Узнайте, как искать несколько подписей в документах .NET с помощью GroupDocs.Signature для обеспечения эффективной безопасности и целостности документов.
weight: 14
url: /ru/net/signature-searching/search-for-multiple-signatures/
---

# Поиск нескольких подписей

## Введение
GroupDocs.Signature для .NET — это мощная библиотека, которая позволяет разработчикам добавлять, искать и удалять различные типы подписей в популярных форматах документов с помощью приложений .NET. В этом руководстве мы сосредоточимся на поиске нескольких подписей в документе с помощью GroupDocs.Signature для .NET.
## Предварительные условия
Прежде чем мы начнем, убедитесь, что у вас есть следующие предварительные условия:
- Visual Studio установлена в вашей системе.
- Базовое понимание языка программирования C#.
- GroupDocs.Signature для библиотеки .NET, установленной в вашем проекте. Вы можете скачать его с[здесь](https://releases.groupdocs.com/signature/net/).

## Импортировать пространства имен
Во-первых, вам необходимо импортировать необходимые пространства имен для доступа к классам и методам, предоставляемым GroupDocs.Signature для .NET.
```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Шаг 1. Загрузите документ
Загрузите документ, в котором вы хотите найти несколько подписей. Убедитесь, что вы указали правильный путь к файлу.
```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Ваш код находится здесь
}
```
## Шаг 2. Определите параметры поиска
Определите параметры поиска для различных типов подписей, таких как текстовые, цифровые, штрих-коды, QR-коды и метаданные. Вы можете указать критерии поиска, такие как текст для сопоставления, тип соответствия и поиск по всем страницам.
```csharp
// Определите параметры поиска
TextSearchOptions textOptions = new TextSearchOptions()
{
    AllPages = true
};
DigitalSearchOptions digitalOptions = new DigitalSearchOptions()
{
    AllPages = true
};
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions()
{
    AllPages = true,
    Text = "123456",
    MatchType = TextMatchType.Exact
};
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions()
{
    AllPages = true,
    Text = "John",
    MatchType = TextMatchType.Contains
};
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```
## Шаг 3. Добавьте параметры поиска в список
Добавьте определенные параметры поиска в список.
```csharp
// Добавить опции в список
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
listOptions.Add(metadataOptions);
listOptions.Add(digitalOptions);
```
## Шаг 4. Поиск подписей
Найдите подписи в документе, используя заданные параметры поиска.
```csharp
// Поиск подписей в документе
SearchResult result = signature.Search(listOptions);
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains following signatures.");
    foreach (var resSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found at page {resSignature.PageNumber} with type {resSignature.SignatureType} and Id#: {resSignature.SignatureId}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## Заключение
В этом руководстве мы узнали, как искать несколько подписей в документе с помощью GroupDocs.Signature для .NET. Следуя предоставленным инструкциям, вы сможете эффективно находить различные типы подписей в своих документах, повышая безопасность и целостность документов.
## Часто задаваемые вопросы
### Могу ли я искать подписи в документах разных форматов?
Да, GroupDocs.Signature для .NET поддерживает широкий спектр форматов документов, включая Word, PDF, Excel и другие.
### Можно ли настроить критерии поиска подписей?
Конечно, вы можете настроить критерии поиска в соответствии со своими требованиями, например, указать точное совпадение текста или поиск по всем страницам.
### Предлагает ли GroupDocs.Signature для .NET поддержку цифровых подписей?
Да, вы можете искать цифровые подписи, а также другие типы, такие как текстовые подписи, подписи со штрих-кодом и QR-кодом.
### Могу ли я легко интегрировать функцию поиска по сигнатурам в свои приложения .NET?
Да, GroupDocs.Signature для .NET предоставляет простой API, который упрощает процесс интеграции.
### Где я могу найти дополнительную поддержку или помощь?
 Вы можете посетить форум GroupDocs.Signature.[здесь](https://forum.groupdocs.com/c/signature/13) для любых вопросов или помощи.