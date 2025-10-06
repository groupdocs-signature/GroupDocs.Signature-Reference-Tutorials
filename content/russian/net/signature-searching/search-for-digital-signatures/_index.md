---
"description": "Освойте поиск цифровых подписей в документах с помощью GroupDocs.Signature для .NET. Повысьте безопасность и верификацию документов с помощью нашего подробного пошагового руководства."
"linktitle": "Поиск цифровых подписей"
"second_title": "GroupDocs.Signature .NET API"
"title": "Поиск цифровых подписей в документах"
"url": "/ru/net/signature-searching/search-for-digital-signatures/"
"weight": 11
type: docs
---
## Введение

В современном цифровом мире обеспечение подлинности и целостности документов критически важно для предприятий и организаций. Цифровые подписи обеспечивают надёжный механизм проверки подлинности документов и обнаружения несанкционированных изменений. GroupDocs.Signature для .NET предлагает комплексное решение для работы с цифровыми подписями в различных форматах документов, позволяя разработчикам легко интегрировать функции подписи в свои приложения .NET.

В этом руководстве вы узнаете о процессе поиска цифровых подписей в документах с использованием GroupDocs.Signature для .NET, предоставив подробные объяснения и практические примеры кода.

## Предпосылки

Прежде чем углубляться в детали реализации, убедитесь, что у вас есть следующие предварительные условия:

1. GroupDocs.Signature для .NET: Загрузите и установите библиотеку с сайта [здесь](https://releases.groupdocs.com/signature/net/).
   
2. Среда разработки: настройте среду разработки .NET с помощью Visual Studio или предпочитаемой вами IDE.
   
3. Образцы документов: подготовьте образцы документов, содержащих цифровые подписи, для целей тестирования.

4. Базовые знания: знакомство с языком программирования C# и основами .NET Framework.

## Импорт пространств имен

Начните с импорта необходимых пространств имен для доступа к функциональным возможностям, предоставляемым GroupDocs.Signature для .NET:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Теперь давайте разобьем процесс поиска цифровых подписей на понятные и выполнимые шаги:

## Шаг 1: Инициализация объекта подписи

Начните с создания экземпляра `Signature` класс, передающий путь к вашему документу:

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // Здесь будет добавлен код для поиска цифровых подписей.
}
```

## Шаг 2: Поиск цифровых подписей

Далее используйте `Search` метод с `SignatureType.Digital` параметр для поиска цифровых подписей в документе:

```csharp
// Поиск цифровых подписей в документе
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
```

## Шаг 3: Обработка и отображение результатов

Наконец, обработайте результаты поиска и отобразите релевантную информацию о найденных цифровых подписях:

```csharp
Console.WriteLine($"\nSource document ['{filePath}'] contains the following digital signatures:");
foreach (var digitalSignature in signatures)
{
    Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation status: {digitalSignature.IsValid}");
    Console.WriteLine($"Certificate: Subject: {digitalSignature.Certificate?.SubjectName}");
    Console.WriteLine($"Certificate: Issuer: {digitalSignature.Certificate?.IssuerName}");
    Console.WriteLine($"Certificate: Serial Number: {digitalSignature.Certificate?.SerialNumber}");
    Console.WriteLine();
}
```

## Полный пример

Вот полный рабочий пример, демонстрирующий, как искать цифровые подписи в документе:

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SearchDigitalSignatures
{
    class Program
    {
        static void Main(string[] args)
        {
            // Путь к документу
            string filePath = "sample_multiple_signatures.docx";
            
            // Инициализировать экземпляр подписи
            using (Signature signature = new Signature(filePath))
            {
                // Поиск цифровых подписей в документе
                List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
                
                // Показать результаты поиска
                Console.WriteLine($"\nSource document ['{filePath}'] contains the following digital signatures:");
                
                if (signatures.Count > 0)
                {
                    foreach (var digitalSignature in signatures)
                    {
                        Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation status: {digitalSignature.IsValid}");
                        Console.WriteLine($"Certificate: Subject: {digitalSignature.Certificate?.SubjectName}");
                        Console.WriteLine($"Certificate: Issuer: {digitalSignature.Certificate?.IssuerName}");
                        Console.WriteLine($"Certificate: Serial Number: {digitalSignature.Certificate?.SerialNumber}");
                        Console.WriteLine();
                    }
                }
                else
                {
                    Console.WriteLine("No digital signatures found in the document.");
                }
            }
        }
    }
}
```

