---
title: 使用數位簽名進行簽名
linktitle: 使用數位簽名進行簽名
second_title: GroupDocs.Signature .NET API
description: 了解如何使用 GroupDocs.Signature 在 .NET 中對文件進行數位簽章。透過這個綜合教程增強安全性和真實性。
weight: 12
url: /zh-hant/net/advanced-signature-techniques/sign-with-digital/
---
## 介紹
數位簽章在確保電子文件的真實性和完整性方面發揮著至關重要的作用。在 .NET 開發領域，GroupDocs.Signature 提供了強大的解決方案，可將數位簽章無縫整合到您的應用程式中。本教學將引導您完成使用 GroupDocs.Signature for .NET 的數位簽章對文件進行簽署的流程。
## 先決條件
在我們深入實施之前，請確保您具備以下先決條件：
1.  GroupDocs.Signature for .NET：從下列位置下載並安裝 GroupDocs.Signature for .NET[下載頁面](https://releases.groupdocs.com/signature/net/).
2. 數位憑證：取得將用於簽署文件的數位憑證 (.pfx)。如果沒有，您可以建立自簽名憑證或從受信任的憑證授權單位取得該憑證。
3. 要簽署的文件：準備您想要進行數位簽章的文件（例如 PDF）。確保您擁有存取和修改文件所需的權限。
4. 簽名圖像：您可以選擇提供將嵌入到文件中的簽名圖像。這為數位簽名增添了個性化的感覺。

## 導入命名空間
首先，讓我們將必要的命名空間匯入到我們的 C# 程式碼中：
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 第 1 步：指定檔案路徑和選項
定義要簽署的文件、簽名影像（如果適用）和數位憑證的文件路徑。
```csharp
string filePath = "sample.pdf";
string fileName = Path.GetFileName(filePath);
string imagePath = "signature_handwrite.jpg";
string certificatePath = "YourSignature.pfx";
string outputFilePath = Path.Combine("Your Document Directory", "SignWithDigital", fileName);
```
## 步驟2：初始化簽名對象
建立一個實例`Signature`class 透過傳遞要簽署的文件的路徑。
```csharp
using (Signature signature = new Signature(filePath))
{
    //定義數位簽章選項
    DigitalSignOptions options = new DigitalSignOptions(certificatePath)
    {
        ImageFilePath = imagePath, //設定影像檔案路徑（可選）
        Left = 50,                 //設定簽名位置的X座標
        Top = 50,                  //設定簽名位置的Y座標
        PageNumber = 1,            //指定要簽署的頁碼
        Password = "1234567890"    //設定證書密碼（如果需要）
    };
    //第 3 步：簽署文件
    SignResult result = signature.Sign(outputFilePath, options);
    //第四步：顯示結果
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## 結論
在本教學中，我們探討如何使用適用於 .NET 的 GroupDocs.Signature 的數位簽章來簽署文件。透過執行這些簡單的步驟，您可以增強電子文件的安全性和真實性，確保它們防篡改並具有法律約束力。
## 常見問題解答
### 什麼是數位簽章？
數位簽章是一種用於驗證數位文件或訊息的真實性和完整性的加密技術。
### 我可以使用自簽名憑證透過 GroupDocs.Signature 簽署文件嗎？
是的，您可以使用 OpenSSL 或 Microsoft MakeCert 等工具產生的自簽名憑證來簽署文件。
### GroupDocs.Signature 是否與不同的文件格式相容？
是的，GroupDocs.Signature 支援多種文件格式，包括 PDF、Word、Excel、PowerPoint 等。
### 我可以自訂數位簽章的外觀嗎？
絕對地！ GroupDocs.Signature 可讓您自訂數位簽章的各個方面，例如其位置、大小和外觀。
### GroupDocs.Signature適合企業級應用嗎？
是的，GroupDocs.Signature 提供了強大的功能和可擴展性，使其成為企業級文件簽章應用程式的理想選擇。