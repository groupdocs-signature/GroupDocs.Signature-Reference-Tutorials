---
title: 從文件中刪除二維碼簽名
linktitle: 從文件中刪除二維碼簽名
second_title: GroupDocs.Signature .NET API
description: 了解如何使用 GroupDocs.Signature for .NET 從文件中刪除 QR 程式碼簽署。請按照我們的逐步指南進行高效率的簽名管理。
type: docs
weight: 16
url: /zh-hant/net/delete-operations/delete-qr-code-signature/
---
## 介紹
在本教學中，我們將引導您完成使用 GroupDocs.Signature for .NET 從文件中刪除 QR 程式碼簽署的過程。請按照這些逐步說明有效刪除 QR 碼簽名。
## 先決條件
在開始之前，請確保您具備以下先決條件：
- 適用於 .NET 的 GroupDocs.Signature：請確保您的 .NET 專案中安裝了 GroupDocs.Signature 程式庫。您可以從以下位置下載：[這裡](https://releases.groupdocs.com/signature/net/).
- 帶有二維碼簽名的文件：準備包含要刪除的二維碼簽名的文件。
- C# 基礎知識：熟悉 C# 程式語言基礎。

## 導入命名空間
在深入研究程式碼之前，將必要的命名空間匯入到您的 C# 檔案中：
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 第 1 步：定義檔路徑
```csharp
//文檔目錄的路徑。
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
//定義修改後的文件的輸出文件路徑。
string outputFilePath = Path.Combine("Your Document Directory", "DeleteQRCode", fileName);
//複製來源文件，因為刪除方法適用於同一文檔。
File.Copy(filePath, outputFilePath, true);
```
## 步驟2：初始化簽名對象
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    //建立用於搜尋 QR 碼簽名的選項。
    QrCodeSearchOptions options = new QrCodeSearchOptions();
    //在文件中搜尋二維碼簽名。
    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```
## 步驟 3：檢查二維碼簽名是否存在
```csharp
    if (signatures.Count > 0)
    {
        //取得文件中找到的第一個二維碼簽章。
        QrCodeSignature qrCodeSignature = signatures[0];
```
## 第四步：刪除二維碼簽名
```csharp
        //從文件中刪除 QR 碼簽章。
        bool result = signature.Delete(qrCodeSignature);
        if (result)
        {
            Console.WriteLine($"Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
        }
        else
        {
            Helper.WriteError($"Signature was not deleted from the document! Signature with Barcode '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was not found!");
        }
    }
}
```
恭喜！您已使用 GroupDocs.Signature for .NET 成功從文件中刪除了 QR 程式碼簽章。

## 結論
在本教學中，我們學習如何使用 GroupDocs.Signature for .NET 從文件中刪除 QR 碼簽章。透過遵循提供的步驟，您可以有效地管理和操作 .NET 應用程式中的簽章。
## 常見問題解答
### 我可以從文件中刪除多個二維碼簽名嗎？
是的，您可以修改程式碼以迭代所有二維碼簽名並相應地刪除它們。
### GroupDocs.Signature是否支援二維碼以外的其他類型簽章？
是的，GroupDocs.Signature 支援各種簽章類型，例如文字、圖像、條碼等。
### GroupDocs.Signature 是否與所有文件格式相容？
GroupDocs.Signature 支援多種文件格式，包括 PDF、Microsoft Word、Excel、PowerPoint 等。
### 我可以自訂簽名的搜尋選項嗎？
是的，您可以根據您的要求自訂搜尋選項，以查找文件中的特定簽名。
### GroupDocs.Signature 是否有試用版？
是的，您可以存取 GroupDocs.Signature 的免費試用版：[這裡](https://releases.groupdocs.com/).