---
"date": "2025-05-07"
"description": "了解如何使用 GroupDocs.Signature 在 .NET 中安全地對 PDF 文件進行簽名，並附帶元資料和加密功能。本指南涵蓋設定、實施和最佳實務。"
"title": "如何使用 GroupDocs.Signature for .NET 對 PDF 進行元資料和加密簽章 | 安全性文件保護指南"
"url": "/zh-hant/net/document-protection/sign-pdfs-metadata-encryption-groupdocs-dotnet/"
"weight": 1
---

# 如何使用 GroupDocs.Signature for .NET 對 PDF 進行元資料和加密簽名

## 介紹

您是否正在尋找一個強大的解決方案，以便在 .NET 中使用元資料和加密技術安全地簽署 PDF 文件？在本指南中，我們將探討如何使用 GroupDocs.Signature for .NET 來實現這一目標。從設定環境到執行簽名流程，我們將逐步解說每個步驟，確保您的資料安全且可驗證。

**您將學到什麼：**
- 如何在 C# 中使用自訂資料類別定義元數據
- 使用加密創建元資料簽名
- 使用 GroupDocs.Signature for .NET 簽署 PDF 文檔
- 設定環境並整合庫

讓我們深入了解如何利用這款強大的工具進行安全文件簽名。但首先，請閱讀下方的先決條件部分，確保您已做好準備。

## 先決條件

在開始為 .NET 實作 GroupDocs.Signature 之前，請確保您具備以下條件：

### 所需的庫和版本
- **GroupDocs.簽名**：確保您安裝的版本與您的專案設定相容。
  
### 環境設定要求
- 您的系統上安裝了 .NET Framework 或 .NET Core。

### 知識前提
- 熟悉C#程式語言。
- 對以程式設計方式處理 PDF 文件有基本的了解。

## 為 .NET 設定 GroupDocs.Signature

要開始使用 GroupDocs.Signature，您需要將其安裝到您的專案中。以下是可用的不同方法：

**使用 .NET CLI：**
```shell
dotnet add package GroupDocs.Signature
```

**使用套件管理器：**
```powershell
Install-Package GroupDocs.Signature
```

**NuGet 套件管理器 UI：**
1. 開啟 NuGet 套件管理器。
2. 搜尋“GroupDocs.Signature”並安裝最新版本。

### 許可證獲取

