---
"description": "Реализуйте безопасную проверку цифровой подписи в приложениях .NET с помощью GroupDocs.Signature. Пошаговое руководство с полными примерами кода для аутентификации документов."
"linktitle": "Проверить цифровую подпись"
"second_title": "GroupDocs.Signature .NET API"
"title": "Проверка цифровых подписей в документах"
"url": "/ru/net/verify-operations/verify-digital/"
"weight": 11
type: docs
---
## Введение

Цифровые подписи играют ключевую роль в обеспечении подлинности, целостности и неотказуемости документов в современных бизнес-процессах. В отличие от традиционных рукописных подписей, цифровые подписи используют криптографические методы для проверки личности подписчика и гарантируют, что документ не был изменён с момента подписания.

GroupDocs.Signature для .NET предоставляет комплексный набор инструментов, позволяющий разработчикам реализовать надежную проверку цифровых подписей в своих приложениях .NET. Это подробное руководство проведет вас через процесс проверки цифровых подписей в документах с помощью GroupDocs.Signature для .NET.

## Предпосылки

Перед внедрением функции проверки цифровой подписи убедитесь, что выполнены следующие предварительные условия:

1. GroupDocs.Signature для .NET: Загрузите и установите библиотеку с сайта [GroupDocs.Signature для релизов .NET](https://releases.groupdocs.com/signature/net/).
2. Среда разработки .NET: Visual Studio или любая совместимая среда разработки .NET.
3. Цифровой сертификат: файл цифрового сертификата (например, .pfx), который был использован для подписания документа, или сертификат, принадлежащий доверенной цепочке.
4. Документ для проверки: документ, содержащий цифровые подписи, требующие проверки.

## Импорт требуемых пространств имен

Начните с импорта необходимых пространств имен для доступа к функциональности GroupDocs.Signature:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Давайте разберем процесс проверки цифровых подписей на понятные и выполнимые шаги:

## Шаг 1: Укажите путь к документу

```csharp
// Путь к документу, содержащему цифровые подписи
string filePath = "sample_multiple_signatures.docx";
```

Замените путь в примере на фактический путь к вашему документу, содержащему цифровые подписи.

## Шаг 2: Инициализация объекта подписи

```csharp
// Создайте экземпляр класса Signature, передав путь к документу
using (Signature signature = new Signature(filePath))
{
    // Код подтверждения будет реализован здесь.
}
```

Класс Signature является основной точкой входа для всех операций в API GroupDocs.Signature.

## Шаг 3: Настройте параметры цифровой верификации

```csharp
// Настройка параметров проверки
DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
{
    Contact = "Mr.Smith",     // Ожидаемый контакт с подписантом
    Password = "1234567890",  // Пароль сертификата (при необходимости)
    AllPages = true           // Проверьте все страницы на наличие подписей.
};
```

Параметры проверки позволяют указать:
- Путь к файлу цифрового сертификата
- Ожидаемая контактная информация подписавшего
- Пароль для сертификата, если он защищен паролем
- Диапазон страниц для проверки (все страницы по умолчанию)

## Шаг 4: Выполните процесс проверки

```csharp
// Выполнить проверку
VerificationResult result = signature.Verify(options);
```

Это выполнит процесс проверки на основе указанных вами параметров.

## Шаг 5: Результаты проверки процесса

```csharp
// Проверьте результат проверки и действуйте соответствующим образом.
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid digital signatures!");
    
    // Отображение сведений о действительных подписях
    foreach (DigitalSignature digitalSignature in result.Succeeded)
    {
        Console.WriteLine($"\nValid signature found:");
        Console.WriteLine($"Signer: {digitalSignature.Subject}");
        Console.WriteLine($"Issuer: {digitalSignature.Issuer}");
        Console.WriteLine($"Valid From: {digitalSignature.ValidFrom}");
        Console.WriteLine($"Valid To: {digitalSignature.ValidTo}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    
    // При необходимости отобразить информацию о неудачных подписях.
    foreach (DigitalSignature failedSignature in result.Failed)
    {
        Console.WriteLine($"Failed signature reason: {failedSignature.Comments}");
    }
}
```

Этот код проверяет, была ли проверка успешной, и предоставляет подробную информацию о проверенных подписях.

## Полный пример

Вот полный рабочий пример, демонстрирующий проверку цифровой подписи:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace GroupDocs.Signature.Examples
{
    class Program
    {
        static void Main(string[] args)
        {
            // Путь к документу
            string filePath = "sample_multiple_signatures.docx";
            
            try
            {
                // Инициализировать экземпляр подписи
                using (Signature signature = new Signature(filePath))
                {
                    // Настройка параметров проверки
                    DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
                    {
                        Contact = "Mr.Smith",
                        Password = "1234567890"
                    };
                    
                    // Проверка подписей документов
                    VerificationResult result = signature.Verify(options);
                    
                    // Результаты проверки процесса
                    if (result.IsValid)
                    {
                        Console.WriteLine($"Document {filePath} contains valid digital signatures!");
                        
                        foreach (DigitalSignature item in result.Succeeded)
                        {
                            Console.WriteLine($"\nValid signature found.");
                            Console.WriteLine($"Subject: {item.Subject}");
                            Console.WriteLine($"Comments: {item.Comments}");
                            Console.WriteLine($"Sign Time: {item.SignTime}");
                        }
                    }
                    else
                    {
                        Console.WriteLine($"\nDocument {filePath} failed verification process.");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
            }
        }
    }
}
```

## Расширенные сценарии проверки

GroupDocs.Signature предоставляет дополнительные возможности для более сложных сценариев проверки:

### Проверка нескольких цифровых подписей

```csharp
// Создайте список вариантов проверки
List<VerifyOptions> listOptions = new List<VerifyOptions>();

// Добавить первые параметры проверки сертификата
listOptions.Add(new DigitalVerifyOptions("Certificate1.pfx")
{
    Contact = "John Smith"
});

// Добавить второй вариант проверки сертификата
listOptions.Add(new DigitalVerifyOptions("Certificate2.pfx")
{
    Contact = "Jane Doe"
});

// Подтвердите с помощью нескольких вариантов
VerificationResult result = signature.Verify(listOptions);
```

### Проверка подписей на определенных страницах

```csharp
// Проверяйте цифровые подписи только на первой странице
DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
{
    AllPages = false,
    PageNumber = 1
};
```

### Использование временной метки и проверки центра сертификации

```csharp
DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
{
    ValidateTimeStampOnly = true,   // Проверять только временную метку
    CertificateAuth = CertificateAuthType.Standard  // Проверяет сертификат подписчика
};
```

## Лучшие практики проверки цифровой подписи

1. Правильное управление сертификатами: надежно храните файлы сертификатов и управляйте паролями надлежащим образом.
2. Проверка сертификата: Реализуйте проверку цепочки сертификатов, чтобы убедиться в действительности самого сертификата.
3. Обработка ошибок: реализуйте надежную обработку ошибок для корректного управления сбоями проверки.
4. Ведение журнала: регистрация попыток проверки и результатов для целей аудита и соблюдения требований.
5. Регулярные обновления сертификатов: обеспечьте обновление сертификатов до истечения срока их действия.

## Устранение распространенных проблем

### Недействительный сертификат
- Проверьте правильность пути к файлу сертификата.
- Убедитесь, что пароль сертификата правильный.
- Проверьте, не истек ли срок действия сертификата

### Подпись не найдена
- Подтвердите, что документ действительно содержит цифровые подписи
- Убедитесь, что вы проверяете нужные страницы.

### Ошибки проверки
- Проверьте, был ли документ изменен после подписания.
- Убедитесь, что сертификат подписчика находится в цепочке доверенных сертификатов.

## Заключение

GroupDocs.Signature для .NET — это мощное и гибкое решение для проверки цифровых подписей в документах. Следуя этому пошаговому руководству, вы сможете реализовать надежную проверку цифровых подписей в своих приложениях .NET, гарантируя подлинность и целостность документов.

Проверка цифровой подписи — важнейший компонент безопасного документооборота в современных бизнес-средах. GroupDocs.Signature позволяет уверенно реализовать эту функцию с минимальными усилиями, используя комплексный API для различных сценариев проверки.

## Часто задаваемые вопросы

### Может ли GroupDocs.Signature проверять подписи в PDF-документах, подписанных с помощью Adobe Acrobat?
Да, GroupDocs.Signature может проверять стандартные цифровые подписи в PDF-документах, созданных Adobe Acrobat и другим совместимым программным обеспечением для работы с PDF.

### Поддерживает ли GroupDocs.Signature проверку временных меток документов?
Да, API предоставляет возможность проверки временных меток документов в рамках процесса проверки цифровой подписи.

### Могу ли я проверить подписи на отдельных страницах многостраничного документа?
Да, вы можете настроить параметры проверки для проверки подписей на определенных страницах, а не во всем документе.

### Поддерживает ли GroupDocs.Signature проверку нескольких подписей в одном документе?
Да, GroupDocs.Signature может проверить несколько цифровых подписей в одном документе и предоставить подробные результаты для каждой подписи.

### Можно ли проверить подписи, созданные с помощью сертификатов разных центров сертификации?
Да, GroupDocs.Signature поддерживает проверку подписей, созданных с использованием сертификатов от разных центров сертификации, если они находятся в доверенной цепочке сертификатов.

### Связанные ресурсы
* [Справочник API GroupDocs.Signature](https://reference.groupdocs.com/signature/net/)
* [GroupDocs.Signature Загрузки](https://releases.groupdocs.com/signature/net/)
* [Примеры кода на GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Документация](https://docs.groupdocs.com/signature/net/)
* [Страница продукта](https://products.groupdocs.com/signature/net/)
* [Статьи блога](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Форум поддержки](https://forum.groupdocs.com/c/signature/13)
* [Временная лицензия](https://purchase.groupdocs.com/temporary-license/)