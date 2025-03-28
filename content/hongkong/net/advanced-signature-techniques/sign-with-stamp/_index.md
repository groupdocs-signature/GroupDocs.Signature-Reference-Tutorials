---
title: 使用 GroupDocs.Signature 進行 Stamp 簽名
linktitle: 蓋章簽名
second_title: GroupDocs.Signature .NET API
description: 了解如何使用 GroupDocs.Signature for .NET 輕鬆將圖章簽章新增至 .NET 文件。增強文件安全性。
weight: 16
url: /zh-hant/net/advanced-signature-techniques/sign-with-stamp/
---

# 使用 GroupDocs.Signature 進行 Stamp 簽名

## 介紹
在本教學中，我們將引導您完成使用 GroupDocs.Signature for .NET 使用圖章簽署文件的流程。透過遵循這些逐步說明，您將能夠輕鬆地在文件中添加印章簽名。
## 先決條件
在我們開始之前，請確保您符合以下先決條件：
1.  GroupDocs.Signature for .NET SDK：從以下位置下載並安裝 SDK：[網站](https://releases.groupdocs.com/signature/net/).
2. 開發環境：確保您為 .NET 開發設定了合適的開發環境。
3. 要簽署的文件：準備您要蓋章簽名的文件（例如 PDF）。

## 導入命名空間
首先將必要的命名空間匯入到您的專案中：
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 第 1 步：載入文檔
```csharp
string filePath = "sample.pdf";
using (Signature signature = new Signature(filePath))
{
    //你的程式碼放在這裡
}
```
## 第 2 步：設定圖章標誌選項
```csharp
StampSignOptions options = new StampSignOptions()
{
    Left = 50,
    Top = 150,                    
    Width = 200,
    Height = 200
};
```
## 步驟 3：配置圖章外觀
```csharp
StampLine outerLine = new StampLine();
outerLine.Text = " * European Union ";
outerLine.TextRepeatType = StampTextRepeatType.FullTextRepeat;
outerLine.Font.Size = 12;
outerLine.Height = 22;
outerLine.TextBottomIntent = 6;
outerLine.TextColor = Color.WhiteSmoke;
outerLine.BackgroundColor = Color.DarkSlateBlue;
options.OuterLines.Add(outerLine);
StampLine innerLine = new StampLine();
innerLine.Text = "John Smith";
innerLine.TextColor = Color.MediumVioletRed;
innerLine.Font.Size = 20;
innerLine.Font.Bold = true;
innerLine.Height = 40;
options.InnerLines.Add(innerLine);
```
## 第 4 步：簽署文件
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithStamp", fileName);
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## 結論
使用 GroupDocs.Signature for .NET 將圖章簽章加入文件中是一個簡單的過程，如本教學所示。透過提供的步驟，您可以輕鬆增強文件的安全性和真實性。
## 常見問題解答
### 我可以自訂印章簽名的外觀嗎？
是的，您可以根據您的要求自訂印章簽名的文字、字體、顏色和位置等各個方面。
### GroupDocs.Signature 是否支援簽署多種文件格式？
是的，GroupDocs.Signature 支援多種文件格式，包括 PDF、Microsoft Word、Excel、PowerPoint 等。
### GroupDocs.Signature 是否有試用版？
是的，您可以從以下位置存取免費試用版：[網站](https://releases.groupdocs.com/).
### 我可以在單一文件中新增多個簽名嗎？
當然，GroupDocs.Signature 允許您在單一文件中添加多個簽名，包括圖章、文字、圖像和數位簽名。
### 如果在實施過程中遇到任何問題，我可以在哪裡尋求支援？
您可以從 GroupDocs.Signature 社群論壇找到支援和協助[這裡](https://forum.groupdocs.com/c/signature/13).