---
"description": "學習如何使用 GroupDocs.Signature for .NET 新增二維碼簽章來增強文件安全性。完整的程式碼範例，簡單易懂。"
"linktitle": "使用二維碼簽名"
"second_title": "GroupDocs.簽署 .NET API"
"title": "如何使用 GroupDocs.Signature 對二維碼文件進行簽名"
"url": "/zh-hant/net/advanced-signature-techniques/sign-with-qr-code/"
"weight": 15
---

# 使用 GroupDocs.Signature 將二維碼簽章新增至文檔

您是否想過如何為您的數位文件添加額外的安全保護和身份驗證？二維碼簽名或許正是您所需要的。在本指南中，我們將引導您完成使用 GroupDocs.Signature for .NET 實作二維碼簽章的整個過程。

## 為什麼要在文件中使用二維碼？

二維碼不僅適用於餐廳菜單和行銷材料。當整合到您的文件工作流程中時，它們可以：

- 提供文件真實性的即時驗證
- 儲存重要的元數據，而不會在視覺上擾亂您的文檔
- 實現快速存取相關數位資源
- 在您的實體和數位文件系統之間建立橋樑

讓我們深入了解如何在 .NET 應用程式中實現這項強大的功能！

## 開始之前你需要什麼

在我們進入程式碼之前，請確保一切準備就緒：

1. GroupDocs.Signature for .NET：您可以直接從 [GroupDocs 網站](https://releases。groupdocs.com/signature/net/).

2. .NET 開發環境：任何最新版本的 Visual Studio 都可以完美地滿足我們的目的。

3. 測試文件：取得您想要試驗的任何 PDF、Word 或其他受支援的文件。

一旦掌握了這些基本知識，您就可以開始實作二維碼簽名了！

## 使用正確的命名空間設定你的項目

首先，我們需要導入必要的命名空間來存取我們需要的所有功能：

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

這些命名空間將使我們能夠存取 GroupDocs.Signature 庫的核心功能，包括二維碼簽章的特定選項。

## 如何定義文檔路徑？

讓我們設定來源文件的文件路徑以及我們想要儲存簽名版本的位置：

```csharp
string filePath = "sample.pdf";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "SignWithQRCode", fileName);
```

記得更換 `"Your Document Directory"` 以及您想要儲存簽名文檔的實際路徑。良好的文件組織方式可以為您省去以後的麻煩！

## 建立您的簽名對象

現在我們將初始化一個 `Signature` 處理我們所有文件簽章需求的對象：

```csharp
using (Signature signature = new Signature(filePath))
{
    // 我們將在接下來的步驟中在此處添加我們的簽名代碼
}
```

該物件是我們想要修改的文檔的主要介面。 `using` 語句確保我們完成後所有資源都妥善處置。

## 如何配置二維碼簽名

這就是奇蹟發生的地方——我們將創建並自訂我們的二維碼簽名：

```csharp
QrCodeSignOptions options = new QrCodeSignOptions("JohnSmith")
{
    EncodeType = QrCodeTypes.QR,
    Left = 50,
    Top = 150,
    Width = 200,
    Height = 200
};
```

在此範例中，我們在二維碼中編碼了“JohnSmith”，但您可以添加任何文本，例如驗證 URL、數位簽章或文檔元資料。我們也將二維碼放置在頁面左側 50 像素、頂部 150 像素的位置，尺寸為 200x200 像素。

## 將二維碼套用到您的文檔

配置好選項後，應用程式簽名就非常簡單了：

```csharp
SignResult result = signature.Sign(outputFilePath, options);
```

這一行程式碼將二維碼套用到您的文檔，並將結果儲存到您指定的輸出路徑。 `SignResult` 物件向我們提供了有關該過程如何進行的資訊。

## 如何驗證一切正常

最後，讓我們加入一些回饋來確認我們的簽名過程是否成功：

```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

這將顯示一條有用的訊息，顯示新增了多少個簽名以及在哪裡可以找到新簽署的文件。

## QR碼簽名的實際應用

你可能想知道如何在你的特定情況下使用它。以下是一些實際應用：

- 法律文件：新增連結到驗證網站或包含加密驗證資料的二維碼
- 公司報告：包含連結到補充線上資源或更新資訊的二維碼
- 教育材料：嵌入連接到視訊教學或互動學習資源的二維碼
- 醫療文件：使用二維碼快速存取患者病史或藥物訊息

## 實作二維碼簽名後下一步是什麼？

現在您已經掌握了在文件中新增二維碼簽章的方法，您可能想要探索 GroupDocs.Signature 函式庫的其他功能，例如：

- 在單一文件中實作多種簽章類型
- 為大量文件簽章建立批次工作流程
- 發展驗證機制來驗證簽署的文件
- 探索更高級的二維碼選項，例如編碼元資料和自訂外觀

## 關於二維碼文件簽名的常見問題

### 我可以自訂文件中二維碼的外觀嗎？

當然！您可以完全控制二維碼的外觀。除了我們演示的位置和大小之外，您還可以調整顏色、添加邊框以及修改編碼類型，以滿足您的特定需求。

### 哪些文檔格式支援二維碼簽章？

GroupDocs.Signature for .NET 程式庫支援多種文件格式，包括：
- PDF 文件
- Microsoft Word 文件（.docx、.doc）
- Excel 試算表
- PowerPoint 簡報
- 以及更多

### 有沒有辦法批次處理多個文件？

是的！ GroupDocs.Signature 可以輕鬆實現批次處理。您可以建立一個簡單的循環，或者使用更高級的並行處理來有效地簽署多個文檔，這非常適合高容量場景。

### 如何驗證二維碼簽名是否為真？

GroupDocs.Signature 提供全面的驗證機制，讓您可以檢查二維碼簽署文件的完整性和真實性。這可確保您的文件在簽名後未被竄改。

### 我可以在購買之前嘗試此功能嗎？

當然！ GroupDocs 提供免費試用版，您可以從他們的 [網站](https://releases.groupdocs.com/)。這可讓您在做出承諾之前全面評估所有功能並確保它們滿足您的要求。