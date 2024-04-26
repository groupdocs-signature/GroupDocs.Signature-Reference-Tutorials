---
title: Удалить несколько подписей из документа
linktitle: Удалить несколько подписей из документа
second_title: GroupDocs.Signature .NET API
description: Легко удаляйте несколько подписей из документов с помощью GroupDocs.Signature для .NET. Оптимизируйте рабочий процесс управления документами.
type: docs
weight: 15
url: /ru/net/delete-operations/delete-multiple-signatures/
---
## Введение
В цифровом мире управление документами часто предполагает работу с различными подписями. Программное удаление нескольких подписей из документа может упростить рабочие процессы и повысить эффективность. Благодаря GroupDocs.Signature для .NET эта задача становится простой и понятной. Это руководство шаг за шагом проведет вас через процесс удаления нескольких подписей из документа.
## Предварительные условия
Прежде чем приступить к изучению руководства, убедитесь, что у вас есть следующие предварительные условия:
- Базовое понимание языка программирования C#.
- Установлена библиотека GroupDocs.Signature для .NET.
- Образец документа с несколькими подписями для тестирования.

## Импортировать пространства имен
Начните с импорта необходимых пространств имен для доступа к функциям GroupDocs.Signature для .NET:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Шаг 1. Определите путь к документу и имя файла.
Задайте путь к файлу документа, содержащего несколько подписей. Убедитесь, что у вас правильный путь к файлу и имя файла:
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
```
## Шаг 2. Скопируйте документ для обработки.
Чтобы не изменять исходный документ, создайте копию для обработки:
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "DeleteMultiple", fileName);
File.Copy(filePath, outputFilePath, true);
```
## Шаг 3. Инициализация объекта подписи
Создайте экземпляр объекта Signature, используя путь к выходному файлу:
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Здесь находится код обработки подписи
}
```
## Шаг 4. Определите параметры поиска
Определите различные параметры поиска для идентификации подписей в документе. Опции включают текстовый поиск, поиск изображений, поиск по штрих-коду и поиск по QR-коду:
```csharp
TextSearchOptions textSearchOptions = new TextSearchOptions();
ImageSearchOptions imageSearchOptions = new ImageSearchOptions();
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions();
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions();
// Добавить опции в список
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textSearchOptions);
listOptions.Add(imageSearchOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
```
## Шаг 5. Поиск подписей
Выполните операцию поиска, чтобы найти все подписи в документе на основе определенных параметров поиска:
```csharp
SearchResult result = signature.Search(listOptions);
```
## Шаг 6. Удаление подписей
Если подписи обнаружены, приступаем к их удалению:
```csharp
if (result.Signatures.Count > 0)
{
    // Попытайтесь удалить все подписи
    DeleteResult deleteResult = signature.Delete(result.Signatures);
    //Проверьте, прошло ли удаление успешно
    if(deleteResult.Succeeded.Count == result.Signatures.Count)
    {
        Console.WriteLine("\nAll signatures were successfully deleted!");                        
    }
    else
    {
        Console.WriteLine($"Successfully deleted signatures : {deleteResult.Succeeded.Count}");
        Helper.WriteError($"Not deleted signatures : {deleteResult.Failed.Count}");
    }
    // Отображать информацию об удаленных подписях
    Console.WriteLine("\nList of deleted signatures:");
    int number = 1;
    foreach(BaseSignature temp in deleteResult.Succeeded)
    {
        Console.WriteLine($"Signature #{number++}: Type: {temp.SignatureType} Id:{temp.SignatureId}, Location: {temp.Left}x{temp.Top}. Size: {temp.Width}x{temp.Height}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## Заключение
Программное удаление нескольких подписей из документа является важной задачей в управлении документами. Благодаря GroupDocs.Signature для .NET этот процесс становится эффективным и надежным. Следуя инструкциям, описанным в этом руководстве, вы можете легко интегрировать функцию удаления подписи в свои приложения .NET.
## Часто задаваемые вопросы
### Может ли GroupDocs.Signature для .NET обрабатывать различные форматы документов?
Да, GroupDocs.Signature для .NET поддерживает широкий спектр форматов документов, включая DOCX, PDF, PPTX, XLSX и другие.
### Можно ли настроить параметры поиска для обнаружения сигнатур?
Конечно, вы можете настроить параметры поиска, такие как поиск по тексту, поиск по изображению, поиск по штрих-коду и поиск по QR-коду, в соответствии с вашими конкретными требованиями.
### Предоставляет ли GroupDocs.Signature для .NET механизмы обработки ошибок?
Да, библиотека предлагает надежные возможности обработки ошибок, обеспечивающие плавное выполнение задач по обработке документов.
### Могу ли я интегрировать GroupDocs.Signature для .NET с другими сторонними библиотеками?
Конечно, GroupDocs.Signature для .NET спроектирована с возможностью полной интеграции с другими библиотеками .NET, обеспечивая гибкость и расширяемость.
### Где я могу найти дополнительную поддержку и ресурсы для GroupDocs.Signature для .NET?
 Вы можете посетить GroupDocs[Форум](https://forum.groupdocs.com/c/signature/13) посвящен обсуждениям, связанным с подписями, и обращается за помощью к сообществу и экспертам.