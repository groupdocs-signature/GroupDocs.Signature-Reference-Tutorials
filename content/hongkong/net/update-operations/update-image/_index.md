---
"description": "了解如何使用 GroupDocs.Signature for .NET 高效更新多種文件格式的映像簽章。這是一份全面的指南，旨在幫助開發人員增強文件安全性和視覺完整性。"
"linktitle": "更新影像"
"second_title": "GroupDocs.簽署 .NET API"
"title": "更新文件中的影像簽名"
"url": "/zh-hant/net/update-operations/update-image/"
"weight": 11
type: docs
---
## 介紹
數位文件管理需要強大的簽章功能來確保其真實性和完整性。影像簽名在這個生態系統中發揮著至關重要的作用，它為文件提供視覺驗證和品牌元素。 GroupDocs.Signature for .NET 為開發人員提供了一個強大的框架，使他們能夠在 .NET 應用程式中實現全面的簽名功能，包括更新現有映像簽名的功能。

本教學特別關注如何更新文件中的圖像簽名，提供該過程的詳細演練並展示 GroupDocs.Signature for .NET 的功能。

## 先決條件
在使用 GroupDocs.Signature for .NET 實作映像簽章更新之前，請確保您已符合以下先決條件：

### 1. 安裝 GroupDocs.Signature for .NET
從下載並安裝最新版本的 GroupDocs.Signature for .NET [下載頁面](https://releases.groupdocs.com/signature/net/)。您可以使用 NuGet 套件管理器或直接引用 DLL 檔案將庫新增至您的專案。

### 2. 取得許可證
雖然 GroupDocs.Signature for .NET 可以與臨時許可證一起使用以進行評估，但建議在生產環境中使用有效許可證。您可以獲取 [臨時執照](https://purchase.groupdocs.com/temporary-license/) 用於測試或購買用於生產用途的完整許可證。

### 3. 開發環境設定
確保您已設定相容的 .NET 開發環境：
- Visual Studio 2017 或更高版本
- .NET Framework 4.6.2 或更高版本，或 .NET Standard 2.0 相容實現
- 對 C# 程式語言有基本的了解

## 導入命名空間
首先匯入存取 GroupDocs.Signature 功能所需的命名空間：

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## 更新影像簽名的逐步指南
讓我們將更新文件中的映像簽名的過程分解為可管理的步驟：

## 步驟 1：指定文檔路徑
首先，定義包含要更新的影像簽署的文件的路徑：

```csharp
string filePath = "sample_multiple_signatures.docx";
```

確保指定的文件存在並且至少包含一個影像簽名。

## 第 2 步：定義輸出路徑
為更新後的文件建立一個路徑。由於 `Update` 方法適用於同一文檔，最好建立一份副本來保留原始文檔：

```csharp
string fileName = Path.GetFileName(filePath);
string outputDirectory = Path.Combine("Your Document Directory", "UpdateImage");
string outputFilePath = Path.Combine(outputDirectory, fileName);

// 確保輸出目錄存在
Directory.CreateDirectory(outputDirectory);
```

## 步驟3：複製來源文件
為更新操作建立原始文件的副本：

```csharp
File.Copy(filePath, outputFilePath, true);
```

## 步驟4：初始化簽名對象
建立一個實例 `Signature` 類別使用輸出檔案路徑：

```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // 附加代碼將放在此處
}
```

## 步驟 5：設定影像簽名的搜尋選項
設定選項以搜尋文件中現有的影像簽名：

```csharp
ImageSearchOptions options = new ImageSearchOptions();
// 如果需要，您可以在此處自訂搜尋選項
// 例如：options.AllPages = true; 在所有頁面中搜尋
```

## 步驟 6：搜尋圖片簽名
使用配置的搜尋選項在文件中尋找影像簽名：

```csharp
List<ImageSignature> signatures = signature.Search<ImageSignature>(options);
```

## 步驟 7：更新影像簽名屬性
檢查是否找到簽名並根據需要更新其屬性：

```csharp
if (signatures.Count > 0)
{
    ImageSignature imageSignature = signatures[0];
    
    // 更新位置
    imageSignature.Left = 200;
    imageSignature.Top = 250;
    
    // 更新大小
    imageSignature.Width = 200;
    imageSignature.Height = 200;
    
    // 您也可以更新其他屬性，例如不透明度
    // 影像簽名.不透明度 = 0.8;
    
    // 應用程式變更
    bool result = signature.Update(imageSignature);
    
    // 檢查結果
    if (result)
    {
        Console.WriteLine($"Image signature at location {imageSignature.Left}x{imageSignature.Top} and Size {imageSignature.Width}x{imageSignature.Height} was updated in the document ['{fileName}'].");
    }
    else
    {
        Console.WriteLine($"Signature was not updated in the document! Signature at location {imageSignature.Left}x{imageSignature.Top} and Size {imageSignature.Width}x{imageSignature.Height} was not found!");
    }
}
else
{
    Console.WriteLine("No image signatures found in the document.");
}
```

## 完整範例
這是一個完整的、可執行的範例，示範如何更新文件中的影像簽名：

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace UpdateImageSignatureExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // 文件路徑
            string filePath = "sample_multiple_signatures.docx";
            
            // 定義輸出路徑
            string fileName = Path.GetFileName(filePath);
            string outputDirectory = Path.Combine(Environment.CurrentDirectory, "UpdateImage");
            string outputFilePath = Path.Combine(outputDirectory, fileName);
            
            // 確保輸出目錄存在
            Directory.CreateDirectory(outputDirectory);
            
            // 建立原始文件的副本
            File.Copy(filePath, outputFilePath, true);
            
            // 初始化簽名實例
            using (Signature signature = new Signature(outputFilePath))
            {
                // 配置搜尋選項
                ImageSearchOptions options = new ImageSearchOptions();
                
                // 搜尋圖片簽名
                List<ImageSignature> signatures = signature.Search<ImageSignature>(options);
                
                // 檢查是否找到簽名
                if (signatures.Count > 0)
                {
                    // 取得第一個簽名
                    ImageSignature imageSignature = signatures[0];
                    
                    // 更新位置和大小
                    imageSignature.Left = 200;
                    imageSignature.Top = 250;
                    imageSignature.Width = 200;
                    imageSignature.Height = 200;
                    
                    // 應用程式更新
                    bool result = signature.Update(imageSignature);
                    
                    // 檢查結果
                    if (result)
                    {
                        Console.WriteLine($"Image signature was successfully updated in document '{fileName}'.");
                        Console.WriteLine($"New position: {imageSignature.Left}x{imageSignature.Top}");
                        Console.WriteLine($"New size: {imageSignature.Width}x{imageSignature.Height}");
                        Console.WriteLine($"Output file path: {outputFilePath}");
                    }
                    else
                    {
                        Console.WriteLine("Failed to update image signature!");
                    }
                }
                else
                {
                    Console.WriteLine("No image signatures found in the document.");
                }
            }
            
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## 高級圖像簽名定制
GroupDocs.Signature 除了基本位置和大小屬性之外，還提供了自訂影像簽章的其他選項：

### 調整不透明度
控制影像簽名的透明度：

```csharp
imageSignature.Opacity = 0.7; // 70% 不透明度
```

### 旋轉影像
將影像簽名旋轉到特定角度：

```csharp
imageSignature.Angle = 45; // 旋轉45度
```

### 新增邊框
使用自訂邊框增強影像簽名：

```csharp
imageSignature.Border.Color = System.Drawing.Color.Red;
imageSignature.Border.DashStyle = System.Drawing.Drawing2D.DashStyle.Dash;
imageSignature.Border.Weight = 2;
imageSignature.Border.Visible = true;
```

## 結論
GroupDocs.Signature for .NET 提供了一個強大且靈活的解決方案，用於更新文件中的映像簽章。按照本教學中概述的步驟，開發人員可以在其 .NET 應用程式中有效地實現映像簽章更新功能，從而增強文件管理功能。

GroupDocs.Signature 憑藉其全面的功能集，使開發人員能夠建立複雜的文件簽章解決方案，滿足現代商業應用程式的要求，同時確保文件的完整性和安全性。

## 常見問題解答
### 我可以在單一文件中更新多個影像簽名嗎？
是的，GroupDocs.Signature 允許您更新文件中的多個影像簽名。搜尋簽名後，您可以遍歷結果清單並單獨更新每個簽名。

### GroupDocs.Signature 是否支援各種文件格式？
當然！ GroupDocs.Signature 支援多種文件格式，包括 PDF、Microsoft Office 文件（Word、Excel、PowerPoint）、OpenDocument 格式和影像格式。

### GroupDocs.Signature for .NET 有試用版嗎？
是的，您可以從 [GroupDocs 網站](https://releases.groupdocs.com/) 在購買之前評估圖書館的能力。

### 我可以替換現有影像簽名中的影像嗎？
雖然 Update 方法可讓您修改現有簽名的屬性，但取代實際圖片內容需要刪除舊簽名並新增簽名。 GroupDocs.Signature 提供了這兩種操作的方法。

### 在哪裡可以找到對 GroupDocs.Signature for .NET 的額外支援？
您可以透過以下資源獲得全面的支援：
- [API 文件](https://docs.groupdocs.com/signature/net/)
- [API 參考](https://reference.groupdocs.com/signature/net/)
- [GitHub 範例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [支援論壇](https://forum.groupdocs.com/c/signature/13)
- [部落格](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)