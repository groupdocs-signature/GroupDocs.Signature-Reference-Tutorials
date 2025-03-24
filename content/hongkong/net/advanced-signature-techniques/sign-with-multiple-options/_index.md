---
title: 使用多個選項進行簽名
linktitle: 使用多個選項進行簽名
second_title: GroupDocs.Signature .NET API
description: 了解如何使用 GroupDocs.Signature for .NET 透過多個選項簽署文件。透過文字、條碼、QR 碼、數位和影像增強文件安全性。
weight: 14
url: /zh-hant/net/advanced-signature-techniques/sign-with-multiple-options/
---

# 使用多個選項進行簽名

## 介紹
在本教學中，我們將探討如何使用 .NET 的 GroupDocs.Signature 函式庫使用多個簽章選項來簽署文件。使用文字、條碼、二維碼、數位、圖像和元資料簽名等各種選項對文件進行簽名可以提供多功能性並增強文件安全性。
## 先決條件
在開始之前，請確保您具備以下先決條件：
1.  GroupDocs.Signature for .NET 函式庫：從下列位置下載並安裝 GroupDocs.Signature for .NET 函式庫[這裡](https://releases.groupdocs.com/signature/net/).
2. 開發環境：建置開發環境，安裝.NET Framework。
3. 要簽署的文件：準備您要簽署的文件（例如，sample.docx）。
4. 證書和圖像：準備數位和圖像簽名所需的任何證書和圖像。

## 導入命名空間
首先，匯入必要的命名空間以在 .NET 應用程式中使用 GroupDocs.Signature 庫：
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 第 1 步：載入文檔
```csharp
string filePath = "sample.docx";
string outputFilePath = Path.Combine("Your Document Directory", "SignWithMultiple", "SignWithMultiple.docx");
using (Signature signature = new Signature(filePath))
{
    //您的程式碼繼續...
}
```
## 第 2 步：定義簽章選項
定義多個不同類型和設定的簽章選項，例如文字、條碼、QR 碼、數位、影像和元資料簽章：
```csharp
TextSignOptions textOptions = new TextSignOptions("Text signature")
{
    VerticalAlignment = VerticalAlignment.Top,
    HorizontalAlignment = HorizontalAlignment.Left
};
BarcodeSignOptions barcodeOptions = new BarcodeSignOptions("123456")
{
    EncodeType = BarcodeTypes.Code128,
    Left = 0,
    Top = 150,
    Height = 50,
    Width = 200
};
//定義其他簽章選項（例如，QR 碼、數位、影像、元資料）...
```
## 第 3 步：建立簽名選項列表
定義包含所有先前定義的選項的簽名選項清單：
```csharp
List<SignOptions> listOptions = new List<SignOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
//將其他簽名選項新增至清單...
```
## 第 4 步：簽署文件
使用簽名選項清單對文件進行簽名並保存簽署的文件：
```csharp
SignResult result = signature.Sign(outputFilePath, listOptions);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## 結論
使用 GroupDocs.Signature for .NET 使用多個選項對文件進行簽名，為增強文件安全性和多功能性提供了強大的解決方案。透過遵循本教學中概述的步驟，您可以將各種簽章類型無縫整合到您的 .NET 應用程式中。
## 常見問題解答
### 我可以使用自訂影像進行數位簽名嗎？
是的，您可以使用 GroupDocs.Signature 庫為數位簽章指定自訂影像。
### GroupDocs.Signature 是否與不同的文件格式相容？
是的，GroupDocs.Signature 支援各種文件格式，包括 DOCX、PDF、PPTX 等。
### 我可以自訂文字簽名的外觀嗎？
當然，您可以自訂文字簽名的外觀，包括字體大小、顏色和樣式。
### GroupDocs.Signature 是否提供數位簽章加密？
是的，GroupDocs.Signature 提供數位簽章加密選項，以確保文件安全。
### 是否有適用於 .NET 的 GroupDocs.Signature 試用版？
是的，您可以從以下位置下載 GroupDocs.Signature for .NET 的免費試用版：[這裡](https://releases.groupdocs.com/).