---
"date": "2025-05-07"
"description": "了解如何使用 GroupDocs.Signature for .NET 對 PDF 進行數位簽章。自訂外觀、套用字體和圖像，確保文件的安全性和真實性。"
"title": ".NET 中的數位 PDF 簽章－使用 GroupDocs.Signature 的指南"
"url": "/zh-hant/net/digital-signatures/sign-pdf-digital-signature-groupdocs-dotnet/"
"weight": 1
type: docs
---
# .NET 中的數位 PDF 簽章：使用 GroupDocs.Signature 的指南

## 介紹

PDF 文件上的數位簽章可確保其真實性、安全性和完整性——這對於法律合約、發票和官方記錄至關重要。 **適用於 .NET 的 GroupDocs.Signature** 簡化了為 PDF 添加數位簽章的過程，同時允許自訂其外觀以增強視覺吸引力。本教學將引導您使用 GroupDocs.Signature 完成 PDF 文件簽名，並專注於講解圖像和字體的配置。

### 您將學到什麼：
- 如何使用 .NET 對 PDF 文件進行數位簽名
- 將自訂外觀設定（如圖像和字體）套用至您的數位簽名
- 在您的專案中設定並初始化 .NET 的 GroupDocs.Signature

讓我們先介紹一下開始所需的先決條件。

## 先決條件（H2）

要遵循本教程，您需要：

- **適用於 .NET 的 GroupDocs.Signature** 庫：確保它是透過 .NET CLI 或 NuGet 套件管理器安裝的。
  - **.NET CLI**： `dotnet add package GroupDocs.Signature`
  - **套件管理器**： `Install-Package GroupDocs.Signature`

- PFX 格式的有效數位證書
- C# 和 .NET 環境設定的基礎知識

## 為 .NET 設定 GroupDocs.Signature（H2）

首先安裝 GroupDocs.Signature 庫：

**.NET CLI**
```shell
dotnet add package GroupDocs.Signature
```

**套件管理器**
```shell
Install-Package GroupDocs.Signature
```

或者，使用 NuGet 套件管理器 UI 搜尋並安裝「GroupDocs.Signature」。

### 許可證獲取

