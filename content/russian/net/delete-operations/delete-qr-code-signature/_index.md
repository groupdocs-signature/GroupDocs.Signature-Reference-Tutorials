---
title: Удалить подпись QR-кода из документа
linktitle: Удалить подпись QR-кода из документа
second_title: GroupDocs.Signature .NET API
description: Узнайте, как удалять подписи QR-кода из документов с помощью GroupDocs.Signature для .NET. Следуйте нашему пошаговому руководству для эффективного управления подписями.
weight: 16
url: /ru/net/delete-operations/delete-qr-code-signature/
---
## Введение
В этом руководстве мы покажем вам процесс удаления подписи QR-кода из документа с помощью GroupDocs.Signature для .NET. Следуйте этим пошаговым инструкциям, чтобы эффективно удалить подписи QR-кода.
## Предварительные условия
Прежде чем начать, убедитесь, что у вас есть следующие предварительные условия:
-  GroupDocs.Signature для .NET: убедитесь, что в вашем проекте .NET установлена библиотека GroupDocs.Signature. Вы можете скачать его с[здесь](https://releases.groupdocs.com/signature/net/).
- Документ с подписью QR-кода: подготовьте документ, содержащий подписи QR-кода, которые вы хотите удалить.
- Базовые знания C#: ознакомьтесь с основами языка программирования C#.

## Импорт пространств имен
Прежде чем углубиться в код, импортируйте необходимые пространства имен в файл C#:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Шаг 1. Определите пути к файлам
```csharp
// Путь к каталогу документов.
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
// Определите путь к выходному файлу для измененного документа.
string outputFilePath = Path.Combine("Your Document Directory", "DeleteQRCode", fileName);
// Скопируйте исходный файл, поскольку метод «Удалить» работает с тем же документом.
File.Copy(filePath, outputFilePath, true);
```
## Шаг 2. Инициализация объекта подписи
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Создайте опции для поиска подписей QR-кода.
    QrCodeSearchOptions options = new QrCodeSearchOptions();
    // Найдите подписи QR-кода в документе.
    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```
## Шаг 3. Проверьте наличие подписи QR-кода
```csharp
    if (signatures.Count > 0)
    {
        // Получите первую подпись QR-кода, найденную в документе.
        QrCodeSignature qrCodeSignature = signatures[0];
```
## Шаг 4. Удалите подпись QR-кода
```csharp
        // Удалите подпись QR-кода из документа.
        bool result = signature.Delete(qrCodeSignature);
        if (result)
        {
            Console.WriteLine($"Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
        }
        else
        {
            Helper.WriteError($"Signature was not deleted from the document! Signature with Barcode '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was not found!");
        }
    }
}
```
Поздравляем! Вы успешно удалили подпись QR-кода из документа с помощью GroupDocs.Signature для .NET.

## Заключение
В этом уроке мы узнали, как удалить подпись QR-кода из документа с помощью GroupDocs.Signature для .NET. Следуя предоставленным инструкциям, вы сможете эффективно управлять подписями и манипулировать ими в своих приложениях .NET.
## Часто задаваемые вопросы
### Могу ли я удалить несколько подписей QR-кода из документа?
Да, вы можете изменить код, чтобы он перебирал все подписи QR-кода и соответственно удалял их.
### Поддерживает ли GroupDocs.Signature другие типы подписей помимо QR-кодов?
Да, GroupDocs.Signature поддерживает различные типы подписей, такие как текст, изображение, штрих-код и т. д.
### Совместим ли GroupDocs.Signature со всеми форматами документов?
GroupDocs.Signature поддерживает широкий спектр форматов документов, включая PDF, Microsoft Word, Excel, PowerPoint и другие.
### Можно ли настроить параметры поиска подписей?
Да, вы можете настроить параметры поиска в соответствии со своими требованиями, чтобы находить конкретные подписи в документе.
### Доступна ли пробная версия для GroupDocs.Signature?
 Да, вы можете получить доступ к бесплатной пробной версии GroupDocs.Signature на сайте[здесь](https://releases.groupdocs.com/).