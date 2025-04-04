---
title: Подписание цифровой подписью
linktitle: Подписание цифровой подписью
second_title: GroupDocs.Signature .NET API
description: Узнайте, как подписывать документы цифровой подписью в .NET с помощью GroupDocs.Signature. Повысьте безопасность и подлинность с помощью этого подробного руководства.
weight: 12
url: /ru/net/advanced-signature-techniques/sign-with-digital/
---

# Подписание цифровой подписью

## Введение
Цифровые подписи играют решающую роль в обеспечении подлинности и целостности электронных документов. В области разработки .NET GroupDocs.Signature предлагает мощное решение для простой интеграции цифровых подписей в ваши приложения. Это руководство проведет вас через процесс подписания документа с помощью цифровой подписи с помощью GroupDocs.Signature для .NET.
## Предварительные условия
Прежде чем мы углубимся в реализацию, убедитесь, что у вас есть следующие предварительные условия:
1.  GroupDocs.Signature для .NET: загрузите и установите GroupDocs.Signature для .NET с сайта[страница загрузки](https://releases.groupdocs.com/signature/net/).
2. Цифровой сертификат: получите цифровой сертификат (.pfx), который будет использоваться для подписи документа. Если у вас его нет, вы можете создать самозаверяющий сертификат или получить его в доверенном центре сертификации.
3. Документ для подписи: подготовьте документ (например, PDF), который вы хотите подписать цифровой подписью. Убедитесь, что у вас есть необходимые разрешения для доступа и изменения документа.
4. Изображение подписи. При желании вы можете предоставить изображение своей подписи, которое будет встроено в документ. Это придает цифровой подписи индивидуальность.

## Импортировать пространства имен
Сначала давайте импортируем необходимые пространства имен в наш код C#:
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## Шаг 1. Укажите пути к файлам и параметры.
Определите пути к файлам для подписываемого документа, изображение подписи (если применимо) и цифровой сертификат.
```csharp
string filePath = "sample.pdf";
string fileName = Path.GetFileName(filePath);
string imagePath = "signature_handwrite.jpg";
string certificatePath = "YourSignature.pfx";
string outputFilePath = Path.Combine("Your Document Directory", "SignWithDigital", fileName);
```
## Шаг 2. Инициализация объекта подписи
 Создайте экземпляр`Signature` класс, передав путь к подписываемому документу.
```csharp
using (Signature signature = new Signature(filePath))
{
    // Определите параметры цифровой подписи
    DigitalSignOptions options = new DigitalSignOptions(certificatePath)
    {
        ImageFilePath = imagePath, // Установите путь к файлу изображения (необязательно)
        Left = 50,                 //Установите координату X положения подписи.
        Top = 50,                  // Установите координату Y позиции подписи.
        PageNumber = 1,            // Укажите номер страницы для подписи
        Password = "1234567890"    // Установите пароль для сертификата (если требуется)
    };
    // Шаг 3: Подпишите документ
    SignResult result = signature.Sign(outputFilePath, options);
    // Шаг 4: Отображение результата
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## Заключение
В этом руководстве мы рассмотрели, как подписать документ с помощью цифровой подписи с помощью GroupDocs.Signature для .NET. Следуя этим простым шагам, вы сможете повысить безопасность и подлинность своих электронных документов, гарантируя, что они останутся защищенными от несанкционированного доступа и будут иметь юридическую силу.
## Часто задаваемые вопросы
### Что такое цифровая подпись?
Цифровая подпись — это криптографический метод, используемый для проверки подлинности и целостности цифровых документов или сообщений.
### Могу ли я подписывать документы с помощью GroupDocs.Signature, используя самозаверяющий сертификат?
Да, вы можете подписывать документы, используя самозаверяющий сертификат, созданный с помощью таких инструментов, как OpenSSL или Microsoft MakeCert.
### Совместим ли GroupDocs.Signature с различными форматами документов?
Да, GroupDocs.Signature поддерживает широкий спектр форматов документов, включая PDF, Word, Excel, PowerPoint и другие.
### Могу ли я настроить внешний вид своей цифровой подписи?
Абсолютно! GroupDocs.Signature позволяет настраивать различные аспекты вашей цифровой подписи, такие как ее положение, размер и внешний вид.
### Подходит ли GroupDocs.Signature для приложений уровня предприятия?
Да, GroupDocs.Signature предлагает надежные функции и масштабируемость, что делает его идеальным выбором для приложений для подписания документов корпоративного уровня.