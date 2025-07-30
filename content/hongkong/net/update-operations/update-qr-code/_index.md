---
"description": "了解如何使用 GroupDocs.Signature for .NET 動態更新各種文件格式的二維碼簽章。現代文件管理解決方案的綜合開發人員指南。"
"linktitle": "更新二維碼"
"second_title": "GroupDocs.簽署 .NET API"
"title": "更新文檔中的二維碼簽名"
"url": "/zh-hant/net/update-operations/update-qr-code/"
"weight": 12
---

## 介紹
在當今數位優先的商業環境中，二維碼已成為文件管理和身份驗證系統中不可或缺的元素。它們提供了一種便捷的資訊編碼和存取方式，涵蓋從簡單的 URL 到複雜的結構化資料。 GroupDocs.Signature for .NET 提供了一個全面的工具包，使開發人員能夠將高級電子簽名功能整合到他們的應用程式中，包括更新文件中現有二維碼簽名的功能。

本教學重點在於如何使用 GroupDocs.Signature for .NET 更新文件中的二維碼簽章。無論您需要修改現有二維碼的位置、大小或編碼數據，本指南都將透過清晰的程式碼範例和說明逐步引導您完成整個過程。

## 先決條件
在使用 GroupDocs.Signature for .NET 進行二維碼簽章更新之前，請確保您已符合以下先決條件：

