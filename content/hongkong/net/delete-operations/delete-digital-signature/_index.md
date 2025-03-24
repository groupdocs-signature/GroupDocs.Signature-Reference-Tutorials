---
title: 從文件中刪除數位簽名
linktitle: 從文件中刪除數位簽名
second_title: GroupDocs.Signature .NET API
description: 了解如何使用 GroupDocs.Signature for .NET 從文件中刪除數位簽章。遵循我們的逐步指南進行高效管理。
weight: 13
url: /zh-hant/net/delete-operations/delete-digital-signature/
---
## 介紹
在數位文件的世界中，確保真實性和安全性至關重要。數位簽章在驗證電子文件的完整性方面發揮著至關重要的作用。 GroupDocs.Signature for .NET 提供了強大的工具來有效管理 .NET 應用程式中的數位簽章。
## 先決條件
在深入使用 GroupDocs.Signature for .NET 從文件中刪除數位簽章之前，請確保您具備以下條件：
1. Visual Studio：在您的系統上安裝 Visual Studio IDE。
2.  GroupDocs.Signature for .NET：從下列位置下載並安裝 GroupDocs.Signature for .NET[下載頁面](https://releases.groupdocs.com/signature/net/).
3. 範例文件：準備包含數位簽章的範例文件以進行測試。

## 導入命名空間
首先，請確保在 .NET 專案中匯入必要的命名空間：
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```
## 第 1 步：定義檔路徑
首先定義來源文檔和輸出文檔的檔案路徑：
```csharp
string filePath = "sample.pdf"_SIGNED_DIGITAL;
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteDigital", fileName);
```
## 第 2 步：複製來源文檔
自從`Delete`方法適用於相同文檔，需要將來源文件複製到新位置：
```csharp
File.Copy(filePath, outputFilePath, true);
```
## 第三步：初始化簽名對象
初始化一個`Signature`具有輸出檔案路徑的物件：
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    //你的程式碼放在這裡
}
```
## 第 4 步：搜尋數位簽名
在文件中搜尋電子數位簽章：
```csharp
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
```
## 步驟5：刪除數位簽名
如果找到數位簽名，則刪除找到的第一個簽名：
```csharp
if (signatures.Count > 0)
{
    DigitalSignature digitalSignature = signatures[0];
    bool result = signature.Delete(digitalSignature);
    if (result)
    {
        Console.WriteLine($"Digital signature #{digitalSignature.Thumbprint} from {digitalSignature.SignTime.ToShortDateString()} was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature# {digitalSignature.Thumbprint} was not found!");
    }
}
```

## 結論
使用 GroupDocs.Signature 可以輕鬆管理 .NET 應用程式中的數位簽章。透過執行上述簡單步驟，您可以無縫地從文件中刪除數位簽名，從而確保資料的完整性和安全性。
## 常見問題解答
### 我可以從單一文件中刪除多個數位簽章嗎？
是的，您可以修改程式碼以迭代找到的所有數位簽名並相應地刪除它們。
### GroupDocs.Signature 是否支援數位簽章之外的其他類型的簽章？
是的，GroupDocs.Signature 支援各種類型的簽名，包括電子簽名、數位簽名和手寫簽名。
### GroupDocs.Signature適合企業級文件管理嗎？
當然，GroupDocs.Signature 旨在滿足個人開發人員和企業級應用程式的需求，提供強大的功能和可擴展性。
### 我可以自訂數位簽章的刪除流程嗎？
是的，GroupDocs.Signature 提供了廣泛的選項和設置，可根據您的特定要求自訂簽名刪除過程。
### 是否有可用於測試 GroupDocs.Signature 的試用版？
是的，您可以從以下位置下載免費試用版[發布頁面](https://releases.groupdocs.com/).