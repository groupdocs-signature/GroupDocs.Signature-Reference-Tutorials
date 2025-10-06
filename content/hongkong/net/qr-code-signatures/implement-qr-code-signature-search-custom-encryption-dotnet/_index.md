---
"date": "2025-05-07"
"description": "了解如何使用 GroupDocs.Signature 在 .NET 應用程式中實作自訂加密的安全二維碼簽章搜尋。遵循這份全面的指南，實現無縫整合。"
"title": "使用 GroupDocs.Signature 在 .NET 中實作自訂加密的二維碼簽章搜尋"
"url": "/zh-hant/net/qr-code-signatures/implement-qr-code-signature-search-custom-encryption-dotnet/"
"weight": 1
type: docs
---
# 使用 GroupDocs.Signature for .NET 實作自訂加密的二維碼簽章搜尋

## 介紹

在數位文件管理領域，透過簽名確保文件的真實性和完整性至關重要。 GroupDocs.Signature for .NET 提供了強大的解決方案，可有效處理簽章資料。本教學將指導您在應用程式中實現帶有自訂加密的安全二維碼簽章搜尋。

**您將學到什麼：**
- 定義一個自訂類別來處理簽名資料。
- 在文件中搜尋二維碼簽名。
- 實施自訂加密選項以增強安全性。
- 應用 .NET 開發中的最佳實務。

完成本指南後，您將能夠將這些功能無縫整合到您的應用程式中。首先，讓我們確保滿足所有先決條件。

## 先決條件

在開始之前，請確保您已：
- **所需庫：** GroupDocs.Signature 用於 .NET 函式庫。
- **環境設定：** 使用 Visual Studio 或任何支援 .NET 應用程式的首選 IDE 設定的開發環境。
- **知識前提：** 對 C# 和 .NET 架構有基本的了解。

## 為 .NET 設定 GroupDocs.Signature

### 安裝

使用下列套件管理器之一安裝 GroupDocs.Signature 庫：

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

### 許可證獲取

若要使用 GroupDocs.Signature，請取得許可證：
- **免費試用：** 探索基本特徵。
- **臨時執照：** 進行更廣泛的測試。
- **完整許可證：** 供生產使用。

訪問 [GroupDocs 許可](https://purchase.groupdocs.com/faqs/licensing) 有關獲取這些許可證的更多資訊。

### 基本初始化和設定

使用以下程式碼片段在您的應用程式中初始化 GroupDocs.Signature：

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_PATH"))
{
    // 您的實作在這裡。
}
```

## 實施指南

本節指導您使用自訂加密實現二維碼簽章搜尋。

### 定義自訂資料簽名類

#### 概述

首先，定義一個自訂類別來表示二維碼簽章中的資料。這允許自訂處理簽名訊息，包括以下屬性： `ID`， `Author`， 和 `Signed`。

#### 實施步驟

**1.建立自訂類**

```csharp
using System;
using GroupDocs.Signature.Domain;

namespace GroupDocs.Signature.Examples.CSharp.AdvancedUsage
{
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
        
        [SkipSerialization]
        public string Comments { get; set; }
    }
}
```

**解釋：**
- **[格式]** 屬性將類別屬性對應到特定的資料格式。
- 這 `Comments` 屬性標記為 `[SkipSerialization]`，表示不會被序列化，從而增強安全性和效能。

### 使用自訂選項搜尋文件中的二維碼簽名

#### 概述

實作一種使用自訂加密選項在文件中搜尋二維碼簽章的方法，以確保敏感資料的安全處理。

#### 實施步驟

**2. 設定加密和搜尋選項**

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Options;

namespace GroupDocs.Signature.Examples.CSharp.AdvancedUsage
{
    public class SearchForQRCodeCustomEncryptionObject
    {
        public static void Run()
        {
            string filePath = "YOUR_DOCUMENT_DIRECTORY\\SamplePdfQrCodeCustomEncryptionObject.pdf";

            using (Signature signature = new Signature(filePath))
            {
                // 建立自訂資料加密實例。
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
                            Console.WriteLine(
                                "QRCode signature found at page {0} with type {1}. ID = {2}, Author = {3}, Signed = {4}, DataFactor = {5}",
                                qrCodeSignature.PageNumber, 
                                qrCodeSignature.EncodeType,
                                documentSignatureData.ID, 
                                documentSignatureData.Author, 
                                documentSignatureData.Signed.ToShortDateString(), 
                                documentSignatureData.DataFactor
                            );
                        }
                    }
                }
                catch (Exception ex)
                {
                    Console.WriteLine("An error occurred: " + ex.Message);
                    Console.WriteLine(
                        "This example requires a license to properly run. Visit the GroupDocs site to obtain a temporary or permanent license."
                    );
                }
            }
        }
    }
}
```

**解釋：**
- **自訂XOREncryption：** 實作自訂資料加密。
- 這 `QrCodeSearchOptions` 物件指定應搜尋所有頁面，並套用加密。

### 故障排除提示

- 確保正確指定文件路徑以避免文件未找到錯誤。
- 驗證您是否擁有處理二維碼簽名所需的許可證。

## 實際應用

此功能可增強各種現實世界場景：

1. **法律文件：** 使用安全加密自動驗證並從法律合約中提取簽名資料。
2. **財務報告：** 在財務文件中搜尋經過驗證的簽名，確保資料的完整性和合規性。
3. **醫療記錄：** 使用加密的二維碼簽章安全地管理敏感的醫療記錄，保護病患資訊。

## 性能考慮

- **優化資源使用：** 逐步處理大檔案以減少記憶體消耗。
- **.NET記憶體管理的最佳實務：**
  - 使用 `using` 聲明以確保妥善處置資源。
  - 分析您的應用程式以識別和優化效能瓶頸。

## 結論

在本教學中，您學習如何使用 GroupDocs.Signature for .NET 實作自訂加密的二維碼簽章搜尋。您學習如何定義自訂資料類別、設定自訂加密的搜尋選項，並探索了這些功能在實際場景中的實際應用。

**後續步驟：**
- 嘗試不同類型的簽名。
- 探索 GroupDocs.Signature 提供的附加功能，以增強應用程式的文件管理功能。

準備好嘗試使用自訂加密實作二維碼簽章搜尋了嗎？立即開始將安全且高效的解決方案整合到您的 .NET 應用程式中！