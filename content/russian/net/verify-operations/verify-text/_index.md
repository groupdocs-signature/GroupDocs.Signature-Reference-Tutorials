---
"description": "Освойте проверку текстовой подписи в приложениях .NET с помощью GroupDocs.Signature. Пошаговое руководство по внедрению с подробными примерами кода и рекомендациями."
"linktitle": "Проверить текст"
"second_title": "GroupDocs.Signature .NET API"
"title": "Проверка текстовых подписей в документах"
"url": "/ru/net/verify-operations/verify-text/"
"weight": 13
---

## Введение

Текстовые подписи, хотя они зачастую проще цифровых или электронных, играют важнейшую роль в управлении документами и их проверке. Будь то водяные знаки, текст нижнего колонтитула или определённые шаблоны контента, проверка наличия и целостности текстовых подписей является важным аспектом процесса проверки документов.

GroupDocs.Signature для .NET предоставляет мощный API для проверки текстовых подписей в документах самых разных форматов. Это подробное руководство поможет вам реализовать функцию проверки текста в ваших .NET-приложениях, гарантируя целостность и подлинность ваших документов.

## Предпосылки

Перед реализацией функции проверки текста убедитесь, что выполнены следующие предварительные условия:

1. GroupDocs.Signature для .NET: Загрузите и установите библиотеку с сайта [страница загрузки](https://releases.groupdocs.com/signature/net/).
2. Среда разработки .NET: Visual Studio или любая совместимая среда разработки .NET.
3. Базовые знания: знакомство с программированием на языке C# и концепциями .NET Framework.
4. Тестовый документ: документ, содержащий текстовые подписи для целей проверки.

## Импорт требуемых пространств имен

Начните с импорта необходимых пространств имен для доступа к функциональности GroupDocs.Signature:

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

Давайте разберем процесс проверки текста на понятные и выполнимые шаги:

## Шаг 1: Укажите путь к документу

```csharp
// Путь к документу, содержащему текстовые подписи
string filePath = "sample_multiple_signatures.docx";
```

Обязательно замените путь в примере на фактический путь к документу, содержащему текстовые подписи.

## Шаг 2: Инициализация объекта подписи

```csharp
// Создайте экземпляр класса Signature, передав путь к документу
using (Signature signature = new Signature(filePath))
{
    // Код подтверждения будет реализован здесь.
}
```

Класс Signature является основной точкой входа для всех операций в API GroupDocs.Signature.

## Шаг 3: Настройте параметры проверки текста

```csharp
// Определить параметры проверки текста
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = true,                               // Проверьте все страницы документа
    SignatureImplementation = TextSignatureImplementation.Native,
    Text = "signature",                            // Текст для проверки
    MatchType = TextMatchType.Contains             // Укажите критерии соответствия
};
```

Параметры проверки позволяют вам определить конкретные критерии для процесса проверки:
- `AllPages`: Установите значение true, чтобы проверить все страницы документа.
- `SignatureImplementation`: Укажите, как будет реализован текст (нативный или стикер)
- `Text`: Текстовое содержимое, которое должно соответствовать документу.
- `MatchType`: Метод сопоставления текста (Содержит, Точно, Начинается с и т. д.)

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
    Console.WriteLine($"Document {filePath} contains valid text signatures!");
    
    // Отображать информацию об успешных подписях
    foreach (TextSignature textSignature in result.Succeeded)
    {
        Console.WriteLine($"\nFound valid text signature:");
        Console.WriteLine($"Text: {textSignature.Text}");
        Console.WriteLine($"Location: Page {textSignature.PageNumber}, {textSignature.Left}x{textSignature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

Этот код проверяет, была ли проверка успешной, и предоставляет подробную информацию о проверенных текстовых подписях.

## Полный пример

Вот полный рабочий пример, демонстрирующий проверку текстовой подписи:

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
                    TextVerifyOptions options = new TextVerifyOptions()
                    {
                        AllPages = true,
                        SignatureImplementation = TextSignatureImplementation.Native,
                        Text = "signature",
                        MatchType = TextMatchType.Contains
                    };
                    
                    // Проверка подписей документов
                    VerificationResult result = signature.Verify(options);
                    
                    // Результаты проверки процесса
                    if(result.IsValid)
                    {
                        Console.WriteLine($"\nDocument {filePath} was verified successfully!");
                        foreach (TextSignature item in result.Succeeded)
                        {
                            Console.WriteLine($"\nValid signature is found with text: {item.Text}");
                            Console.WriteLine($"Location: Page {item.PageNumber}, position {item.Left}x{item.Top}");
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

### Использование регулярных выражений для проверки

Для более гибкого сопоставления с шаблонами вы можете использовать регулярные выражения:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    Text = "Invoice\\s+#\\d{5,6}",  // Сопоставьте шаблоны, например «Счет № 12345».
    MatchType = TextMatchType.Regex
};
```

### Проверка текста в определенных областях документа

Вы можете ограничить проверку определенными областями документа:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = false,
    PageNumber = 1,  // Подтвердить только на первой странице
    
    // Определить область поиска (координаты в точках)
    PagesSetup = new PagesSetup() 
    { 
        FirstPage = true,
        LastPage = false,
        OddPages = false,
        EvenPages = false 
    },
    
    // Площадь прямоугольника в миллиметрах
    Rectangle = new Rectangle(10, 10, 100, 30),
    
    Text = "Confidential"
};
```

### Одновременная проверка нескольких текстовых шаблонов

Вы можете создать несколько вариантов проверки для проверки различных текстовых шаблонов:

```csharp
// Создайте список вариантов проверки
List<VerifyOptions> listOptions = new List<VerifyOptions>();

// Добавить первое текстовое подтверждение
listOptions.Add(new TextVerifyOptions()
{
    Text = "Confidential",
    MatchType = TextMatchType.Exact
});

// Добавить второе текстовое подтверждение
listOptions.Add(new TextVerifyOptions()
{
    Text = "Do not copy",
    MatchType = TextMatchType.Contains
});

// Подтвердите с помощью нескольких вариантов
VerificationResult result = signature.Verify(listOptions);
```

### Проверка текста с определенным внешним видом

Вы также можете проверить текст с определенными характеристиками форматирования:

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    Text = "APPROVED",
    MatchType = TextMatchType.Exact,
    
    // Проверить конкретные свойства внешнего вида
    ForegroundColorRGB = System.Drawing.Color.Green,
    Font = new SignatureFont() { FontFamily = "Arial", FontSize = 12, Bold = true }
};
```

## Лучшие практики проверки текста

1. Выберите подходящие типы соответствия: выберите правильный тип соответствия (Содержит, Точное, Регулярное выражение) в зависимости от ваших требований к проверке.
2. Оптимизация производительности: для больших документов рассмотрите возможность проверки отдельных страниц, а не всего документа.
3. Обработка ошибок: реализуйте правильную обработку ошибок для корректного управления непредвиденными ситуациями.
4. Учитывайте чувствительность к регистру: при сопоставлении текста, особенно при критических проверках, учитывайте регистр.
5. Тщательное тестирование: протестируйте проверку с различными форматами документов и текстовыми шаблонами, чтобы убедиться в совместимости.

## Устранение распространенных проблем

### Текст не обнаружен
- Проверьте, влияет ли форматирование или кодировка текста на обнаружение.
- Убедитесь, что текст действительно присутствует в документе как обычный текст (а не изображение)
- Попробуйте использовать другие критерии соответствия (содержит вместо «Точное»).

### Проблемы с производительностью
- Оптимизируйте проверку, нацелившись на определенные страницы или области
- Используйте более конкретные текстовые шаблоны, чтобы уменьшить количество ложных срабатываний.

### Ошибки проверки
- Проверьте, влияют ли пробелы, специальные символы или форматирование на совпадение.
- Убедитесь, что текст не является частью отсканированного изображения (для чего требуется OCR)
- Убедитесь, что документ не был изменен с момента добавления текста.

## Заключение

Проверка текста — это универсальный и практичный подход к аутентификации документов, который можно использовать как самостоятельно, так и в сочетании с другими методами проверки. GroupDocs.Signature для .NET предоставляет комплексный и простой в использовании API для реализации надежной функции проверки текста в ваших приложениях .NET.

Следуя этому пошаговому руководству, вы узнали, как:
- Настройте и инициализируйте процесс проверки текста
- Укажите различные критерии проверки
- Обработка и интерпретация результатов проверки
- Реализуйте расширенные сценарии проверки

Эти возможности позволяют создавать безопасные и надежные системы обработки документов, способные проверять подлинность текста в документах различных форматов.

## Часто задаваемые вопросы

### Может ли GroupDocs.Signature проверять текст в отсканированных документах?
GroupDocs.Signature в первую очередь предназначен для цифровой проверки текста. Для отсканированных документов необходимо сначала использовать технологию OCR (оптического распознавания символов), чтобы преобразовать отсканированные изображения в текст.

### Какие форматы документов поддерживаются для проверки текста?
GroupDocs.Signature поддерживает широкий спектр форматов документов, включая PDF, документы Word (DOC, DOCX), электронные таблицы Excel (XLS, XLSX), презентации PowerPoint (PPT, PPTX), изображения и многое другое.

### Могу ли я проверить форматированный текст (жирный, курсив, определенные шрифты)?
Да, GroupDocs.Signature предоставляет возможности проверки текста с определенными характеристиками форматирования, включая семейство шрифтов, размер, стиль (жирный, курсив) и цвет.

### Можно ли проверить текст в документах, защищенных паролем?
Да, GroupDocs.Signature предоставляет возможность указывать пароли документов при открытии защищенных документов для проверки.

### Могу ли я проверить водяные знаки и фоновый текст?
Да, GroupDocs.Signature может проверять различные типы текстовых подписей, включая водяные знаки и фоновый текст, в зависимости от того, как они были реализованы в документе.

### Связанные ресурсы
* [Справочник API GroupDocs.Signature](https://reference.groupdocs.com/signature/net/)
* [GroupDocs.Signature Загрузки](https://releases.groupdocs.com/signature/net/)
* [Примеры кода на GitHub](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [Документация](https://docs.groupdocs.com/signature/net/)
* [Страница продукта](https://products.groupdocs.com/signature/net/)
* [Статьи блога](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [Форум поддержки](https://forum.groupdocs.com/c/signature/13)
* [Временная лицензия](https://purchase.groupdocs.com/temporary-license/)