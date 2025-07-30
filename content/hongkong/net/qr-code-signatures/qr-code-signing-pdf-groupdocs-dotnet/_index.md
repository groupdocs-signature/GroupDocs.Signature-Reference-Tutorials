---
"date": "2025-05-07"
"description": "了解如何使用 GroupDocs.Signature 在 .NET 應用程式中透過精確對齊和自訂的二維碼簽署 PDF 文件。"
"title": "如何使用 GroupDocs.Signature for .NET 對帶有二維碼的 PDF 進行簽名"
"url": "/zh-hant/net/qr-code-signatures/qr-code-signing-pdf-groupdocs-dotnet/"
"weight": 1
---

# 如何使用 GroupDocs.Signature for .NET 對帶有二維碼的 PDF 進行簽名

## 介紹

對 PDF 文件進行數位簽署並確保簽名位置準確對於商業、法律和官方記錄至關重要。本教程將指導您使用 **適用於 .NET 的 GroupDocs.Signature** 透過精確對齊二維碼簽章的位置來簽署 PDF 檔案。閱讀完本指南後，您將了解如何：

- 安裝並配置 GroupDocs.Signature for .NET
- 為您的數位簽名使用不同的對齊設置
- 自訂二維碼的大小和邊距

我們將首先回顧先決條件，以確保您已做好成功準備。

## 先決條件

要遵循本教程，請確保您已具備：

- **適用於 .NET 的 GroupDocs.Signature**：可透過 .NET CLI、套件管理器控制台或 NuGet 安裝。
- **環境設定**：Visual Studio 2019 或更高版本，帶有 .NET Framework 版本 4.6.1+。
- **了解 C# 程式設計和數位簽名**。

## 為 .NET 設定 GroupDocs.Signature

### 安裝

首先，使用以下方法之一安裝 GroupDocs.Signature 套件：

**使用 .NET CLI：**
```bash
dotnet add package GroupDocs.Signature
```

**使用套件管理器控制台：**
```powershell
Install-Package GroupDocs.Signature
```

**使用 NuGet 套件管理器 UI：**
- 在 Visual Studio 中開啟您的解決方案。
- 導航至“NuGet 套件管理器”。
- 搜尋“GroupDocs.Signature”並安裝最新版本。

### 許可證獲取

要使用 GroupDocs.Signature，您可能需要許可證。具體方法如下：
- **免費試用**：下載自 [GroupDocs 簽章下載](https://releases。groupdocs.com/signature/net/).
- **臨時執照**：請求方式 [GroupDocs 購買](https://purchase。groupdocs.com/temporary-license/).
- **購買**：如需長期使用，請透過以下方式購買產品 [GroupDocs 購買](https://purchase。groupdocs.com/buy).

### 基本初始化

在您的應用程式中設定並初始化 GroupDocs.Signature：

```csharp
using GroupDocs.Signature;
using System;

// 使用輸入文檔路徑初始化簽名實例
string filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
Signature signature = new Signature(filePath);
Console.WriteLine("GroupDocs.Signature for .NET is ready to use.");
```

## 實施指南

### 功能概述：使用二維碼定位簽署 PDF

此功能可讓您簽署 PDF 文檔，同時使用各種對齊設定精確控制二維碼簽章的位置。

#### 步驟 1：定義文件和輸出路徑

指定來源 PDF 檔案的路徑以及簽章輸出的儲存位置：

```csharp
string filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf"; // 替換為您的文件路徑
string fileName = System.IO.Path.GetFileName(filePath);
string outputFilePath = System.IO.Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithAlignment", fileName);
```

#### 步驟2：設定二維碼簽名選項

透過迭代不同的水平和垂直對齊來設定二維碼簽名的大小和對齊選項：

```csharp
using GroupDocs.Signature.Options;
using System.Collections.Generic;

// 定義二維碼尺寸
int qrWidth = 100;
int qrHeight = 100;

List<SignOptions> listOptions = new List<SignOptions>();

foreach (HorizontalAlignment horizontalAlignment in Enum.GetValues(typeof(HorizontalAlignment)))
{
    foreach (VerticalAlignment verticalAlignment in Enum.GetValues(typeof(VerticalAlignment)))
    {
        if (verticalAlignment != VerticalAlignment.None && horizontalAlignment != HorizontalAlignment.None)
        {
            // 新增具有指定對齊方式和邊距的 QRCodeSignOptions
            listOptions.Add(new QrCodeSignOptions("Left-Top")
            {
                Width = qrWidth,
                Height = qrHeight,
                HorizontalAlignment = horizontalAlignment,
                VerticalAlignment = verticalAlignment,
                Margin = new Padding(5)
            });
        }
    }
}
```

#### 步驟3：簽署文件

使用定義的選項簽署您的文件並儲存：

```csharp
using (Signature signature = new Signature(filePath))
{
    // 使用指定的選項簽署文件並將其儲存到輸出文件路徑
    SignResult signResult = signature.Sign(outputFilePath, listOptions);
}
```

### 故障排除提示

- 確保您的專案中正確引用了所有必要的庫。
- 驗證輸入和輸出檔案的路徑是否正確設定。
- 如果簽名未如預期出現，請檢查對齊設定。

## 實際應用

GroupDocs.Signature 的二維碼定位功能可用於：

- **法律文件**：確保合約和協議上的簽名準確無誤。
- **商業報告**：透過在特定位置新增數位簽章來簡化文件審批流程。
- **教育證書**：自動簽署帶有連結到學生詳細資料的二維碼的證書。

## 性能考慮

為了在使用 GroupDocs.Signature 時獲得最佳性能：

- 如果可能的話，透過分塊處理大型 PDF 檔案來優化記憶體使用情況。
- 在適用的情況下使用非同步方法來保持應用程式的回應。
- 定期更新至 GroupDocs.Signature 的最新版本，以提高效能和修復錯誤。

## 結論

您已經學習如何使用 GroupDocs.Signature for .NET 為 PDF 文件簽章時實現二維碼定位。掌握這些知識後，您可以透過確保數位簽章的精確對齊和自訂來增強文件管理系統。接下來，您可以探索 GroupDocs.Signature 的全部功能，或深入研究時間戳記和加密等其他功能。

## 常見問題部分

**問題 1：什麼是 .NET 的 GroupDocs.Signature？**
A1：一個綜合庫，允許開發人員在各種格式的文件（包括 PDF）中添加數位簽章。

**Q2：如何為我的專案安裝 GroupDocs.Signature？**
A2：透過 .NET CLI、套件管理器控制台或 NuGet 套件管理器 UI 搜尋「GroupDocs.Signature」進行安裝。

**問題 3：我可以將二維碼放置在文件中的任何位置嗎？**
A3：是的，您可以設定水平和垂直對齊，以便在文件中精確放置二維碼。

**Q4：GroupDocs.Signature 還支援哪些其他簽章類型？**
A4：除了二維碼，它還支援文字、圖像、數位簽名、印章簽名等。

**Q5：GroupDocs.Signature 有試用版嗎？**
A5：是的，從官方下載頁面下載免費試用版來測試其功能。

## 資源
- **文件**： [GroupDocs 簽署文檔](https://docs.groupdocs.com/signature/net/)
- **API 參考**： [GroupDocs API 參考](https://reference.groupdocs.com/signature/net/)
- **下載**： [GroupDocs 簽章下載](https://releases.groupdocs.com/signature/net/)
- **購買**： [購買 GroupDocs 商品](https://purchase.groupdocs.com/buy)