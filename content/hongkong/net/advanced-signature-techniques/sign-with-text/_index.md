---
title: 使用 GroupDocs.Signature for .NET 進行文字簽名
linktitle: 用文字簽名
second_title: GroupDocs.Signature .NET API
description: 了解如何使用 GroupDocs.Signature for .NET 對帶有文字的文件進行簽署。以程式設計方式新增文字簽名的逐步指南。
type: docs
weight: 17
url: /zh-hant/net/advanced-signature-techniques/sign-with-text/
---
## 介紹
在數位時代，電子簽名文件已成為一種標準做法，節省了時間和資源。 GroupDocs.Signature for .NET 提供了一個全面的解決方案，以程式設計方式將文字簽章新增至各種文件格式。在本教學中，我們將引導您完成使用 GroupDocs.Signature for .NET 對文字文件進行簽署的過程。
## 先決條件
在我們深入學習本教程之前，請確保您具備以下先決條件：
1.  GroupDocs.Signature for .NET：確保您已安裝 GroupDocs.Signature for .NET 程式庫。您可以從以下位置下載：[這裡](https://releases.groupdocs.com/signature/net/).
2. 開發環境：為.NET 開發設定工作環境。
3. 文件：準備要使用文字簽名的文件（例如 PDF、Word）。

## 導入命名空間
首先，您需要將必要的命名空間匯入到 .NET 專案中才能使用 GroupDocs.Signature 功能。
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

讓我們將使用文字簽署文件的過程分解為多個步驟：
## 第 1 步：載入文檔
載入您要使用文字簽名的文檔。
```csharp
string filePath = "sample.pdf"; //文件的路徑
string fileName = Path.GetFileName(filePath);
```
## 第2步：設定輸出檔路徑
定義儲存簽名文件的輸出檔路徑。
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithText", fileName);
```
## 第 3 步：建立簽名選項
設定文字簽名的選項，包括文字內容、位置、大小、顏色和字體。
```csharp
TextSignOptions options = new TextSignOptions("John Smith")
{
    Left = 50, //設定簽名位置
    Top = 200,
    Width = 100, //設定簽名矩形
    Height = 30,
    ForeColor = Color.Red, //設定文字顏色
    Font = new SignatureFont { Size = 14, FamilyName = "Comic Sans MS" } //設定字體
};
```
## 第 4 步：簽署文件
使用 GroupDocs.Signature 使用指定選項對文件進行簽名，並將簽署的文件儲存到輸出檔案路徑。
```csharp
using (Signature signature = new Signature(filePath))
{
    SignResult result = signature.Sign(outputFilePath, options); //簽署文件
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## 結論
在本教學中，我們學習如何使用 GroupDocs.Signature for .NET 對包含文字的文件進行簽署。透過執行這些步驟，您可以以程式設計方式有效地將文字簽章新增至文件中，從而增強安全性和真實性。
## 常見問題解答
### 我可以自訂文字簽名的外觀嗎？
是的，您可以根據您的喜好自訂文字簽署的顏色、字體、大小和位置等各種參數。
### GroupDocs.Signature 是否與多種文件格式相容？
是的，GroupDocs.Signature 支援各種文件格式，包括 PDF、Word、Excel、PowerPoint 等。
### 我可以在單一文件中新增多個文字簽名嗎？
當然，您可以為文件添加多個文字簽名，每個簽名都有自己的一組自訂選項。
### GroupDocs.Signature 是否確保簽署後文件的完整性？
是的，GroupDocs.Signature 採用強大的加密演算法來確保文檔完整性並防止簽名後被篡改。
### 購買前是否有試用版可供測試？
是的，您可以從以下位置下載免費試用版[這裡](https://releases.groupdocs.com/)在購買前探索功能。