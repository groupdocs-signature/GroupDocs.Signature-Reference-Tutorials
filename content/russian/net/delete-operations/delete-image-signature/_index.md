---
title: Удалить подпись изображения
linktitle: Удалить подпись изображения
second_title: GroupDocs.Signature .NET API
description: Узнайте, как удалять подписи изображений из документов с помощью GroupDocs.Signature для .NET. Следуйте нашему пошаговому руководству для эффективного управления подписями.
weight: 14
url: /ru/net/delete-operations/delete-image-signature/
---

# Удалить подпись изображения

## Введение
В этом руководстве мы рассмотрим, как удалять подписи изображений из документов с помощью GroupDocs.Signature для .NET. GroupDocs.Signature — мощная библиотека, позволяющая разработчикам работать с цифровыми подписями, штампами и полями форм в различных форматах документов.
## Предварительные условия
Прежде чем мы начнем, убедитесь, что у вас есть следующее:
### 1. GroupDocs.Signature для .NET
 Загрузите и установите GroupDocs.Signature для .NET с сайта[Веб-сайт](https://releases.groupdocs.com/signature/net/). Следуйте инструкциям по установке, приведенным в документации.
### 2. .NET Framework
Убедитесь, что на вашем компьютере установлена .NET Framework.
## Импортировать пространства имен
Включите в свой проект необходимые пространства имен:
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
Давайте разобьем процесс удаления подписей изображений на несколько этапов:
## Шаг 1. Определите пути к файлам
Сначала укажите пути для входного документа и выходного документа после удаления подписи:
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteImage", fileName);
```
## Шаг 2. Скопируйте исходный файл
 Поскольку`Delete`метод работает с тем же документом, необходимо скопировать исходный файл в другое место:
```csharp
File.Copy(filePath, outputFilePath, true);
```
## Шаг 3. Инициализация объекта подписи
 Создайте экземпляр`Signature` class и укажите путь к выходному документу:
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Код находится здесь
}
```
## Шаг 4. Поиск сигнатур изображений
Определите параметры поиска и найдите подписи изображений в документе:
```csharp
ImageSearchOptions options = new ImageSearchOptions();
List<ImageSignature> signatures = signature.Search<ImageSignature>(options);
```
## Шаг 5. Удаление подписи изображения
Если подписи изображений найдены, удалите первую:
```csharp
if (signatures.Count > 0)
{
    ImageSignature imageSignature = signatures[0];
    bool result = signature.Delete(imageSignature);
    if (result)
    {
        Console.WriteLine($"Image signature at location {imageSignature.Left}x{imageSignature.Top} and Size {imageSignature.Size} was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature at location {imageSignature.Left}x{imageSignature.Top} and Size {imageSignature.Size} was not found!");
    }
}
```
## Заключение
В этом уроке мы узнали, как удалять подписи изображений из документов с помощью GroupDocs.Signature для .NET. Следуя пошаговому руководству, разработчики смогут эффективно управлять цифровыми подписями в своих приложениях.
## Часто задаваемые вопросы
### Могу ли я удалить несколько подписей изображений из документа?
 Да, вы можете изменить код, чтобы удалить несколько подписей изображений, перебирая`signatures` список.
### Поддерживает ли GroupDocs.Signature другие форматы документов, кроме DOCX?
Да, GroupDocs.Signature поддерживает широкий спектр форматов документов, включая PDF, PPT, XLS и другие.
### Доступна ли пробная версия GroupDocs.Signature для .NET?
 Да, вы можете скачать бесплатную пробную версию с сайта[Веб-сайт](https://releases.groupdocs.com/).
### Как я могу получить поддержку для GroupDocs.Signature?
 Вы можете посетить[Форум GroupDocs.Подпись](https://forum.groupdocs.com/c/signature/13) за помощь и поддержку.
### Могу ли я приобрести временную лицензию для GroupDocs.Signature?
 Да, вы можете приобрести временную лицензию на сайте[страница покупки](https://purchase.groupdocs.com/temporary-license/).