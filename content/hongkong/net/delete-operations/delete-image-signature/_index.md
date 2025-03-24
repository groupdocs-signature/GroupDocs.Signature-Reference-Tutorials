---
title: 刪除影像簽名
linktitle: 刪除影像簽名
second_title: GroupDocs.Signature .NET API
description: 了解如何使用 GroupDocs.Signature for .NET 從文件中刪除映像簽章。請按照我們的逐步指南進行高效率的簽名管理。
weight: 14
url: /zh-hant/net/delete-operations/delete-image-signature/
---
## 介紹
在本教學中，我們將探討如何使用 GroupDocs.Signature for .NET 從文件中刪除影像簽章。 GroupDocs.Signature 是一個功能強大的程式庫，可讓開發人員使用各種文件格式中的數位簽章、圖章和表單欄位。
## 先決條件
在我們開始之前，請確保您具備以下條件：
### 1..NET 的 GroupDocs.Signature
從下列位置下載並安裝 GroupDocs.Signature for .NET[網站](https://releases.groupdocs.com/signature/net/)。請按照文件中提供的安裝說明進行操作。
### 2..NET框架
確保您的電腦上安裝了 .NET Framework。
## 導入命名空間
在您的專案中包含必要的命名空間：
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
讓我們將刪除影像簽名的過程分解為多個步驟：
## 第 1 步：定義檔路徑
首先指定刪除簽章後輸入文件和輸出文件的路徑：
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteImage", fileName);
```
## 步驟2：複製來源文件
自從`Delete`方法適用於同一文檔，必須將來源文件複製到另一個位置：
```csharp
File.Copy(filePath, outputFilePath, true);
```
## 第三步：初始化簽名對象
建立一個實例`Signature`類別並指定輸出文檔的路徑：
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    //代碼放在這裡
}
```
## 第 4 步：搜尋圖片簽名
定義搜尋選項並在文件中搜尋影像簽名：
```csharp
ImageSearchOptions options = new ImageSearchOptions();
List<ImageSignature> signatures = signature.Search<ImageSignature>(options);
```
## 步驟5：刪除影像簽名
如果找到圖片簽名，則刪除第一個：
```csharp
if (signatures.Count > 0)
{
    ImageSignature imageSignature = signatures[0];
    bool result = signature.Delete(imageSignature);
    if (result)
    {
        Console.WriteLine($"Image signature at location {imageSignature.Left}x{imageSignature.Top} and Size {imageSignature.Size} was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature at location {imageSignature.Left}x{imageSignature.Top} and Size {imageSignature.Size} was not found!");
    }
}
```
## 結論
在本教學中，我們學習如何使用 GroupDocs.Signature for .NET 從文件中刪除影像簽章。透過遵循逐步指南，開發人員可以有效地管理其應用程式中的數位簽章。
## 常見問題解答
### 我可以從文件中刪除多個圖像簽名嗎？
是的，您可以修改程式碼以透過迭代來刪除多個圖像簽名`signatures`列表。
### GroupDocs.Signature 是否支援 DOCX 之外的其他文件格式？
是的，GroupDocs.Signature 支援多種文件格式，包括 PDF、PPT、XLS 等。
### 是否有適用於 .NET 的 GroupDocs.Signature 試用版？
是的，您可以從以下位置下載免費試用版[網站](https://releases.groupdocs.com/).
### 我如何獲得對 GroupDocs.Signature 的支援？
您可以訪問[GroupDocs.Signature 論壇](https://forum.groupdocs.com/c/signature/13)尋求幫助和支持。
### 我可以購買 GroupDocs.Signature 的臨時授權嗎？
是的，您可以從[購買頁面](https://purchase.groupdocs.com/temporary-license/).