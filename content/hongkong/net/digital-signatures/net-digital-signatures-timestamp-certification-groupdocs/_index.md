---
"date": "2025-05-07"
"description": "了解如何使用 GroupDocs.Signature 在 .NET 中對 PDF 進行數位簽名，包括新增時間戳記和驗證文件。確保文件的完整性和真實性。"
"title": "如何使用 GroupDocs.Signature for .NET 實作帶有時間戳記和認證的 .NET 數位簽名"
"url": "/zh-hant/net/digital-signatures/net-digital-signatures-timestamp-certification-groupdocs/"
"weight": 1
type: docs
---
# 如何使用 GroupDocs.Signature for .NET 實作帶有時間戳記和認證的 .NET 數位簽名

## 介紹

您是否希望使用 .NET 中的數位簽章來增強 PDF 文件的安全性？ GroupDocs.Signature for .NET 可以更輕鬆地確保文件的真實性、完整性和不可否認性。無論您是需要新增來自受信任的第三方網站的時間戳，還是需要認證文件是否符合法律規定，這個強大的函式庫都能簡化流程。

在本教程中，我們將指導您使用 GroupDocs.Signature for .NET 對 PDF 文件進行數位簽名，並在簽名中添加時間戳記。我們還將介紹如何使用數位簽章對這些文件進行認證。學習本指南後，您將全面了解如何在應用程式中實現這些功能。

**您將學到什麼：**
- 為 .NET 設定 GroupDocs.Signature
- 使用時間戳實現數位簽名
- 以數位方式認證 PDF 文件
- 優化效能和最佳實踐

讓我們深入了解開始的先決條件！

## 先決條件

在開始之前，請確保您具備以下條件：

1. **所需的庫和依賴項**
   - GroupDocs.Signature for .NET：此程式庫對於在您的應用程式中實作數位簽章至關重要。
   - .NET Framework（4.7.2 或更高版本）或 .NET Core 3.0+

2. **環境設定要求**
   - 類似 Visual Studio 的開發環境，您可以在其中建立和執行 C# 專案。

3. **知識前提**
   - 對 C# 程式設計有基本的了解。
   - 熟悉處理 .NET 應用程式中的檔案路徑和 I/O 操作。

## 為 .NET 設定 GroupDocs.Signature

若要將 GroupDocs.Signature 整合到您的專案中，請按照以下步驟操作：

**使用 .NET CLI：**

```bash
dotnet add package GroupDocs.Signature
```

**套件管理器控制台：**

```powershell
Install-Package GroupDocs.Signature
```

**NuGet 套件管理器 UI：**
在 NuGet 套件管理員中搜尋“GroupDocs.Signature”並安裝最新版本。

### 許可證獲取
- **免費試用：** 從免費試用開始探索 GroupDocs.Signature 的功能。
- **臨時執照：** 取得臨時許可證來無限制地評估功能。
- **購買：** 購買完整許可證以供長期使用。

設定好環境後，初始化並配置庫以開始簽署文件。

## 實施指南

我們將介紹兩個主要功能：為數位簽章新增時間戳記以及認證 PDF 文件。每個部分都會透過程式碼片段和說明逐步指導您。

### 帶有時間戳記的數位簽名

此功能可讓您以數位方式簽署 PDF，同時使用受信任的第三方時間戳伺服器確保簽名的有效性。

#### 步驟1：初始化簽名對象
首先，創建一個 `Signature` 透過提供文件的路徑來新增類別：

```csharp
string filePath = "@YOUR_DOCUMENT_DIRECTORY/sample.pdf";
using (Signature signature = new Signature(filePath))
{
    // 進一步的步驟將在此處添加
}
```

#### 步驟2：配置PdfDigitalSignature
創建並設定 `PdfDigitalSignature` 物件包含必要的詳細信息，例如聯絡資訊、位置和簽名原因：

```csharp
PdfDigitalSignature pdfDigitalSignature = new PdfDigitalSignature()
{
    ContactInfo = "Contact",
    Location = "Location",
    Reason = "Reason"
};
```

#### 步驟 3：設定時間戳詳細信息
透過指定第三方伺服器的 URL 來配置時間戳，在本例中， `freetsa.org`：

