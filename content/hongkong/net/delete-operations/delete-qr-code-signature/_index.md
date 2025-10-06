---
"description": "透過我們的逐步開發人員指南，了解如何使用 GroupDocs.Signature for .NET 輕鬆地從文件中刪除二維碼簽章。"
"linktitle": "從文件中刪除二維碼簽名"
"second_title": "GroupDocs.簽署 .NET API"
"title": "如何從 .NET 文件中刪除二維碼簽名"
"url": "/zh-hant/net/delete-operations/delete-qr-code-signature/"
"weight": 16
type: docs
---
# 如何從文件中刪除二維碼簽名

## 介紹

您是否曾經需要透過程式設計方式從文件中刪除二維碼簽名？無論您是清理過期訊息，還是準備重新分發文檔，有效地管理文檔簽名對於 .NET 開發人員來說都是一項至關重要的技能。

在本指南中，我們將詳細指導您如何使用 GroupDocs.Signature for .NET 從文件中刪除二維碼簽章。這個強大的庫使簽名管理變得簡單易行，讓您可以專注於構建出色的應用程序，而無需費力應對文檔操作的挑戰。

## 開始之前你需要什麼

在深入研究程式碼之前，請確保一切準備就緒：

- GroupDocs.Signature for .NET：您需要在專案中安裝該程式庫。您可以直接從 [GroupDocs 發布頁面](https://releases。groupdocs.com/signature/net/).
- 帶有二維碼的文檔：為了練習，準備一份包含至少一個您想要刪除的二維碼簽名的文檔。
- 基本 C# 知識：您應該熟悉 C# 基礎知識，以便能夠遵循我們的範例。

一旦滿足了這些先決條件，您就可以開始刪除這些二維碼了！

## 使用正確的命名空間設定你的項目

首先，讓我們導入必要的命名空間，以使我們的程式碼順利運行：

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

這些導入使我們能夠存取 GroupDocs.Signature 庫中所需的所有功能，以及一些用於檔案處理的基本 .NET 類別。

## 步驟1：你的文件在哪裡？設定文檔路徑

讓我們先定義文件的位置以及我們想要儲存修改版本的位置：

```csharp
// 文檔目錄的路徑。
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);

// 定義修改後的文件的輸出文件路徑。
string outputFilePath = Path.Combine("Your Document Directory", "DeleteQRCode", fileName);

// 複製來源文件，因為 Delete 方法適用於同一個 Document。
File.Copy(filePath, outputFilePath, true);
```

請注意，我們正在建立原始文件的副本。這一點很重要，因為簽名刪除過程會直接修改文件，而我們始終希望保留原始文件。

## 步驟 2：建立要使用的簽章對象

現在我們將建立一個連接到我們文件的簽署物件：

```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // 建立搜尋二維碼簽名的選項。
    QrCodeSearchOptions options = new QrCodeSearchOptions();
    
    // 在文件中搜尋二維碼簽名。
    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```

這段程式碼使用我們的文件初始化 Signature 對象，然後搜尋其中存在的任何二維碼簽名。搜尋將傳回找到的所有二維碼簽署的清單。

## 步驟 3：是否有需要刪除的二維碼？

在嘗試刪除任何內容之前，我們應該檢查是否有二維碼：

```csharp
    if (signatures.Count > 0)
    {
        // 取得文件中找到的第一個二維碼簽章。
        QrCodeSignature qrCodeSignature = signatures[0];
```

這個簡單的檢查確保只有在文件中至少有一個二維碼簽名時，我們才能繼續執行。在本例中，我們的目標是找到的第一個二維碼，但您可以根據需要輕鬆修改它以處理多個簽名。

## 步驟4：從文件中刪除二維碼

現在進入正題－刪除二維碼：

```csharp
        // 從文件中刪除二維碼簽名。
        bool result = signature.Delete(qrCodeSignature);
        
        if (result)
        {
            Console.WriteLine($"Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
        }
        else
        {
            Console.WriteLine($"Signature was not deleted from the document! Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was not found!");
        }
    }
}
```

程式碼會刪除簽名並提供操作是否成功的回饋。此回饋對於調試和確認程式碼是否按預期工作至關重要。

## 我們取得了什麼成就？

恭喜！您剛剛學習如何使用 GroupDocs.Signature for .NET 從文件中刪除二維碼簽章。這項技能將為您的應用程式中的文件管理帶來無限可能。

只需幾行程式碼，您現在就可以以程式設計方式清理文檔，刪除過時或不必要的二維碼簽名，確保您的文檔始終只包含相關資訊。

## 您可能遇到的常見問題

### 我可以一次刪除多個二維碼嗎？

當然！除了刪除找到的第一個簽名之外，您還可以遍歷整個簽名列表，然後刪除每個簽名，如下所示：

```csharp
foreach(var qrSignature in signatures)
{
    signature.Delete(qrSignature);
}
```

### 我可以使用 GroupDocs.Signature 管理哪些其他類型的簽章？

GroupDocs.Signature 功能極為豐富，支援各種簽章類型，包括：
- 文字簽名
- 影像簽名
- 條碼簽名
- 數位簽名
- 還有更多！

### 這適用於我所有的文檔格式嗎？

您會很高興地知道 GroupDocs.Signature 適用於多種文件格式，包括：
- PDF 文件
- Microsoft Word 文件
- Excel 試算表
- PowerPoint 簡報
- 以及其他許多人

### 我可以搜尋特定的二維碼而不是刪除所有二維碼嗎？

是的！ `QrCodeSearchOptions` 該類別提供各種屬性來過濾搜尋結果。例如，您可以搜尋包含特定文字或以特定格式編碼的二維碼。

### 有沒有辦法在購買前試用 GroupDocs.Signature？

是的，您可以從下載免費試用版 [GroupDocs 網站](https://releases.groupdocs.com/) 在做出承諾之前，先用你的具體用例來測試它。