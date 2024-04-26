---
title: 使用 GroupDocs.Signature 透過 QR 碼簽署文檔
linktitle: 使用二維碼簽名
second_title: GroupDocs.Signature .NET API
description: 了解如何使用 GroupDocs.Signature for .NET 將 QR 程式碼簽章新增至文件。輕鬆增強安全性和身份驗證。
type: docs
weight: 15
url: /zh-hant/net/advanced-signature-techniques/sign-with-qr-code/
---
## 介紹
在本教學中，我們將演練使用 GroupDocs.Signature for .NET 透過 QR 程式碼簽署文件的流程。 GroupDocs.Signature for .NET 是一個功能強大的 API，可讓開發人員以程式設計方式為數位文件添加各種類型的簽章。使用二維碼簽署文件可以為您的文件提供額外的安全性和驗證層。
## 先決條件
在開始之前，請確保您已安裝以下先決條件：
1.  GroupDocs.Signature for .NET：您可以從以下位置下載該程式庫：[網站](https://releases.groupdocs.com/signature/net/).
2. 開發環境：確保您的電腦上設定了 .NET 開發環境。
3. 範例文件：準備要使用 QR 碼簽署的範例文件（例如 PDF）。

## 導入必要的命名空間
在深入研究程式碼之前，讓我們先導入必要的名稱空間：
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## 第 1 步：定義檔路徑
```csharp
string filePath = "sample.pdf";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "SignWithQRCode", fileName);
```
確保更換`"Your Document Directory"`以及要儲存簽名文檔的目錄路徑。
## 步驟2：初始化簽名對象
```csharp
using (Signature signature = new Signature(filePath))
{
    //簽名代碼位於此處
}
```
初始化一個`Signature`物件包含您要簽署的文件的路徑。
## 步驟3：建立QRCodeSignOptions
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
創建一個`QrCodeSignOptions`具有 QR 碼簽名所需設定的物件。您可以自訂參數，例如要編碼的文字、QR 碼的位置和尺寸。
## 第 4 步：簽署文件
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
使用`Sign`的方法`Signature`物件使用指定選項簽署文件。該方法傳回一個`SignResult`包含有關簽名過程的資訊的物件。
## 第5步：顯示結果
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
顯示一則訊息，指示簽名過程成功以及簽署文件的儲存位置。

## 結論
在本教學中，我們學習如何使用 GroupDocs.Signature for .NET 透過 QR 碼簽署文件。透過執行這些簡單的步驟，您可以將 QR 碼簽章新增至您的數位文件中，從而增強安全性和身分驗證。

## 常見問題解答
### 我可以自訂二維碼的外觀嗎？
是的，您可以根據您的需求自訂二維碼的大小、位置、編碼類型等各種參數。
### 二維碼簽名支援哪些文檔格式？
GroupDocs.Signature for .NET 支援多種文件格式，包括 PDF、Word、Excel、PowerPoint 等。
### 是否可以批次簽署多個文件？
當然，您可以使用 GroupDocs.Signature for .NET 同時簽署多個文檔，從而簡化您的工作流程。
### 我可以驗證使用二維碼簽署的檔案的真實性嗎？
是的，GroupDocs.Signature for .NET 提供驗證機制來確保簽署文件的完整性和真實性。
### 購買前是否有試用版測試功能？
是的，您可以從以下位置下載免費試用版[網站](https://releases.groupdocs.com/)評估 GroupDocs.Signature for .NET 的特性和功能。