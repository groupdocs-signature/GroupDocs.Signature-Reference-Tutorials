---
"description": "了解如何使用 GroupDocs.Signature for .NET 在文件中搜尋和提取表單欄位簽章。本指南包含程式碼範例，可實現無縫整合。"
"linktitle": "搜尋表單字段"
"second_title": "GroupDocs.簽署 .NET API"
"title": "在文件中搜尋表單字段"
"url": "/zh-hant/net/signature-searching/search-for-form-fields/"
"weight": 12
type: docs
---
## 介紹

在現代文件管理系統中，表單欄位在資料收集、使用者互動和文件自動化中發揮著至關重要的作用。 GroupDocs.Signature for .NET 為開發人員提供了一套強大的工具，用於處理各種文件格式的表單字段，包括以程式設計方式搜尋、檢索和處理這些元素。

本綜合指南將引導您完成使用 GroupDocs.Signature for .NET 在文件中搜尋表單欄位簽章的流程，提供清晰的解釋、實用的程式碼範例和最佳實務。

## 先決條件

在深入使用 GroupDocs.Signature for .NET 搜尋表單欄位之前，請確保您已滿足以下先決條件：

1. 開發環境：使用 Visual Studio 或您喜歡的 IDE 設定 .NET 開發環境。

2. GroupDocs.Signature for .NET：從下列位置下載並安裝 GroupDocs.Signature for .NET 函式庫 [這裡](https://releases。groupdocs.com/signature/net/).

3. 文件存取：熟悉以下網址提供的綜合文檔 [GroupDocs.Signature for .NET 文檔](https://docs。groupdocs.com/signature/net/).

4. 基礎知識：了解 C# 程式設計和 .NET 框架基礎將會有所幫助。

## 導入命名空間

首先匯入必要的命名空間來存取 GroupDocs.Signature 的功能：

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

現在讓我們將在文件中搜尋表單欄位的過程分解為清晰、可操作的步驟：

## 步驟 1：定義文檔路徑

首先，指定包含要搜尋的表單欄位的文件的路徑：

```csharp
string filePath = "sample_signed_formfield.pdf";
```

## 步驟2：初始化簽名對象

建立一個實例 `Signature` 透過將檔案路徑傳遞給建構函數來建立類別：

```csharp
using (Signature signature = new Signature(filePath))
{
    // 表單欄位搜尋代碼將在此處新增
}
```

## 步驟 3：搜尋表單欄位簽名

使用 `Search` 具有適當簽名類型的方法來尋找文件中的表單欄位：

```csharp
// 在文件中搜尋表單欄位簽名
List<FormFieldSignature> formFields = signature.Search<FormFieldSignature>(SignatureType.FormField);
```

## 步驟4：處理並顯示結果

遍歷找到的表單欄位並存取其屬性：

```csharp
// 顯示有關找到的表單欄位的信息
Console.WriteLine($"\nDocument '{filePath}' contains {formFields.Count} form field signature(s):");

foreach (var formField in formFields)
{
    Console.WriteLine($"Form Field Name: {formField.Name}");
    Console.WriteLine($"Form Field Type: {formField.Type}");
    Console.WriteLine($"Form Field Value: {formField.Value}");
    Console.WriteLine($"Form Field Page: {formField.PageNumber}");
    Console.WriteLine();
}
```

## 完整範例

這是一個完整的、可運行的範例，示範如何在文件中搜尋表單欄位：

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace FormFieldSearchExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // 文件路徑 - 使用您的文件路徑更新
            string filePath = "sample_signed_formfield.pdf";

            // 初始化簽名實例
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // 搜尋表單欄位簽名
                    List<FormFieldSignature> formFields = signature.Search<FormFieldSignature>(SignatureType.FormField);

                    // 顯示結果
                    Console.WriteLine($"\nDocument '{filePath}' contains {formFields.Count} form field signature(s):");

                    foreach (var formField in formFields)
                    {
                        Console.WriteLine($"Form Field Name: {formField.Name}");
                        Console.WriteLine($"Form Field Type: {formField.Type}");
                        Console.WriteLine($"Form Field Value: {formField.Value}");
                        Console.WriteLine($"Form Field Page: {formField.PageNumber}");
                        Console.WriteLine();
                    }
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"Error occurred: {ex.Message}");
                }
            }

            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## 進階表單欄位搜尋技術

### 使用特定表單欄位選項進行搜尋

如需更有針對性的搜索，您可以使用 `FormFieldSearchOptions` 自訂您的搜尋條件：

```csharp
// 建立表單欄位搜尋選項
FormFieldSearchOptions options = new FormFieldSearchOptions
{
    // 在特定頁面中搜尋
    AllPages = false,
    PageNumber = 1,
    
    // 按欄位名稱過濾
    Name = "Signature",
    
    // 按字段類型過濾
    Type = FormFieldType.TextFormField
};

// 使用特定選項進行搜尋
List<FormFieldSignature> specificFormFields = signature.Search<FormFieldSignature>(options);
```

### 使用不同類型的表單字段

GroupDocs.Signature 支援各種表單欄位類型，每種類型都有特定的屬性：