- **免費試用**：使用臨時評估許可證探索全部功能。
- **臨時執照**：從 [這裡](https://purchase。groupdocs.com/temporary-license/).
- **購買**：如需長期使用，請購買訂閱 [此連結](https://purchase。groupdocs.com/buy).

### 基本初始化和設定

若要在 .NET 專案中初始化 GroupDocs.Signature：

```csharp
using GroupDocs.Signature;

// 使用來源 PDF 檔案初始化簽名物件。
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF.pdf")) {
    // 您簽署文件的程式碼放在這裡。
}
```

## 實施指南

### 使用數位簽章 (H2) 簽署 PDF 文檔

此功能可讓您為 PDF 文件添加數位簽名，以確保其真實性和完整性。

#### 功能概述
透過實現此功能，您可以使用 GroupDocs.Signature for .NET 對任何 PDF 文件進行數位簽署。您還可以套用自訂設定來客製化簽名的外觀，包括圖像和字體。

#### 實施步驟（H3）

##### 步驟 1：設定您的環境

確保您的專案配置了必要的引用：

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Options;
using GroupDocs.Signature.Domain;

namespace DigitalSignatureExample {
    public class SignPdfWithDigitalSignature {
        // 定義來源 PDF 和數位憑證的路徑
        private static string sourceFile = "YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF.pdf";
        private static string outputFile = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithPdfDigitalAdvanced_Signed.pdf");
        private static string certificatePath = "YOUR_DOCUMENT_DIRECTORY/CertificatePfx.pfx";

        public static void Run() {
            // 初始化簽名對象
            using (Signature signature = new Signature(sourceFile)) {
                // 設定數位簽名選項
                DigitalSignOptions options = new DigitalSignOptions(certificatePath) {
                    Password = "1234567890",  // 證書密碼
                    Reason = "Sign",          // 簽名原因
                    Contact = "JohnSmith",    // 聯絡資訊
                    Location = "Office1",     // 簽約地點
                    Visible = true,            // 使簽名可見
                    Left = 400,                // 水平位置
                    Top = 20,                  // 垂直位置
                    Height = 70,               // 簽名高度
                    Width = 200,               // 簽名寬度
                    ImageFilePath = "YOUR_DOCUMENT_DIRECTORY/ImageHandwrite.png", // 外觀圖
                    Appearance = new PdfDigitalSignatureAppearance() {
                        Foreground = System.Drawing.Color.FromArgb(50, System.Drawing.Color.Gray),
                        FontFamilyName = "TimesNewRoman",
                        FontSize = 12
                    }
                };

                // 簽署文件並將其儲存到輸出路徑。
                SignResult signResult = signature.Sign(outputFile, options);
                Console.WriteLine($"Document signed successfully with {signResult.Succeeded.Count} signature(s). File saved at {outputFile}.");
            }
        }
    }
}
```

##### 步驟 2：自訂簽名外觀

使用字體和圖像設定自訂數位簽名的外觀：

```csharp
using System;
using GroupDocs.Signature.Options;
using GroupDocs.Signature.Domain;
using System.Drawing;

namespace DigitalSignatureAppearanceExample {
    public class CustomizeDigitalSignatureAppearance {
        public static void Run() {
            // 初始化數位簽名的外觀設定。
            PdfDigitalSignatureAppearance appearance = new PdfDigitalSignatureAppearance() {
                Foreground = Color.FromArgb(50, Color.Gray),  // 設定自訂字體顏色
                FontFamilyName = "TimesNewRoman",          // 指定字型系列
                FontSize = 12                               // 定義字體大小
            };

            Console.WriteLine("Custom appearance settings for digital signature have been applied.");
        }
    }
}
```

#### 關鍵配置選項
- **證書路徑**：確保您提供了 PFX 檔案的正確路徑。
- **密碼**：使用與您的數位憑證關聯的密碼。
- **外觀設定**：自訂字體和顏色以符合品牌要求。

##### 故障排除提示
- 驗證您的數位憑證是否有效且配置正確。
- 確保所有路徑（PDF、輸出、影像）都可以從應用程式環境存取。

### 將自訂外觀設定套用至數位簽章 (H2)

使用 GroupDocs.Signature for .NET 透過自訂字體和圖像設定增強數位簽章的視覺吸引力。

#### 概述
自訂數位簽名的外觀可以使其更具視覺吸引力，並符合品牌標準。此功能可讓您設定特定的字體、顏色和圖像。

#### 實施步驟（H3）

##### 步驟1：初始化外觀設置

建立一個實例 `PdfDigitalSignatureAppearance`：

```csharp
using System.Drawing;

// 定義數位簽章的自訂外觀設定。
PdfDigitalSignatureAppearance appearance = new PdfDigitalSignatureAppearance() {
    Foreground = Color.FromArgb(50, Color.Gray),  // 自訂字體顏色
    FontFamilyName = "TimesNewRoman",            // 字體系列
    FontSize = 12                                // 字體大小
};
```

##### 步驟 2：套用外觀設定

將這些設定整合到您的數位簽章選項中：

```csharp
DigitalSignOptions options = new DigitalSignOptions(certificatePath) {
    ImageFilePath = "YOUR_DOCUMENT_DIRECTORY/ImageHandwrite.png",
    Appearance = appearance
};
```

## 實際應用（H2）

以下是使用 GroupDocs.Signature 簽署 PDF 的一些實際場景：
1. **合約簽訂**：確保法律協議以數位方式簽署和驗證。
2. **發票審核**：對發票進行數位簽名，以便財務部門更快處理。
3. **文件認證**：驗證官方文件的真實性，防止未經授權的更改。

透過遵循本指南，您將使用 GroupDocs.Signature 將數位簽章有效整合到您的 .NET 應用程式中，從而增強安全性和專業性。