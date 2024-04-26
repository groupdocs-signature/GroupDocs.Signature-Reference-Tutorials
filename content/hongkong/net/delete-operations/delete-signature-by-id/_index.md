---
title: 按 ID 刪除簽名
linktitle: 按 ID 刪除簽名
second_title: GroupDocs.Signature .NET API
description: 了解如何使用 GroupDocs.Signature 函式庫按 ID 刪除 .NET 文件中的簽章。簡單的逐步指南。
type: docs
weight: 11
url: /zh-hant/net/delete-operations/delete-signature-by-id/
---
## 介紹
在本教學中，我們將探討如何使用 GroupDocs.Signature for .NET 按 ID 刪除簽章。 GroupDocs.Signature for .NET 是一個功能強大的程式庫，可讓開發人員使用 .NET 應用程式新增、刪除或驗證各種文件格式的數位簽章。
## 先決條件
在我們開始之前，請確保您具備以下先決條件：
1.  GroupDocs.Signature for .NET Library：從以下位置下載並安裝該程式庫[這裡](https://releases.groupdocs.com/signature/net/).
2. .NET Framework：請確定您的系統上安裝了 .NET Framework。
3. 帶有簽名的文件：準備帶有要刪除的簽名的文件（例如 DOCX、PDF）。

## 導入命名空間
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 第 1 步：定義檔路徑
首先，指定包含簽署的文件的文件路徑，以及儲存修改後的文件的輸出文件路徑。
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteById", fileName);
```
## 第 2 步：複製文檔
自從`Delete`方法就地修改文檔，最好建立原始文檔的副本。
```csharp
File.Copy(filePath, outputFilePath, true);
```
## 步驟3：按ID刪除簽名
初始化`Signature`物件與文檔文件路徑並使用`Delete`方法透過 ID 刪除簽名。
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    string id = @"eff64a14-dad9-47b0-88e5-2ee4e3604e71";
    bool result = signature.Delete(id);
    if (result)
    {
        Console.WriteLine($"Signature with Id# '{id}' was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature with id# '{id}' was not found!");
    }
}
```

## 結論
在本教學中，我們學習如何使用 GroupDocs.Signature for .NET 按 ID 刪除簽章。該庫提供了一種以程式設計方式管理各種文件格式的數位簽章的便捷方法。
## 常見問題解答
### 我可以一次刪除多個簽名嗎？
是的，您可以透過迭代 ID 並調用`Delete`每個 ID 的方法。
### GroupDocs.Signature for .NET 是否與所有文件格式相容？
GroupDocs.Signature for .NET 支援多種文件格式，包括 PDF、DOCX、XLSX 等。
### 我可以自訂簽名的外觀嗎？
是的，您可以自訂簽名的外觀，包括其位置、大小、字體和顏色。
### 有試用版嗎？
是的，您可以從以下位置下載免費試用版[這裡](https://releases.groupdocs.com/).
### 在哪裡可以找到 GroupDocs.Signature for .NET 的協助或支援？
您可以造訪支援論壇[這裡](https://forum.groupdocs.com/c/signature/13)尋求幫助。