```csharp
foreach (var formField in formFields)
{
    switch (formField.Type)
    {
        case FormFieldType.TextFormField:
            // 處理文字表單字段
            Console.WriteLine($"Text Field: {formField.Name}, Value: {formField.Value}");
            break;
            
        case FormFieldType.CheckboxFormField:
            // 處理複選框字段
            bool isChecked = Convert.ToBoolean(formField.Value);
            Console.WriteLine($"Checkbox: {formField.Name}, Checked: {isChecked}");
            break;
            
        case FormFieldType.ComboboxFormField:
            // 處理組合框字段
            Console.WriteLine($"Combobox: {formField.Name}, Selected Value: {formField.Value}");
            break;
            
        case FormFieldType.DigitalFormField:
            // 處理數位簽名字段
            Console.WriteLine($"Digital Signature Field: {formField.Name}");
            break;
            
        case FormFieldType.RadioButtonFormField:
            // 處理單選按鈕字段
            Console.WriteLine($"Radio Button: {formField.Name}, Selected: {formField.Value}");
            break;
    }
}
```

### 提取表單欄位資料進行處理

您可以提取和處理表單欄位資料以供在應用程式中進一步使用：

```csharp
// 建立字典來儲存表單欄位值
Dictionary<string, object> formData = new Dictionary<string, object>();

// 提取表單欄位數據
foreach (var field in formFields)
{
    formData.Add(field.Name, field.Value);
}

// 處理收集的數據
ProcessFormData(formData);

// 範例處理方法
static void ProcessFormData(Dictionary<string, object> data)
{
    // 在這裡實作您的資料處理邏輯
    foreach (var item in data)
    {
        Console.WriteLine($"Processing field '{item.Key}' with value '{item.Value}'");
    }
}
```

## 結論

在本指南中，我們探討如何使用 GroupDocs.Signature for .NET 在文件中搜尋和處理表單欄位簽章。從基本搜尋到針對不同表單欄位類型的進階技巧，您現在掌握了在 .NET 應用程式中實作表單欄位功能的知識。

GroupDocs.Signature 提供了一個強大且靈活的框架來處理文件簽名，使您能夠建立強大的文件管理解決方案，高效、安全地處理表單欄位。

## 常見問題解答

### GroupDocs.Signature 可以搜尋受密碼保護的文件中的表單欄位嗎？

是的，GroupDocs.Signature 可以透過在初始化時提供密碼來搜尋受密碼保護的文件中的表單字段 `Signature` 目的：

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // 搜尋表單字段
}
```

### 哪些文檔格式支援表單欄位搜尋？

GroupDocs.Signature 支援各種文件格式的表單欄位搜索，包括 PDF、Microsoft Word（DOC、DOCX）、Excel（XLS、XLSX）、PowerPoint（PPT、PPTX）等。

### 搜尋表單欄位值後我可以修改它們嗎？

是的，搜尋表單欄位後，您可以修改它們的值並更新文件：

```csharp
// 搜尋表單字段
List<FormFieldSignature> fields = signature.Search<FormFieldSignature>(SignatureType.FormField);

// 修改欄位值
foreach (var field in fields)
{
    if (field.Name == "CustomerName")
    {
        field.Value = "John Doe";
    }
}

// 儲存更新後的文檔
signature.Save("updated_document.pdf");
```

### 如何搜尋具有特定值的表單欄位？

您可以使用自訂搜尋選項來搜尋具有特定值的表單欄位：

```csharp
// 建立搜尋選項
FormFieldSearchOptions options = new FormFieldSearchOptions
{
    // 使用委託按值進行過濾
    ProcessCompleted = (fieldSignature) =>
    {
        // 僅對具有特定值的欄位傳回 true
        return fieldSignature.Value != null && fieldSignature.Value.ToString().Contains("Approved");
    }
};

// 使用過濾器搜尋
List<FormFieldSignature> filteredFields = signature.Search<FormFieldSignature>(options);
```

### 我可以在一次操作中搜尋包括表單欄位在內的多種簽章類型嗎？

是的，您可以在一次操作中搜尋多種簽名類型：

```csharp
// 為不同的簽名類型建立搜尋選項
FormFieldSearchOptions formFieldOptions = new FormFieldSearchOptions();
DigitalSearchOptions digitalOptions = new DigitalSearchOptions();

// 建立搜尋選項列表
List<SearchOptions> searchOptions = new List<SearchOptions>
{
    formFieldOptions,
    digitalOptions
};

// 搜尋多種簽名類型
SearchResult result = signature.Search(searchOptions);

// 從結果中存取不同的簽名類型
foreach (var sig in result.Signatures)
{
    if (sig is FormFieldSignature formField)
    {
        Console.WriteLine($"Form Field: {formField.Name}");
    }
    else if (sig is DigitalSignature digitalSignature)
    {
        Console.WriteLine($"Digital Signature: {digitalSignature.Certificate?.SubjectName}");
    }
}
```

## 參見

* [API 參考](https://reference.groupdocs.com/signature/net/)
* [GitHub 上的程式碼範例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [文件](https://docs.groupdocs.com/signature/net/)
* [產品頁面](https://products.groupdocs.com/signature/net/)
* [下載最新版本](https://releases.groupdocs.com/signature/net/)
* [部落格文章](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [免費支援論壇](https://forum.groupdocs.com/c/signature/13)
* [臨時執照](https://purchase.groupdocs.com/temporary-license/)