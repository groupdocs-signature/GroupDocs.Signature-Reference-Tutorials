---
"date": "2025-05-07"
"description": "了解如何使用 GroupDocs.Signature for .NET 對 PDF 文件進行加密和二維碼簽名，從而確保文件安全。增強數位化工作流程中的文件真實性。"
"title": "使用 GroupDocs.Signature for .NET 使用二維碼加密和簽署 PDF"
"url": "/zh-hant/net/qr-code-signatures/encrypt-sign-pdf-qr-code-groupdocs-signature-net/"
"weight": 1
type: docs
---
# 使用 GroupDocs.Signature for .NET 使用二維碼加密和簽署 PDF

## 介紹

在當今的數位時代，確保文件的安全性和真實性至關重要。無論您是在保護敏感的商業合同，還是在驗證法律文件中的身份，加密和數位簽名都是必不可少的工具。本指南將指導您使用 GroupDocs.Signature for .NET 對帶有二維碼的 PDF 進行加密和簽名，從而提供額外的安全保障和驗證。

**您將學到什麼：**
- 如何設定 GroupDocs.Signature 庫
- 在 PDF 文件中實現加密和簽名
- 使用自訂資料建立二維碼簽名
- 配置項目以獲得最佳效能

在深入實施之前，讓我們先回顧一下您需要什麼。

## 先決條件（H2）
為了有效地遵循本教程，請確保您具備以下條件：

1. **所需的庫和版本：**
   - GroupDocs.Signature for .NET（最新版本）
   - 您的電腦上安裝了 .NET Core 或 .NET Framework

2. **環境設定要求：**
   - 支援 C# 的文字編輯器或 IDE（如 Visual Studio）
   - 對 C# 程式語言和 .NET 框架概念有基本的了解

3. **知識前提：**
   - 熟悉 C# 中的物件導向程式設計原理
   - 了解加密基礎知識，尤其是 AES 等對稱加密演算法

## 為 .NET 設定 GroupDocs.Signature（H2）

### 安裝資訊：
要將 GroupDocs.Signature 整合到您的專案中，您可以根據您的開發環境使用以下方法之一：

**.NET CLI：**
```bash
dotnet add package GroupDocs.Signature
```

**套件管理器：**
```powershell
Install-Package GroupDocs.Signature
```

**NuGet 套件管理器 UI：**
搜尋“GroupDocs.Signature”並安裝最新版本。

