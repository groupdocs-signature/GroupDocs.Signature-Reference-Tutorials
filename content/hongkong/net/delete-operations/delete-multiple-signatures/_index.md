---
title: 從文件中刪除多個簽名
linktitle: 從文件中刪除多個簽名
second_title: GroupDocs.Signature .NET API
description: 使用 GroupDocs.Signature for .NET 輕鬆刪除文件中的多個簽章。簡化您的文件管理工作流程。
weight: 15
url: /zh-hant/net/delete-operations/delete-multiple-signatures/
---
## 介紹
在數位世界中，文件管理通常涉及處理各種簽名。以程式設計方式從文件中刪除多個簽名可以簡化工作流程並提高效率。透過 GroupDocs.Signature for .NET，此任務變得無縫且簡單。本教學將引導您逐步完成從文件中刪除多個簽名的過程。
## 先決條件
在深入學習本教程之前，請確保您具備以下先決條件：
- 對 C# 程式語言有基本了解。
- 為 .NET 程式庫安裝了 GroupDocs.Signature。
- 用於測試的具有多個簽名的範例文件。

## 導入命名空間
首先匯入必要的命名空間以存取 GroupDocs.Signature for .NET 的功能：
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 第 1 步：定義文件路徑和文件名
設定包含多個簽署的文件的文件路徑。確保您具有適當的檔案路徑和檔案名稱：
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
```
## 第 2 步：複製文件進行處理
為了避免修改原始文檔，請建立副本進行處理：
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "DeleteMultiple", fileName);
File.Copy(filePath, outputFilePath, true);
```
## 第三步：初始化簽名對象
使用輸出檔案路徑實例化 Signature 物件：
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    //簽名處理程式碼放在這裡
}
```
## 第 4 步：定義搜尋選項
定義各種搜尋選項來識別文件中的簽名。選項包括文字搜尋、圖像搜尋、條碼搜尋和二維碼搜尋：
```csharp
TextSearchOptions textSearchOptions = new TextSearchOptions();
ImageSearchOptions imageSearchOptions = new ImageSearchOptions();
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions();
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions();
//將選項新增至列表
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textSearchOptions);
listOptions.Add(imageSearchOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
```
## 第 5 步：搜尋簽名
執行搜尋操作，根據定義的搜尋選項尋找文件中的所有簽名：
```csharp
SearchResult result = signature.Search(listOptions);
```
## 步驟6：刪除簽名
如果找到簽名，請繼續刪除它們：
```csharp
if (result.Signatures.Count > 0)
{
    //嘗試刪除所有簽名
    DeleteResult deleteResult = signature.Delete(result.Signatures);
    //檢查是否刪除成功
    if(deleteResult.Succeeded.Count == result.Signatures.Count)
    {
        Console.WriteLine("\nAll signatures were successfully deleted!");                        
    }
    else
    {
        Console.WriteLine($"Successfully deleted signatures : {deleteResult.Succeeded.Count}");
        Helper.WriteError($"Not deleted signatures : {deleteResult.Failed.Count}");
    }
    //顯示有關已刪除已簽署的信息
    Console.WriteLine("\nList of deleted signatures:");
    int number = 1;
    foreach(BaseSignature temp in deleteResult.Succeeded)
    {
        Console.WriteLine($"Signature #{number++}: Type: {temp.SignatureType} Id:{temp.SignatureId}, Location: {temp.Left}x{temp.Top}. Size: {temp.Width}x{temp.Height}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## 結論
以程式設計方式從文件中刪除多個簽章是文件管理中的關鍵任務。透過 GroupDocs.Signature for .NET，此流程變得有效率且可靠。透過遵循本教學中概述的步驟，您可以輕鬆地將簽章刪除功能整合到您的 .NET 應用程式中。
## 常見問題解答
### GroupDocs.Signature for .NET 可以處理各種文件格式嗎？
是的，GroupDocs.Signature for .NET 支援多種文件格式，包括 DOCX、PDF、PPTX、XLSX 等。
### 是否可以自訂簽名檢測的搜尋選項？
當然，您可以定製文字搜尋、圖像搜尋、條碼搜尋和二維碼搜尋等搜尋選項來滿足您的特定要求。
### GroupDocs.Signature for .NET 是否提供錯誤處理機制？
是的，該程式庫提供強大的錯誤處理功能，以確保文件處理任務的順利執行。
### 我可以將 GroupDocs.Signature for .NET 與其他第三方程式庫整合嗎？
當然，GroupDocs.Signature for .NET 旨在與其他 .NET 程式庫無縫集成，提供靈活性和可擴展性。
### 在哪裡可以找到針對 .NET 的 GroupDocs.Signature 的其他支援和資源？
您可以存取 GroupDocs[論壇](https://forum.groupdocs.com/c/signature/13)致力於簽署相關的討論並尋求社群和專家的協助。