---
"date": "2025-05-07"
"description": "了解如何使用 GroupDocs.Signature for .NET 將 GS1DotCode 和 HanXin QR Code 簽章整合到您的文件中。增強安全性並簡化工作流程。"
"title": "使用 GroupDocs.Signature for .NET 對 GS1DotCode 和 HanXin QR 碼進行安全文件簽名"
"url": "/zh-hant/net/barcode-signatures/sign-documents-gs1dotcode-hanxin-qr-groupdocs-signature-dotnet/"
"weight": 1
type: docs
---
# 使用 GroupDocs.Signature for .NET 對 GS1DotCode 和 HanXin QR 碼進行安全文件簽名
## 如何使用 GroupDocs.Signature for .NET 簽署帶有 GS1DotCode 和 HanXin QR 碼的文檔
在當今的數位時代，安全地以電子方式簽署文件至關重要。無論您是商務人士還是希望實現工作流程自動化的開發人員，整合條碼和二維碼簽名都能增強安全性並簡化流程。本教學將指導您使用 GroupDocs.Signature for .NET 在應用程式中實作 GS1DotCode 和漢信二維碼簽章。
## 您將學到什麼
- 將 GroupDocs.Signature for .NET 整合到您的專案中。
- 使用 GS1DotCode 條碼簽署文件。
- 實作漢信二維碼簽章。
- 列出簽署文件後新建立的簽名。
- 了解實際應用和效能考量。
準備好增強您的文件工作流程了嗎？讓我們開始吧！
## 先決條件
在開始之前，請確保您已具備以下條件：
### 所需庫
- **適用於 .NET 的 GroupDocs.Signature**：此程式庫允許您使用不同的條碼和二維碼格式簽署各種類型的文件。
### 環境設定要求
- 使用相容的 .NET 環境（最好是 .NET Core 或 .NET Framework 4.7.2+）。
- 如果您正在使用桌面應用程序，請安裝 Visual Studio。
### 知識前提
- 對 C# 和 .NET 開發有基本的了解。
- 熟悉使用 NuGet 套件進行依賴項管理。
## 為 .NET 設定 GroupDocs.Signature
首先安裝 GroupDocs.Signature 庫：
**使用 .NET CLI**
```bash
dotnet add package GroupDocs.Signature
```
**套件管理器控制台**
```powershell
Install-Package GroupDocs.Signature
```
**NuGet 套件管理器 UI**： 
搜尋“GroupDocs.Signature”並安裝最新版本。
### 許可證取得步驟
- **免費試用**：下載試用版來測試功能。
- **臨時執照**：申請臨時許可證以進行延長評估。
- **購買**：如果您準備在生產中部署，請購買完整許可證。
#### 基本初始化
若要初始化 GroupDocs.Signature，請建立一個實例 `Signature` 類與您的文件路徑：
```csharp
using (Signature signature = new Signature("your-document-path"))
{
    // 您的簽名代碼在這裡
}
```
## 實施指南
讓我們逐步分解如何實現每個功能。
### 使用 GS1DotCode 條碼簽署文件
**概述**：將 GS1DotCode 條碼新增至您的文件中，這是供應鏈和庫存管理的熱門選擇。
#### 步驟1：初始化簽名對象
建立一個實例 `Signature` 使用來源檔案路徑：
```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY"))
{
    // 代碼繼續...
}
```
#### 步驟 2：配置 GS1DotCode 選項
設定條碼選項，包括內容、格式和尺寸。
```csharp
var gs1DotCodeOptions = new BarcodeSignOptions(
    "(01)04912345123459(15)970331(30)128(10)ABC123", 
    BarcodeTypes.GS1DotCode)
{
    Left = 1,
    Top = 1,
    Height = 150,
    Width = 200,
    ReturnContent = true, // 檢索簽名影像的內容
    ReturnContentType = FileType.PNG // 輸出為 PNG
};
```
#### 步驟 3：簽署並儲存文檔
執行簽名流程，並將結果儲存到指定路徑。
```csharp
var signResult = signature.Sign("YOUR_OUTPUT_DIRECTORY/AdvancedBarCodeTypes.pptx", gs1DotCodeOptions);
```
### 使用漢信二維碼簽署文件
**概述**：在您的文件中嵌入漢信二維碼，廣泛用於安全資料共享。
#### 步驟1：初始化簽名對象
與條碼設定類似，初始化 `Signature`：
```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY"))
{
    // 代碼繼續...
}
```
#### 步驟2：設定漢信二維碼選項
使用內容和外觀設定定義您的二維碼選項。
```csharp
var hanXinOptions = new QrCodeSignOptions(
    "(01)04912345123459(15)970331(30)128(10)ABC123", 
    QrCodeTypes.HanXin)
{
    Left = 201,
    Top = 1,
    Height = 200,
    Width = 200,
    ReturnContent = true, // 檢索簽名影像的內容
    ReturnContentType = FileType.PNG // 輸出為 PNG
};
```
#### 步驟 3：簽署並儲存文檔
繼續簽署並儲存您的文件。
```csharp
var signResult = signature.Sign("YOUR_OUTPUT_DIRECTORY/AdvancedQRCodeTypes.pptx", hanXinOptions);
```
### 列出新建立的簽名
**概述**：透過列出簽名後的內容來驗證所新增的簽名。
#### 實施步驟：
1. **初始化簽名對象**：就像以前的功能一樣。
2. **列出並輸出簽名**：使用一種方法來遍歷已簽署的項目。
```csharp
void ListNewSignatures(SignResult signResult)
{
    Console.WriteLine("\nList of newly created signatures:");
    int number = 1;
    foreach (var item in signResult.Succeeded)
    {
        switch (item)
        {
            case BarcodeSignature barcodeSignature:
                string barOutputImagePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", $"image{number}{barcodeSignature.Format.Extension}");
                using (FileStream fs = new FileStream(barOutputImagePath, FileMode.Create))
                {
                    fs.Write(barcodeSignature.Content, 0, barcodeSignature.Content.Length);
                }
                number++;
                break;
            case QrCodeSignature qrCodeSignature:
                string qrOutputImagePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", $"image{number}{qrCodeSignature.Format.Extension}");
                using (FileStream fs = new FileStream(qrOutputImagePath, FileMode.Create))
                {
                    fs.Write(qrCodeSignature.Content, 0, qrCodeSignature.Content.Length);
                }
                number++;
                break;
        }
    }
}
```
## 實際應用
- **供應鏈管理**：使用 GS1DotCode 追蹤產品從製造到零售的整個過程。
- **安全資料共享**：實施漢信二維碼，實現商業文件中資訊的加密共享。
- **自動發票處理**：使用條碼簡化發票驗證和批准流程。
## 性能考慮
使用 GroupDocs.Signature 時，請考慮以下提示：
- **優化資源使用**：及時關閉流並釋放資源，避免記憶體洩漏。
- **平行處理**：盡可能使用非同步方法或並行處理以獲得更好的效能。
- **記憶體管理**：定期分析您的應用程式以確保有效使用.NET 的垃圾收集器。
## 結論
在本教學中，您學習如何使用 GroupDocs.Signature for .NET 實作 GS1DotCode 條碼和 HanXin 二維碼。這些工具可以顯著提高文件工作流程的安全性和效率。
### 後續步驟
- 試試 GroupDocs.Signature 提供的不同條碼類型。
- 探索與其他系統（如 CRM 或 ERP 解決方案）的整合。
準備好在您的應用程式中簽署文件了嗎？立即嘗試實現這些功能！
## 常見問題部分
1. **什麼是適用於 .NET 的 GroupDocs.Signature？**
   - 一個在 .NET 應用程式中啟用數位簽章功能的函式庫，支援各種文件格式和簽章類型。
2. **我可以將其他條碼格式與 GroupDocs.Signature 一起使用嗎？**
   - 是的，它支援多種條碼標準，包括二維碼、Code 128、PDF417 等。
3. **如何處理簽名過程中的錯誤？**
   - 實施異常處理 `Sign` 方法呼叫來優雅地管理潛在的錯誤。
4. **在大型文件中新增條碼會對效能產生影響嗎？**
   - 雖然添加條碼通常很有效，但效能會根據文件的大小和複雜性而有所不同。