### 許可證取得步驟：
1. **免費試用：** 首先從下載試用版 [GroupDocs 免費試用](https://releases.groupdocs.com/signature/net/)。這使您無需做出承諾即可探索功能。
   
2. **臨時執照：** 如需延長測試時間，請申請臨時駕照 [臨時執照](https://purchase。groupdocs.com/temporary-license/).

3. **購買：** 如果對功能滿意，請從 [GroupDocs 購買頁面](https://purchase.groupdocs.com/buy) 繼續無限制地使用該產品。

### 基本初始化和設定：
安裝 GroupDocs.Signature 後，請在 C# 專案中進行初始化，如下所示：
```csharp
using (Signature signature = new Signature("Sample.pdf"))
{
    // 您的簽名邏輯在這裡
}
```
此基本設定足以開始使用 GroupDocs.Signature 執行文件處理任務。

## 實施指南

### 使用二維碼加密和簽署 PDF 文檔
讓我們將該流程分解為可管理的步驟，以便在 PDF 文件中實現加密和簽名：

#### 1.定義自訂資料簽章類別（H3）
在深入研究簽章選項之前，先定義一個自訂類別來儲存要序列化到二維碼中的資料：
```csharp
class DocumentSignatureData
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
```
**為什麼這很重要：** 自訂資料可讓您將特定的元資料嵌入到二維碼中，使其能夠滿足各種文件管理需求。

#### 2. 設定加密（H3）
選擇像AES這樣的對稱加密演算法，安全高效：
```csharp
string key = "1234567890"; // 你的密鑰
string salt = "1234567890"; // 增加獨特性的鹽

IDataEncryption encryption = new SymmetricEncryption(SymmetricAlgorithmType.AES, key, salt);
```
**為什麼要使用 AES？** AES 被廣泛認為是安全且快速的，使其成為加密敏感資料的標準選擇。

#### 3. 準備二維碼簽名選項（H3）
配置二維碼簽名選項以包含您的自訂資料和加密設定：
```csharp
QrCodeSignOptions options = new QrCodeSignOptions()
{
    Data = new DocumentSignatureData()
    {
        ID = Guid.NewGuid().ToString(),
        Author = Environment.UserName,
        Signed = DateTime.Now,
        DataFactor = 11.22M
    },
    EncodeType = QrCodeTypes.QR,
    DataEncryption = encryption,
    Height = 100,
    Width = 100,
    VerticalAlignment = VerticalAlignment.Center,
    HorizontalAlignment = HorizontalAlignment.Left,
    Margin = new Padding() { Right = 10, Bottom = 10 }
};
```
**關鍵配置選項：** 調整 `Height`， `Width`和對齊方式以滿足文件的設計需求。

#### 4. 簽署文件（H3）
最後，將簽名選項套用到您的文件：
```csharp
using (Signature signature = new Signature("Sample.pdf"))
{
    string outputFilePath = "QRCodeEncryptedObject.pdf";
    signature.Sign(outputFilePath, options);
}
```
**簽名為何重要：** 此步驟透過在二維碼中嵌入加密資料來保護您的文檔，確保真實性和機密性。

### 故障排除提示：
- 確保加密金鑰和鹽的安全。
- 驗證檔案路徑以避免 `FileNotFoundException`。
- 檢查與不支援的文件格式或簽名選項相關的異常。

## 實際應用（H2）
將 GroupDocs.Signature 與二維碼加密整合在以下幾種情況下很有價值：

1. **法律文件驗證：** 透過嵌入驗證真實性的加密細節來增強合約安全性。
   
2. **公司協議：** 使用額外的加密簽名來保護敏感的公司協議。
   
3. **醫療記錄管理：** 使用加密的數位簽章確保患者資料的機密性。
   
4. **活動票務系統：** 透過在設計中加入加密的二維碼來保護活動門票免遭詐騙。
   
5. **供應鏈文件：** 驗證裝運和接收文件以防止運輸過程中被竄改。

## 性能考慮（H2）
優化應用程式的效能至關重要，尤其是在處理大量文件時：

- **記憶體管理：** 使用 `using` 語句來有效地管理資源並避免記憶體洩漏。
  
- **批次：** 批量處理多個文件而不是單獨處理以提高吞吐量。
  
- **錯誤處理：** 實施強大的錯誤處理機制，以便從異常中正常恢復。

## 結論
透過本指南，您學習如何使用 GroupDocs.Signature for .NET 實作二維碼加密和簽章。這項強大的功能不僅可以增強文件安全性，還能提昇在當今數位環境中至關重要的真實性。

**後續步驟：**
- 探索 GroupDocs.Signature 支援的其他簽章類型。
- 將該解決方案整合到您現有的文件管理系統中。

如果您有任何疑問，或想分享您實現此功能的經驗，請隨時與我們聯繫。祝您編碼愉快！

## 常見問題部分（H2）

1. **什麼是 AES 加密以及為什麼要使用它？**
   AES，即高級加密標準，是一種以速度和安全性著稱的對稱加密演算法，非常適合加密二維碼內的敏感資料。

2. **我可以自訂二維碼簽名的外觀嗎？**
   是的，您可以使用 GroupDocs.Signature 選項調整大小、對齊方式和邊距以滿足文件的設計要求。

3. **我可以在二維碼中加密的資料量有限制嗎？**
   雖然沒有嚴格的限制，但請確保資料符合二維碼的容量。