您可以取得免費試用版或臨時許可證，以探索 GroupDocs.Signature 的所有功能。如需長期使用，請考慮購買授權：
- **免費試用**： [免費下載](https://releases.groupdocs.com/signature/net/)
- **臨時執照**： [在此請求](https://purchase.groupdocs.com/temporary-license/)
- **購買許可證**： [立即購買](https://purchase.groupdocs.com/buy)

取得許可證後，在專案中初始化 GroupDocs.Signature 以開始使用其功能。

## 實施指南

### 元資料簽章資料類

**概述：**
定義一個資料類，用於保存簽章所需的元資料資訊。此類別將用於保存各種屬性，例如 ID、作者、簽名日期以及特定格式的資料因子 (DataFactor)。

#### 步驟 1：定義資料類
```csharp
using System;

namespace GroupDocs.Signature.Domain
{
    public class DocumentSignatureData
    {
        [Format("SignID")]
        public string ID { get; set; }

        [Format("SAuth")]
        public string Author { get; set; }

        [Format("SDate", "yyyy-MM-dd")]
        public DateTime Signed { get; set; }

        [Format("SDFact", "N2")]
        public decimal DataFactor { get; set; }
    }
}
```

**解釋：**
- `ID`， `Author`， `Signed`， 和 `DataFactor` 是使用以下方式定義的具有特定格式的屬性 `[Format]`。
- 此設定可確保元資料的簽章格式一致。

### 元資料簽章建立和加密

**概述：**
了解如何使用 Rijndael 對稱加密演算法建立和加密元資料簽章。

#### 第 2 步：設定對稱加密
```csharp
using System;
using GroupDocs.Signature;

namespace MetadataSignatureCreation
{
    public class CreateMetadataSignatures
    {
        string key = "1234567890"; // 在生產中使用安全密鑰
        string salt = "1234567890"; // 在生產中使用安全的鹽

        IDataEncryption encryption = new SymmetricEncryption(SymmetricAlgorithmType.Rijndael, key, salt);

        DocumentSignatureData documentSignature = new DocumentSignatureData()
        {
            ID = Guid.NewGuid().ToString(),
            Author = Environment.UserName,
            Signed = DateTime.Now,
            DataFactor = 11.22M
        };

        PdfMetadataSignature mdDocument = new PdfMetadataSignature("DocumentSignature", documentSignature);
        mdDocument.DataEncryption = encryption;

        PdfMetadataSignature mdAuthor = new PdfMetadataSignature("Author", "Mr.Sherlock Holmes");
        mdAuthor.DataEncryption = encryption;

        PdfMetadataSignature mdDocId = new PdfMetadataSignature("DocumentId", Guid.NewGuid().ToString());
        mdDocId.DataEncryption = encryption;
    }
}
```

**解釋：**
- `SymmetricEncryption` 設定了金鑰和鹽，確保元資料的安全加密。
- 為文件詳細資訊和作者資訊建立元資料簽名。

### 使用元資料簽名對 PDF 進行簽名

**概述：**
使用 GroupDocs.Signature 庫實現簽署流程，以使用準備好的元資料簽章對您的 PDF 文件進行簽署。

#### 步驟 3：簽署 PDF
```csharp
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Options;

namespace SignPdfWithMetadata
{
    public class SignPdf
    {
        string filePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "sample.pdf");
        string fileName = Path.GetFileName(filePath);
        string outputFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignPdfWithCustomMetadata", fileName);

        public void Execute()
        {
            using (Signature signature = new Signature(filePath))
            {
                MetadataSignOptions options = new MetadataSignOptions();

                CreateMetadataSignatures signer = new CreateMetadataSignatures();
                options.Add(signer.mdDocument);
                options.Add(signer.mdAuthor);
                options.Add(signer.mdDocId);

                SignResult signResult = signature.Sign(outputFilePath, options);
            }
        }
    }
}
```

**解釋：**
- 這 `Signature` 該類別使用 PDF 文件路徑進行初始化。
- `MetadataSignOptions` 用於新增元資料簽章以進行簽章。
- 簽名後的文件保存在指定的輸出路徑。

## 實際應用

### 真實用例
1. **法律文件簽署**：使用加密元資料自動簽署合約和協議，以增強安全性。
2. **發票管理**：對發票進行數位簽名，安全地嵌入客戶和交易詳細資料。
3. **頒發認證證書**：頒發包含頒發日期和收件人資訊等加密元資料的證書。

### 整合可能性
- 與 CRM 系統整合以自動化簽名工作流程。
- 與文件管理解決方案結合，實現簽署文件的安全存檔。

## 性能考慮

使用 GroupDocs.Signature 時，請考慮以下效能提示：
- 透過在使用後及時處置資源來優化記憶體使用。
- 在高負載環境中利用非同步簽章操作。
- 定期更新庫以受益於效能改進和新功能。

## 結論

在本指南中，我們探討如何使用 GroupDocs.Signature for .NET 對具有元資料和加密的 PDF 文件進行簽署。請按照以下步驟操作，您可以確保您的數位簽章安全且合規。

**後續步驟：**
- 嘗試不同的元資料配置。
- 透過查看文件來探索 GroupDocs.Signature 的其他功能。

準備好嘗試了嗎？在您的下一個專案中實施此解決方案，以增強文件安全性！

## 常見問題部分

**問題 1：我可以將 GroupDocs.Signature 用於大型 PDF 文件嗎？**
A1：是的，它旨在高效處理大文件。請確保您擁有足夠的系統資源。

**問題 2：如何解決簽章錯誤？**
A2：請檢查您的檔案路徑，並確保所有依賴項已正確安裝。具體錯誤代碼請參考文件。

**Q3：我可以自訂加密演算法嗎？**
A3：雖然建議使用 Rijndael，但您可以參考 GroupDocs.Signature 文件來探索其他支援的演算法。