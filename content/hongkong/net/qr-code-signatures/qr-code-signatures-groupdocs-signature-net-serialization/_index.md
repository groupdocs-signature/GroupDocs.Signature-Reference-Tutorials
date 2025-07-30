---
"date": "2025-05-07"
"description": "了解如何使用 GroupDocs.Signature for .NET 實作自訂序列化的二維碼簽章。增強文件安全性並有效率地管理資料。"
"title": "使用 GroupDocs.Signature 在 .NET 中透過自訂序列化實現二維碼簽名"
"url": "/zh-hant/net/qr-code-signatures/qr-code-signatures-groupdocs-signature-net-serialization/"
"weight": 1
---

# 使用 GroupDocs.Signature 在 .NET 中實作自訂序列化的二維碼簽名

## 介紹

在當今的數位時代，管理文件真實性在法律、商業和軟體開發等各個領域都至關重要。 GroupDocs.Signature for .NET 提供強大的功能，可將二維碼簽章與自訂資料序列化無縫整合到您的應用程式中。

本教學探討如何使用 GroupDocs.Signature for .NET 中的自訂序列化實作二維碼簽名，增強文件安全性並提供可自訂的簽名資料處理方法。

**您將學到什麼：**
- QR 碼中自訂資料序列化的基礎知識
- GroupDocs.Signature for .NET 的環境設置
- 使用自訂選項實作和搜尋二維碼簽名
- 現實場景中的實際應用

在深入實施之前，讓我們先回顧一些先決條件。

## 先決條件

要有效地遵循本教程：

### 所需的函式庫、版本和相依性

- GroupDocs.Signature for .NET：確保與您的 .NET Framework 或 .NET Core 版本相容。
- 使用 Visual Studio 2019/2022 或其他支援 .NET 專案的 IDE。

### 環境設定要求

- 存取儲存文件的檔案系統。
- 對 C# 程式設計有基本的了解，並熟悉物件導向的概念。

### 知識前提

- 了解文件安全中的二維碼。
- 熟悉資料序列化概念。

## 為 .NET 設定 GroupDocs.Signature

若要開始使用 GroupDocs.Signature，請設定您的開發環境：

**安裝 GroupDocs.Signature：**

選擇您喜歡的安裝方法：

**.NET CLI**
```bash
dotnet add package GroupDocs.Signature
```

**套件管理器**
```powershell
Install-Package GroupDocs.Signature
```

**NuGet 套件管理器 UI**
搜尋“GroupDocs.Signature”並安裝最新版本。

### 許可證取得步驟

1. **免費試用：** 下載免費試用版 [這裡](https://releases。groupdocs.com/signature/net/).
2. **臨時執照：** 申請臨時許可證以進行無限制評估。
3. **購買：** 如需長期使用，請購買完整版 [GroupDocs 的購買頁面](https://purchase。groupdocs.com/buy).

### 基本初始化和設定

安裝後，在您的 C# 專案中初始化 GroupDocs.Signature：

```csharp
using GroupDocs.Signature;

// 使用文件路徑初始化一個新的簽章實例
Signature signature = new Signature("YOUR_DOCUMENT_PATH");
```

這將設定您的環境以開始實施二維碼簽名。

## 實施指南

在本節中，我們將介紹如何使用 GroupDocs.Signature for .NET 實作二維碼簽章的自訂資料序列化和搜尋。

### QR碼簽名的自訂資料序列化

**概述：**
自訂資料序列化可讓您為簽名資料定義特定格式，這對於根據應用程式的要求建立資訊至關重要。

#### 步驟1：定義簽章資料類

建立一個保存簽名資料的類別：

```csharp
using System;
using GroupDocs.Signature.Domain;

[CustomSerialization]
private class DocumentSignatureData
{
    [Format("SignID")]
    public string ID { get; set; }

    [Format("SAuth")]
    public string Author { get; set; }

    [Format("SDate", "yyyy-MM-dd")]
    public DateTime Signed { get; set; }

    [Format("SDFact", "N2")]
    public decimal DataFactor { get; set; }

    // 從序列化中排除註解字段
    [SkipSerialization]
    public string Comments { get; set; }
}
```

**解釋：**
- **自訂序列化：** 將此類標記為自訂資料處理。
- **格式屬性：** 定義每個屬性的序列化方式，包括格式類型。
- **跳過序列化：** 從序列化中排除某些屬性。

#### 步驟 2：使用自訂選項搜尋二維碼簽名

**概述：**
您可以使用自訂選項在文件中搜尋二維碼簽名，確保高效率的文件驗證。

##### 設定搜尋

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Options;
using GroupDocs.Signature.Domain.Extensions;

public class SearchForQRCodeWithCustomOptions
{
    public static void Run()
    {
        string filePath = "YOUR_DOCUMENT_DIRECTORY";

        using (Signature signature = new Signature(filePath))
        {
            IDataEncryption encryption = new CustomXOREncryption();

            QrCodeSearchOptions options = new QrCodeSearchOptions()
            {
                AllPages = true,
                DataEncryption = encryption
            };

            try
            {
                List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);

                foreach (var qrCodeSignature in signatures)
                {
                    DocumentSignatureData documentSignatureData = qrCodeSignature.GetData<DocumentSignatureData>();
                    if (documentSignatureData != null)
                    {
                        Console.WriteLine("QRCode signature found with details:");
                        Console.WriteLine("ID: {0}, Author: {1}, Signed: {2}, DataFactor: {3}", 
                            documentSignatureData.ID, documentSignatureData.Author,
                            documentSignatureData.Signed.ToShortDateString(), documentSignatureData.DataFactor);
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine("Error during search process: " + ex.Message);
            }
        }
    }
}
```

**解釋：**
- **自訂XOREncryption：** 實施自訂資料加密以增加安全性。
- **QrCode搜尋選項：** 配置二維碼搜尋設置，包括應用自訂資料加密。
- **GetData方法：** 從找到的簽章中提取序列化資料。

### 故障排除提示

- 確保正確指定文件路徑以避免文件未找到異常。
- 驗證所有相依性均已安裝且為最新，以防止執行時間錯誤。

## 實際應用

自訂序列化的二維碼簽名可以應用於各種場景：

1. **法律合約：** 透過在法律文件中嵌入獨特的加密簽名來增強合約安全性。
2. **財務文件：** 透過安全簽章驗證確保財務報表的真實性。
3. **身份驗證：** 使用序列化的二維碼資料實現一個強大的身份驗證系統。
4. **供應鏈管理：** 使用自訂序列化的二維碼來追蹤和驗證裝運文件。
5. **醫療記錄：** 透過整合加密的二維碼簽章來保護病患記錄。

## 性能考慮

為了優化實施的性能：
- 使用高效的加密演算法來最大限度地減少處理時間。
- 透過在 .NET 應用程式中適當處置未使用的物件和流來優化記憶體使用情況。
- 定期更新 GroupDocs.Signature 以利用新版本的改進和錯誤修復。

## 結論

本教學探討如何使用 GroupDocs.Signature for .NET 實作自訂序列化的二維碼簽章。請按照以下步驟操作，您可以增強文件安全性並有效地自訂簽章資料處理。