## Расширенные параметры поиска

Для более целевого поиска вы можете использовать `DigitalSearchOptions` чтобы настроить критерии поиска:

```csharp
// Создайте варианты цифрового поиска
DigitalSearchOptions options = new DigitalSearchOptions()
{
    // Искать только на определенных страницах (например, на страницах 1 и 2)
    PageNumber = 1,
    PagesSetup = new PagesSetup() { Pages = new List<int> { 1, 2 } },
    
    // Фильтр по комментариям в цифровых подписях
    Comments = "Approved",
    
    // Установите диапазон даты и времени для поиска
    SignDateTimeFrom = new DateTime(2022, 1, 1),
    SignDateTimeTo = DateTime.Now
};

// Поиск с конкретными параметрами
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(options);
```

## Работа с информацией сертификата

Цифровые подписи содержат ценную информацию сертификата, к которой вы можете получить доступ и проверить ее:

```csharp
foreach (var digitalSignature in signatures)
{
    if (digitalSignature.Certificate != null)
    {
        // Свойства сертификата доступа
        Console.WriteLine($"Certificate Valid From: {digitalSignature.Certificate.NotBefore}");
        Console.WriteLine($"Certificate Valid To: {digitalSignature.Certificate.NotAfter}");
        
        // Проверьте, находится ли сертификат в допустимом диапазоне дат.
        bool isDateValid = DateTime.Now >= digitalSignature.Certificate.NotBefore && 
                          DateTime.Now <= digitalSignature.Certificate.NotAfter;
        
        Console.WriteLine($"Certificate Date Validity: {isDateValid}");
        
        // Доступ к данным эмитента сертификата
        Console.WriteLine($"Certificate Issuer: {digitalSignature.Certificate.IssuerName}");
    }
}
```

## Заключение

GroupDocs.Signature для .NET предоставляет мощное и гибкое решение для поиска и проверки цифровых подписей в документах. В этом руководстве мы пошагово рассмотрели процесс реализации функции поиска цифровых подписей в приложениях .NET, предоставив вам знания для повышения безопасности и проверки целостности документов.

Используя GroupDocs.Signature, вы можете создать надежные системы управления документами, которые гарантируют подлинность и целостность ваших цифровых документов, способствуя доверию и соблюдению требований ваших бизнес-процессов.

## Часто задаваемые вопросы

### Может ли GroupDocs.Signature проверять действительность цифровых подписей?

Да, GroupDocs.Signature автоматически проверяет цифровые подписи во время поиска и предоставляет статус проверки через `IsValid` собственность `DigitalSignature` сорт.

### Какие форматы документов поддерживают поиск по цифровой подписи?

GroupDocs.Signature поддерживает поиск цифровых подписей в различных форматах, включая PDF, документы Microsoft Office (Word, Excel, PowerPoint), форматы OpenOffice и другие.

### Можно ли искать цифровые подписи в документах, защищенных паролем?

Да, вы можете искать цифровые подписи в документах, защищенных паролем, указав пароль при инициализации `Signature` объект:

```csharp
LoadOptions loadOptions = new LoadOptions() { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // Поиск цифровых подписей
}
```

### Как проверить, была ли цифровая подпись создана конкретным человеком?

Вы можете проверить имя субъекта сертификата и другие свойства, чтобы проверить личность подписавшего:

```csharp
foreach (var signature in signatures)
{
    if (signature.Certificate?.SubjectName?.Contains("John Doe") == true)
    {
        Console.WriteLine("Found signature by John Doe");
    }
}
```

### Могу ли я извлечь открытый ключ из сертификата цифровой подписи?

Да, вы можете получить доступ к информации открытого ключа через свойства сертификата:

```csharp
if (signature.Certificate != null)
{
    // Доступ к информации открытого ключа
    Console.WriteLine($"Public Key: {signature.Certificate.GetPublicKeyString()}");
}
```

## Смотрите также

* [Справочник API](https://reference.groupdocs.com/signature/net/)
* [Примеры кода](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Документация по продукту](https://docs.groupdocs.com/signature/net/)
* [Страница продукта](https://products.groupdocs.com/signature/net/)
* [Загрузить последнюю версию](https://releases.groupdocs.com/signature/net/)
* [Статьи блога](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Форум поддержки](https://forum.groupdocs.com/c/signature/13)
* [Временная лицензия](https://purchase.groupdocs.com/temporary-license/)