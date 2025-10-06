---
"description": "了解如何使用 GroupDocs.Signature for .NET 高效更新各種文件格式的文字簽章。透過本教學全面掌握文件身份驗證。"
"linktitle": "更新文字"
"second_title": "GroupDocs.簽署 .NET API"
"title": "更新文件中的文字簽名"
"url": "/zh-hant/net/update-operations/update-text/"
"weight": 13
type: docs
---
## 介紹
GroupDocs.Signature for .NET 是一款全面的文件簽章解決方案，可讓開發人員將強大的簽章功能整合到他們的 .NET 應用程式中。借助這個功能強大的庫，您可以輕鬆添加、搜尋、驗證和更新各種文件格式的各種類型的簽名，包括文字簽名。本教學重點在於如何更新文件中的文字簽名，並為您提供無縫實施的逐步指導。

## 先決條件
在使用 GroupDocs.Signature for .NET 進行文字簽章更新之前，請確保您已符合以下先決條件：

1. Visual Studio：在您的系統上安裝最新版本的 Visual Studio IDE。
2. GroupDocs.Signature for .NET：從下載並安裝 GroupDocs.Signature for .NET 函式庫 [下載頁面](https://releases。groupdocs.com/signature/net/).
3. .NET Framework 或 .NET Core：請確定您的開發機器上安裝了 .NET Framework 或 .NET Core。
4. 基本 C# 知識：熟悉 C# 程式設計基礎。

## 導入命名空間
在開始更新文件中的文字簽名之前，您需要將必要的命名空間匯入專案。這些命名空間提供對 GroupDocs.Signature 類別和方法的存取。

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## 步驟 1：設定文檔路徑
首先，建立包含要更新的文字簽署的文件的路徑。

```csharp
string filePath = "sample_multiple_signatures.docx";
```

此行指定來源文檔的路徑。替換 `"sample_multiple_signatures.docx"` 使用您的文件的實際路徑。

## 第 2 步：複製文檔
自 `Update` 方法適用於同一文檔，因此建立原始文檔的備份副本是一種很好的做法。

```csharp
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "UpdateText", fileName);
File.Copy(filePath, outputFilePath, true);
```

此程式碼片段在指定目錄中建立原始文件的副本。替換 `"Your Document Directory"` 與您想要儲存更新文件的實際路徑。

## 步驟3：初始化簽名對象
現在，初始化 `Signature` 物件以及文件副本的路徑。

```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // 您的程式碼在這裡
}
```

這 `Signature` 類別是 GroupDocs.Signature 功能的主要入口點。 `using` 語句確保資源在使用後得到適當處置。

## 步驟 4：搜尋文字簽名
在更新文字簽名之前，您需要在文件中找到它。

```csharp
TextSearchOptions options = new TextSearchOptions();
List<TextSignature> signatures = signature.Search<TextSignature>(options);
```

此代碼使用預設搜尋選項搜尋文件中的所有文字簽名。您可以透過配置以下屬性來自訂搜尋： `TextSearchOptions` 班級。

## 步驟5：更新文字簽名
找到文字簽名後，您可以選擇一個並更新其屬性。

```csharp
if (signatures.Count > 0)
{
    TextSignature textSignature = signatures[0];
    textSignature.Text = "John Walkman";
    textSignature.Left = textSignature.Left + 10;
    textSignature.Top = textSignature.Top + 10;
    textSignature.Width = 200;
    textSignature.Height = 100;
    bool result = signature.Update(textSignature);
    if (result)
    {
        Console.WriteLine($"Signature with Text '{textSignature.Text}' was updated in the document ['{fileName}'].");
    }
    else
    {
        Console.WriteLine($"Signature was not updated in the document! Signature with Text '{textSignature.Text}' was not found!");
    }
}
```

此代碼：
1. 檢查是否找到任何文字簽名
2. 從清單中取得第一個簽名
3. 修改其文字內容、位置（左、上）和大小（寬度、高度）
4. 呼叫 `Update` 應用更改的方法
5. 根據結果顯示成功或失敗的訊息

## 完整範例
下面是一個完整的範例，示範如何更新文件中的文字簽名：

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace UpdateTextSignature
{
    class Program
    {
        static void Main(string[] args)
        {
            // 文件路徑
            string filePath = "sample_multiple_signatures.docx";
            
            // 影印文件
            string fileName = Path.GetFileName(filePath);
            string outputFilePath = Path.Combine("OutputDirectory", "UpdateText", fileName);
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
            File.Copy(filePath, outputFilePath, true);
            
            // 初始化簽名對象
            using (Signature signature = new Signature(outputFilePath))
            {
                // 搜尋文字簽名
                TextSearchOptions options = new TextSearchOptions();
                List<TextSignature> signatures = signature.Search<TextSignature>(options);
                
                // 更新文字簽名
                if (signatures.Count > 0)
                {
                    TextSignature textSignature = signatures[0];
                    textSignature.Text = "John Walkman";
                    textSignature.Left = textSignature.Left + 10;
                    textSignature.Top = textSignature.Top + 10;
                    textSignature.Width = 200;
                    textSignature.Height = 100;
                    
                    // 應用程式變更
                    bool result = signature.Update(textSignature);
                    
                    // 檢查結果
                    if (result)
                    {
                        Console.WriteLine($"Signature with Text '{textSignature.Text}' was updated in the document ['{fileName}'].");
                    }
                    else
                    {
                        Console.WriteLine($"Signature was not updated in the document! Signature with Text '{textSignature.Text}' was not found!");
                    }
                }
                else
                {
                    Console.WriteLine("No text signatures found in the document.");
                }
            }
        }
    }
}
```

## 高級文字簽名定制
GroupDocs.Signature 為文字簽名提供了豐富的自訂選項。您可以修改各種屬性，例如：

- 字體：更改字體系列、大小、樣式和顏色
- 邊框：新增或修改邊框樣式和顏色
- 背景：設定背景顏色或透明度
- 旋轉：將文字簽名旋轉到特定角度
- 透明度：調整簽名的不透明度

以下是如何自訂字體屬性的範例：

```csharp
textSignature.ForeColor = System.Drawing.Color.Blue;
textSignature.Font.FontFamily = "Arial";
textSignature.Font.FontSize = 16;
textSignature.Font.Bold = true;
textSignature.Font.Italic = true;
textSignature.Font.Underline = true;
```

## 結論
GroupDocs.Signature for .NET 提供了一個強大且靈活的解決方案，以程式設計方式更新文件中的文字簽章。透過遵循本教學中概述的步驟，開發人員可以有效地將文字簽章更新功能整合到他們的 .NET 應用程式中，從而增強文件管理和驗證流程。

GroupDocs.Signature 擁有全面的功能和使用者友好的 API，使開發人員能夠建立滿足現代商業應用程式要求的複雜文件簽章解決方案。

## 常見問題解答
### 我可以在單一文件中更新多個文字簽名嗎？
是的，您可以透過遍歷找到的簽名清單並對每個簽名單獨套用必要的變更來更新多個文字簽名。

### GroupDocs.Signature 除了文字之外還支援其他類型的簽章嗎？
當然！ GroupDocs.Signature 支援多種類型的簽名，包括圖像簽名、數位簽名、條碼簽名、二維碼簽名和印章簽名。每種類型都有各自的屬性和方法，用於建立、搜尋和更新。

### GroupDocs.Signature for .NET 有試用版嗎？
是的，您可以從下載免費試用版 [這裡](https://releases.groupdocs.com/) 在購買之前評估圖書館的功能。

### 我可以自訂文字簽名的外觀嗎？
是的，GroupDocs.Signature 為文字簽名提供了廣泛的自訂選項，包括字體屬性（系列、大小、樣式）、顏色、邊框、背景、旋轉和透明度。

### GroupDocs.Signature for .NET 是否適用於所有文件格式？
GroupDocs.Signature 支援多種文件格式，包括 PDF、Microsoft Office 格式（Word、Excel、PowerPoint）、OpenDocument 格式、圖片等。完整清單請參閱 [文件](https://docs。groupdocs.com/signature/net/).

### 如何獲得 GroupDocs.Signature 的技術支援？
您可以透過以下管道獲得技術支援：
- [論壇](https://forum.groupdocs.com/c/signature/13)
- [文件](https://docs.groupdocs.com/signature/net/)
- [API 參考](https://reference.groupdocs.com/signature/net/)
- [GitHub 上的範例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [部落格](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)