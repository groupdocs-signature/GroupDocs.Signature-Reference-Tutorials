---
title: Удалить цифровую подпись из документа
linktitle: Удалить цифровую подпись из документа
second_title: GroupDocs.Signature .NET API
description: Узнайте, как удалять цифровые подписи из документов с помощью GroupDocs.Signature для .NET. Следуйте нашему пошаговому руководству для эффективного управления.
weight: 13
url: /ru/net/delete-operations/delete-digital-signature/
---
## Введение
В мире цифровых документов обеспечение их подлинности и безопасности имеет первостепенное значение. Цифровые подписи играют решающую роль в проверке целостности электронных документов. GroupDocs.Signature для .NET предлагает мощные инструменты для эффективного управления цифровыми подписями в приложениях .NET.
## Предварительные условия
Прежде чем приступить к использованию GroupDocs.Signature для .NET для удаления цифровых подписей из документов, убедитесь, что у вас есть следующее:
1. Visual Studio: установите интегрированную среду разработки Visual Studio в вашей системе.
2.  GroupDocs.Signature для .NET: загрузите и установите GroupDocs.Signature для .NET с сайта[страница загрузки](https://releases.groupdocs.com/signature/net/).
3. Образец документа: подготовьте образец документа, содержащего цифровые подписи, для тестирования.

## Импортировать пространства имен
Для начала обязательно импортируйте необходимые пространства имен в свой проект .NET:
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```
## Шаг 1. Определите пути к файлам
Начните с определения путей к файлам для исходного документа и выходного документа:
```csharp
string filePath = "sample.pdf"_SIGNED_DIGITAL;
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteDigital", fileName);
```
## Шаг 2. Скопируйте исходный документ
 Поскольку`Delete` метод работает с тем же документом, необходимо скопировать исходный файл в новое место:
```csharp
File.Copy(filePath, outputFilePath, true);
```
## Шаг 3. Инициализация объекта подписи
 Инициализировать`Signature` объект с путем выходного файла:
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // Ваш код находится здесь
}
```
## Шаг 4. Поиск цифровых подписей
Поиск электронных цифровых подписей внутри документа:
```csharp
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
```
## Шаг 5. Удалите цифровую подпись
Если обнаружены цифровые подписи, удалите первую найденную подпись:
```csharp
if (signatures.Count > 0)
{
    DigitalSignature digitalSignature = signatures[0];
    bool result = signature.Delete(digitalSignature);
    if (result)
    {
        Console.WriteLine($"Digital signature #{digitalSignature.Thumbprint} from {digitalSignature.SignTime.ToShortDateString()} was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature# {digitalSignature.Thumbprint} was not found!");
    }
}
```

## Заключение
Управление цифровыми подписями в приложениях .NET становится проще с помощью GroupDocs.Signature. Следуя простым шагам, описанным выше, вы можете легко удалить цифровые подписи из своих документов, гарантируя целостность и безопасность данных.
## Часто задаваемые вопросы
### Могу ли я удалить несколько цифровых подписей из одного документа?
Да, вы можете изменить код, чтобы он перебирал все найденные цифровые подписи и соответственно удалял их.
### Поддерживает ли GroupDocs.Signature другие типы подписей, кроме цифровых?
Да, GroupDocs.Signature поддерживает различные типы подписей, включая электронные, цифровые и рукописные.
### Подходит ли GroupDocs.Signature для управления документами на уровне предприятия?
Безусловно, GroupDocs.Signature предназначен для удовлетворения потребностей как отдельных разработчиков, так и приложений уровня предприятия, предлагая надежные функции и масштабируемость.
### Могу ли я настроить процесс удаления цифровых подписей?
Да, GroupDocs.Signature предоставляет широкий спектр опций и настроек для настройки процесса удаления подписи в соответствии с вашими конкретными требованиями.
### Доступна ли пробная версия для тестирования GroupDocs.Signature?
 Да, вы можете скачать бесплатную пробную версию с сайта[страница релизов](https://releases.groupdocs.com/).