```csharp
pdfDigitalTimestamp = new TimeStamp("https://freetsa.org/tsr”, “”, “”);
pdfDigitalSignature.TimeStamp = pdfDigitalTimestamp;
```

#### 步驟 4：設定數位簽章選項
透過指定數位憑證路徑和密碼以及簽章對齊首選項來設定簽章選項：

```csharp
digitalSignOptions = new DigitalSignOptions(certificatePath)
{
    Password = "1234567890",
    Signature = pdfDigitalSignature,
    VerticalAlignment = VerticalAlignment.Bottom,
    HorizontalAlignment = HorizontalAlignment.Right
};
```

#### 第五步：簽署文件並取得結果
執行簽名流程，將簽名後的文件儲存到指定路徑，並列印結果：

```csharp
SignResult signResult = signature.Sign(outputFilePathSigned, digitalSignOptions);
Console.WriteLine($"
Source document signed successfully with {signResult.Succeeded.Count} signature(s).
File saved at {outputFilePathSigned}.
");
```

### 數位簽章認證

認證 PDF 文件可確保其符合一定的真實性和安全性標準。此流程對於法律和合規性至關重要。

#### 步驟1：初始化簽名對象
與時間戳功能類似，先初始化 `Signature` 班級：

```csharp
string filePath = "@YOUR_DOCUMENT_DIRECTORY/sample.pdf";
using (Signature signature = new Signature(filePath))
{
    // 進一步的步驟將在此處添加
}
```

#### 步驟2：配置PdfDigitalSignature進行認證
創建一個 `PdfDigitalSignature` 對象，指定詳細資訊並將類型設定為證書：

```csharp
PdfDigitalSignature pdfDigitalSignature = new PdfDigitalSignature()
{
    ContactInfo = "Contact",
    Location = "Location",
    Reason = "Reason"
};

pdfDigitalSignature.Type = PdfDigitalSignatureType.Certificate;
```

#### 步驟 3：設定數位簽章選項
設定簽名選項，類似於新增時間戳記：

```csharp
digitalSignOptions = new DigitalSignOptions(certificatePath)
{
    Password = "1234567890",
    Signature = pdfDigitalSignature,
    VerticalAlignment = VerticalAlignment.Bottom,
    HorizontalAlignment = HorizontalAlignment.Right
};
```

#### 步驟4：簽署文件並取得結果
執行認證流程，儲存認證文檔，並列印結果：

```csharp
SignResult signResult = signature.Sign(outputFilePathCertified, digitalSignOptions);
Console.WriteLine($"
Source document signed successfully with {signResult.Succeeded.Count} signature(s).
File saved at {outputFilePathCertified}.
");
```

## 實際應用

- **法律文件：** 確保合約和協議長期保持完整性。
- **財務報告：** 證明財務報表的準確性和合規性。
- **教育證書：** 驗證結業證書或獎勵證書。
- **電子商務交易：** 確保採購訂單和收據的安全。
- **政府表格：** 驗證提交給公共機構的表格。

## 性能考慮

為了優化使用 GroupDocs.Signature 時的效能：

- **資源使用：** 監控記憶體使用情況，尤其是在處理大型文件時。
- **批次：** 如果簽署多個文件，請考慮批次以提高效率。
- **非同步操作：** 使用非同步方法避免阻塞操作並提高應用程式的回應能力。

## 結論

透過本指南，您學習如何使用 GroupDocs.Signature for .NET 對 PDF 文件進行數位簽章並新增時間戳，以及如何對其進行認證。掌握這些技能後，您可以增強數位內容的安全性和真實性，確保跨領域的合規性。

下一步包括探索 GroupDocs.Signature 提供的其他功能，或將其整合到您應用程式中更大規模的工作流程中。歡迎您隨時嘗試不同的選項和配置。

## 常見問題部分

1. **什麼是數位簽章？**
   - 數位簽章可確保文件的真實性和完整性，就像數位領域的手寫簽名一樣。

2. **如何獲得簽署文件的證書？**
   - 您可以從受信任的憑證授權單位 (CA) 購買證書，或將自簽名憑證用於內部用途。

3. **GroupDocs.Signature 是否與所有 .NET 版本相容？**
   - 是的，它支援先決條件中指定的 .NET Framework 和 .NET Core。