1. 開發環境：可用的 .NET 開發環境，例如 Visual Studio 2017 或更高版本。
2. GroupDocs.Signature 函式庫：從下載並安裝 GroupDocs.Signature for .NET 函式庫 [下載頁面](https://releases。groupdocs.com/signature/net/).
3. 許可證（可選）：對於生產用途，您需要有效的許可證。出於測試目的，您可以使用 [臨時執照](https://purchase。groupdocs.com/temporary-license/).
4. 範例文件：包含您希望更新的二維碼簽名的文件。
5. 基本 C# 知識：熟悉 C# 程式設計概念。

## 導入命名空間
首先匯入必要的命名空間以存取 GroupDocs.Signature 功能：

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

讓我們將更新二維碼簽名的過程分解為清晰、易於管理的步驟：

## 步驟 1：設定文檔路徑
首先，定義來源文件的路徑以及更新文件的儲存位置：

```csharp
// 帶有二維碼簽名的來源文檔路徑
string filePath = "sample_multiple_signatures.docx";

// 取得輸出的檔名
string fileName = Path.GetFileName(filePath);

// 定義輸出目錄和檔案路徑
string outputDirectory = Path.Combine("Your Document Directory", "UpdateQRCode");
string outputFilePath = Path.Combine(outputDirectory, fileName);

// 確保輸出目錄存在
Directory.CreateDirectory(outputDirectory);
```

## 第 2 步：複製來源文檔
由於更新操作直接修改文檔，因此建立原始文檔的副本以保存它：

```csharp
// 建立原始文件的副本
File.Copy(filePath, outputFilePath, true);
```

## 步驟3：初始化簽名實例
建立一個實例 `Signature` 與文件一起工作的類別：

```csharp
// 使用輸出檔案路徑初始化簽章實例
using (Signature signature = new Signature(outputFilePath))
{
    // 簽名操作將在這裡執行
}
```

## 步驟4：設定二維碼搜尋選項
設定搜尋選項以尋找文件中現有的二維碼簽名：

```csharp
// 配置二維碼簽名的搜尋選項
QrCodeSearchOptions options = new QrCodeSearchOptions();

// 如果需要，您可以自訂搜尋選項
// options.AllPages = true; // 在所有頁面上搜尋
// options.PageNumber = 1; // 在特定頁面上搜尋
// options.EncodeType = QrCodeTypes.QR; // 搜尋特定的二維碼類型
```

## 步驟5：搜尋二維碼簽名
使用配置的搜尋選項在文件中尋找二維碼簽名：

```csharp
// 搜尋二維碼簽名
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```

## 步驟6：更新二維碼簽章屬性
如果找到二維碼簽名，則根據需要更新其屬性：

```csharp
// 檢查是否找到簽名
if (signatures.Count > 0)
{
    // 取得第一個二維碼簽名
    QrCodeSignature qrCodeSignature = signatures[0];
    
    // 更新位置
    qrCodeSignature.Left = 200;
    qrCodeSignature.Top = 250;
    
    // 更新大小
    qrCodeSignature.Width = 200;
    qrCodeSignature.Height = 200;
    
    // 您也可以根據需要更新二維碼數據
    // qrCodeSignature.Text = "已更新二維碼資料";
    
    // 應用程式更新
    bool result = signature.Update(qrCodeSignature);
    
    // 檢查結果
    if (result)
    {
        Console.WriteLine($"QR Code signature was successfully updated in the document '{fileName}'.");
        Console.WriteLine($"New position: {qrCodeSignature.Left}x{qrCodeSignature.Top}");
        Console.WriteLine($"New size: {qrCodeSignature.Width}x{qrCodeSignature.Height}");
    }
    else
    {
        Console.WriteLine($"Failed to update QR Code signature in the document!");
    }
}
else
{
    Console.WriteLine("No QR Code signatures found in the document.");
}
```

## 完整範例
這是一個完整的、實用的範例，示範如何更新文件中的二維碼簽章：

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace UpdateQRCodeSignatureExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // 文件路徑
            string filePath = "sample_multiple_signatures.docx";
            
            // 定義輸出路徑
            string fileName = Path.GetFileName(filePath);
            string outputDirectory = Path.Combine(Environment.CurrentDirectory, "UpdateQRCode");
            string outputFilePath = Path.Combine(outputDirectory, fileName);
            
            // 確保輸出目錄存在
            Directory.CreateDirectory(outputDirectory);
            
            // 建立原始文件的副本
            File.Copy(filePath, outputFilePath, true);
            
            // 初始化簽名實例
            using (Signature signature = new Signature(outputFilePath))
            {
                // 配置搜尋選項
                QrCodeSearchOptions options = new QrCodeSearchOptions();
                
                // 搜尋二維碼簽名
                List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
                
                // 檢查是否找到簽名
                if (signatures.Count > 0)
                {
                    // 取得第一個簽名
                    QrCodeSignature qrCodeSignature = signatures[0];
                    
                    // 更新位置和大小
                    qrCodeSignature.Left = 200;
                    qrCodeSignature.Top = 250;
                    qrCodeSignature.Width = 200;
                    qrCodeSignature.Height = 200;
                    
                    // 應用程式更新
                    bool result = signature.Update(qrCodeSignature);
                    
                    // 檢查結果
                    if (result)
                    {
                        Console.WriteLine($"QR Code signature was successfully updated in document '{fileName}'.");
                        Console.WriteLine($"New position: {qrCodeSignature.Left}x{qrCodeSignature.Top}");
                        Console.WriteLine($"New size: {qrCodeSignature.Width}x{qrCodeSignature.Height}");
                        Console.WriteLine($"Output file path: {outputFilePath}");
                    }
                    else
                    {
                        Console.WriteLine("Failed to update QR Code signature!");
                    }
                }
                else
                {
                    Console.WriteLine("No QR Code signatures found in the document.");
                }
            }
            
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## 高級二維碼簽名定制
GroupDocs.Signature 提供了基本位置和大小之外的自訂二維碼簽章的附加選項：

### 更新編碼數據
您可以更新二維碼中編碼的實際資料：

```csharp
// 更新編碼數據
qrCodeSignature.Text = "https://www.updated-website.com」；
```

### 調整外觀屬性
自訂二維碼的視覺效果：

```csharp
// 設定前景色（二維碼顏色）
qrCodeSignature.ForeColor = System.Drawing.Color.Blue;

// 設定背景顏色
qrCodeSignature.BackgroundColor = System.Drawing.Color.LightYellow;

// 調整透明度
qrCodeSignature.Opacity = 0.8;
```

### 新增邊框
使用自訂邊框增強二維碼：

```csharp
qrCodeSignature.Border.Color = System.Drawing.Color.Red;
qrCodeSignature.Border.DashStyle = System.Drawing.Drawing2D.DashStyle.Dash;
qrCodeSignature.Border.Weight = 2;
qrCodeSignature.Border.Visible = true;
```

### 旋轉二維碼
將二維碼簽名旋轉到特定角度：

```csharp
qrCodeSignature.Angle = 30; // 旋轉 30 度
```

## 使用不同的文件格式
GroupDocs.Signature 支援更新各種文件格式的二維碼簽章：

- PDF 文件
- Microsoft Word 文件（DOC、DOCX）
- Microsoft Excel 電子表格（XLS、XLSX）
- Microsoft PowerPoint 簡報（PPT、PPTX）
- 開放文件格式
- 影像格式

只需進行少量調整，即可在這些格式中使用相同的程式碼。

## 結論
GroupDocs.Signature for .NET 提供了一個強大且靈活的解決方案，用於更新文件中的二維碼簽章。依照本教學中概述的步驟，開發人員可以在其 .NET 應用程式中有效地實現二維碼簽章更新功能，從而增強文件管理和驗證功能。

GroupDocs.Signature 憑藉其全面的功能集和直覺的 API，使開發人員能夠建立複雜的文件簽章解決方案，滿足現代商業應用程式的要求，同時確保文件的完整性和可存取性。

## 常見問題解答
### 我可以在單一文件中更新多個二維碼簽名嗎？
是的，GroupDocs.Signature 允許您更新同一文件中的多個二維碼簽章。搜尋簽名後，您可以遍歷結果清單並分別更新每個二維碼簽名。

### GroupDocs.Signature 是否支援不同的二維碼類型？
是的，GroupDocs.Signature 支援各種二維碼類型，包括標準二維碼、微型二維碼和其他二維碼。您可以使用 `EncodeType` 財產。

### GroupDocs.Signature for .NET 有試用版嗎？
是的，您可以從 [GroupDocs 網站](https://releases.groupdocs.com/signature/net/) 在購買之前評估圖書館的功能。

### 我可以透過程式更改二維碼糾錯等級嗎？
是的，您可以在新增新的二維碼時變更錯誤更正級別，但並非所有文件格式都支援更新現有二維碼的此屬性。

### 在哪裡可以找到對 GroupDocs.Signature for .NET 的額外支援？
您可以透過以下資源獲得全面的支援：
- [API 文件](https://docs.groupdocs.com/signature/net/)
- [API 參考](https://reference.groupdocs.com/signature/net/)
- [GitHub 範例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [支援論壇](https://forum.groupdocs.com/c/signature/13)
- [部落格](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)