---
title: 使用元資料對影像進行簽名
linktitle: 使用元資料對影像進行簽名
second_title: GroupDocs.Signature .NET API
description: 了解如何使用 GroupDocs.Signature 在 .NET 中使用元資料對影像進行簽署。簡單、高效且可自訂的元資料簽章解決方案。
weight: 10
url: /zh-hant/net/document-signing/sign-image-with-metadata/
---
## 介紹
GroupDocs.Signature for .NET 讓開發人員能夠有效地使用元資料對影像進行簽署。本教學將引導您逐步完成流程。
## 先決條件
在開始之前，請確保您具備以下條件：
1. 適用於 .NET 的 GroupDocs.Signature：在 .NET 專案中安裝 GroupDocs.Signature 套件。您可以從以下位置下載：[這裡](https://releases.groupdocs.com/signature/net/).   
2. 影像檔案：準備要使用元資料簽署的影像檔案。

## 導入命名空間
確保在 C# 程式碼中導入必要的命名空間：
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 第 1 步：載入圖片文件
首先，指定影像檔案的路徑以及帶有元資料的簽名影像的輸出目錄：
```csharp
string filePath = "sample.png";            
string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
```
## 第 2 步：建立元資料簽名
接下來，建立不同的元資料簽章並將它們新增至選項簽章集合：
```csharp
using (Signature signature = new Signature(filePath))
{
    ushort imgsMetadataId = 41996;
    MetadataSignOptions options = new MetadataSignOptions();
    options
        .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Scherlock Holmes")) //字串值
        .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          //日期時間值
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                //整數值
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              //雙倍價值
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              //十進制值
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             //浮動值
    
    //簽署文件歸檔
    SignResult result = signature.Sign(outputFilePath, options);
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## 結論
在本教學中，您學習如何使用 GroupDocs.Signature for .NET 使用元資料對影像進行簽署。透過執行這些步驟，您可以輕鬆地將元資料簽章合併到您的 .NET 應用程式中。

## 常見問題解答
### 我可以使用 GroupDocs.Signature for .NET 使用元資料簽署多個映像嗎？
是的，您可以透過迭代每個影像檔案並應用元資料簽名來使用元資料對多個影像進行簽名。
### 是否有適用於 .NET 的 GroupDocs.Signature 試用版？
是的，您可以從以下位置下載試用版[這裡](https://releases.groupdocs.com/).
### GroupDocs.Signature for .NET 是否支援圖像以外的其他檔案格式？
是的，GroupDocs.Signature 支援各種文件格式，包括 PDF、Word、Excel 等。
### 我可以自訂元資料簽章的外觀嗎？
是的，您可以自訂元資料簽名的外觀，例如字體大小、顏色和位置。
### 在哪裡可以獲得對 .NET 的 GroupDocs.Signature 的支援？
您可以從 GroupDocs.Signature 論壇獲得支持[這裡](https://forum.groupdocs.com/c/signature/13).