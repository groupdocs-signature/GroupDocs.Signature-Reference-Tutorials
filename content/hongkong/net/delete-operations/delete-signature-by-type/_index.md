---
title: 按類型刪除簽名
linktitle: 按類型刪除簽名
second_title: GroupDocs.Signature .NET API
description: 了解如何使用 GroupDocs.Signature 輕鬆刪除 .NET 文件中的類型簽名，從而提高文件管理效率。
weight: 12
url: /zh-hant/net/delete-operations/delete-signature-by-type/
---
## 介紹
在當今的數位時代，高效能文件管理的需求至關重要。無論您是處理合約的商業專業人士還是處理法律文件的個人，確保文件的真實性和完整性都至關重要。 GroupDocs.Signature for .NET 提供了一個強大的解決方案來無縫管理文件中的簽章。在本教程中，我們將深入研究使用 GroupDocs.Signature for .NET 按類型刪除簽署的流程，為您提供簡化文件管理任務的逐步指南。
## 先決條件
在我們開始之前，請確保您具備以下先決條件：
- C# 程式語言的基礎知識。
-  GroupDocs.Signature for .NET 安裝在您的開發環境中。您可以從以下位置下載：[這裡](https://releases.groupdocs.com/signature/net/).
- 系統上安裝了整合開發環境 (IDE)，例如 Visual Studio。
- 包含用於演示目的的簽名的範例文件。
## 導入命名空間
首先，請確保將必要的命名空間匯入到您的專案中。這使您可以輕鬆存取 GroupDocs.Signature for .NET 提供的功能。
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```
## 第 1 步：定義檔路徑
首先定義輸入文件的路徑和儲存修改後的文件的輸出目錄。
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteBySignatureType", fileName);
```
確保更換`"Your Document Directory"`與儲存文件的實際目錄路徑。
## 步驟2：複製來源文件
自從`Delete`方法適用於同一文檔，建議複製來源文件以保留原始文件。
```csharp
File.Copy(filePath, outputFilePath, true);
```
此步驟可確保對文件所做的任何修改不會影響原始文件。
## 步驟 3：刪除簽名
現在，初始化一個`Signature`物件與輸出檔案路徑並繼續按類型刪除簽名。
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    DeleteResult result = signature.Delete(SignatureType.QrCode);
```
在這裡，我們從文件中刪除二維碼簽名。您可以更換`SignatureType.QrCode`根據您的要求使用所需的簽名類型。
## 步驟4：處理刪除結果
刪除後，查看結果判斷操作成功，並顯示相關資訊。
```csharp
if (result.Succeeded.Count > 0)
{
    Console.WriteLine("Following QR-Code signatures were deleted:");
    int number = 1;
    foreach (QrCodeSignature temp in result.Succeeded)
    {
        Console.WriteLine($"Signature #{number++}: Type: {temp.SignatureType} Id:{temp.SignatureId}, Text: {temp.Text}");
    }
}
else
{
    Helper.WriteError("No QR-Code signature was deleted.");
}
```
此步驟透過提供有關已刪除簽署的回饋來確保透明度。

## 結論
總之，使用 GroupDocs.Signature for .NET 簡化了文件中簽章的管理。透過遵循本教學中概述的步驟，您可以輕鬆地按類型刪除簽名，從而提高文件管理工作流程的效率。
## 常見問題解答
### 我可以一次刪除多種類型的簽名嗎？
是的，您可以透過迭代每種類型並相應地執行刪除過程來刪除多種類型的簽名。
### GroupDocs.Signature for .NET 是否與各種文件格式相容？
絕對地！ GroupDocs.Signature for .NET 支援多種文件格式，包括 PDF、Word、Excel、PowerPoint 等。
### 我可以根據特定標準自訂刪除流程嗎？
當然！ GroupDocs.Signature for .NET 提供了豐富的選項，可根據各種參數（例如簽章類型、文字內容、位置等）自訂簽章刪除。
### 購買前是否有試用版可供測試？
是的，您可以透過下載免費試用版來探索 GroupDocs.Signature for .NET 的功能[這裡](https://releases.groupdocs.com/).
### 我可以在哪裡尋求有關 GroupDocs.Signature for .NET 的協助或支援？
如有任何疑問或協助，您可以造訪 GroupDocs.Signature 論壇[這裡](https://forum.groupdocs.com/c/signature/13).