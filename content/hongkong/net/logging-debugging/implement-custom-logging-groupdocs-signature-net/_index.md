---
"date": "2025-05-07"
"description": "使用 GroupDocs.Signature for .NET 掌握自訂日誌記錄。了解如何透過控制台和基於 API 的日誌記錄解決方案增強文件簽章的可見性。"
"title": "在 GroupDocs.Signature for .NET 中實作自訂日誌記錄－綜合指南"
"url": "/zh-hant/net/logging-debugging/implement-custom-logging-groupdocs-signature-net/"
"weight": 1
---

# 在 GroupDocs.Signature for .NET 中實作自訂日誌記錄：綜合指南

## 介紹

在使用 GroupDocs.Signature for .NET 進行文件簽章過程中，您是否面臨錯誤和事件追蹤的挑戰？本指南將指導您設定自訂日誌記錄，這是一項強大的功能，可增強應用程式簽署流程的可見性。透過整合控制台和基於 API 的日誌記錄解決方案，您可以有效率地擷取詳細的日誌。

**您將學到什麼：**
- 在 GroupDocs.Signature for .NET 中實作自訂日誌記錄
- 使用增強日誌記錄功能簽署受密碼保護的文件的步驟
- 設定將日誌訊息傳送到指定端點的 API 記錄器

準備好解鎖更好的調試和監控功能了嗎？讓我們先了解先決條件。

## 先決條件

在深入自訂日誌記錄之前，請確保已做好以下準備：

### 所需的庫和版本
- **適用於 .NET 的 GroupDocs.Signature**：此庫必須整合到您的專案中。它提供了強大的文件簽名功能，並支援二維碼等各種簽名類型。
- **系統.Net.Http**：對於實作基於 API 的日誌記錄至關重要。

### 環境設定要求
- .NET 開發環境（例如 Visual Studio）。
- 如果您打算使用自訂 API 記錄器功能，則可存取 API 端點。

### 知識前提
- 對 C# 和 .NET 架構有基本的了解。
- 熟悉.NET 中的異常處理。

滿足這些先決條件後，讓我們繼續為您的專案設定 GroupDocs.Signature。

## 為 .NET 設定 GroupDocs.Signature

要開始使用 GroupDocs.Signature，您需要透過其中一個軟體套件管理器進行安裝。步驟如下：

### 安裝選項

**.NET CLI**
```shell
dotnet add package GroupDocs.Signature
```

**套件管理器**
```powershell
Install-Package GroupDocs.Signature
```

**NuGet 套件管理器 UI**
- 在您的 IDE 中開啟 NuGet 套件管理器。
- 搜尋“GroupDocs.Signature”並安裝最新版本。

### 許可證獲取

要使用 GroupDocs.Signature，您可以：
- **免費試用**：下載試用版以探索基本功能。
- **臨時執照**：取得全功能測試的臨時許可證。
- **購買**：取得生產環境的商業許可證。

### 基本初始化

以下是在 .NET 應用程式中初始化 GroupDocs.Signature 的方法：

```csharp
using GroupDocs.Signature;

// 建立 Signature 類別的實例
signature = new Signature("sample.pdf");
```

此設定構成了我們建立自訂日誌記錄功能的基礎。

## 實施指南

現在，讓我們深入研究如何實作自訂日誌記錄。我們將探索兩個關鍵功能：基於控制台的日誌記錄和基於 API 的日誌記錄。

### 簽名過程的自訂日誌記錄

#### 概述
此功能示範如何在使用 `ConsoleLogger`。

#### 逐步實施

**定義路徑和載入選項**
首先設定檔案路徑和錯誤密碼以進行示範：

```csharp
string filePath = "YOUR_DOCUMENT_DIRECTORY\\sample.pdf"; // 替換為您的實際文件路徑
LoadOptions loadOptions = new LoadOptions() { Password = "12345678901" };
```

**初始化自訂記錄器**
建立一個實例 `ConsoleLogger` 並配置日誌記錄設定：

```csharp
var logger = new ConsoleLogger();
var settings = new SignatureSettings(logger);
settings.LogLevel = LogLevel.Warning | LogLevel.Error;
```

**簽署文件**
使用 GroupDocs.Signature 對您的文件進行簽名並啟用自訂日誌記錄：

```csharp
try
{
    using (Signature signature = new Signature(filePath, loadOptions, settings))
    {
        QrCodeSignOptions options = new QrCodeSignOptions("JohnSmith")
        {
            EncodeType = QrCodeTypes.QR,
            Left = 100,
            Top = 100
        };

        signature.Sign("outputPath", options);
    }
}
catch (Exception ex)
{
    logger.Error("Signing process failed.", ex);
}
```

**故障排除提示**
- 確保檔案路徑設定正確且可存取。
- 如果不是為了演示，請驗證您的文件密碼是否正確。

### 自訂 API 記錄器

#### 概述
此功能將日誌訊息傳送到指定的 API 端點，允許集中日誌管理。

#### 逐步實施

**設定 HttpClient**
初始化一個 `HttpClient` 帶有必要的標題：

```csharp
class APILogger : ILogger
{
    private object _lock = new object();
    private HttpClient _client;

    public APILogger()
    {
        _client = new HttpClient() { BaseAddress = new Uri("http://本機：64195 /”）};
        _client.DefaultRequestHeaders.Accept.Clear();
        _client.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));
    }
}
```

**實作日誌記錄方法**
定義記錄錯誤、追蹤和警告的方法：

```csharp
public void Error(string message, Exception exception)
{
    if (string.IsNullOrEmpty(message) || exception == null) throw new ArgumentNullException(message == null ? nameof(message) : nameof(exception));
    PostMessage(LogLevel.Error, $"{message}. Exception: {exception}");
}

private string PostMessage(LogLevel level, string message)
{
    var hdrs = level switch
    {
        LogLevel.Warning => "WARNING",
        LogLevel.Error => "ERROR",
        _ => "INFO"
    };

    var date = DateTime.Now.ToString("MM/dd/yyyy hh:mm tt");
    var line = $"GroupDocs.Signature {hdrs} [{date}]. Message: {message}";
    var content = new StringContent(line);

    lock (_lock)
    {
        var response = _client.PostAsync("api/logging", content).Result;
        response.EnsureSuccessStatusCode();
        return response.Content.ReadAsStringAsync().Result;
    }
}
```

**故障排除提示**
- 確保您的 API 端點可存取且配置正確。
- 如果遇到 HTTP 請求問題，請驗證網路連線。

## 實際應用

### 使用 GroupDocs.Signature 進行自訂日誌記錄的用例
1. **文件管理系統**：追蹤企業文件工作流程中的簽名流程。
2. **法律文件自動化**：監控簽名事件以確保合規性和完整性。
3. **電子商務平台**：在結帳過程中記錄客戶協議。
4. **教育機構**：以電子方式記錄同意書或學生錄取情況。
5. **醫療保健提供者**：透過詳細記錄安全地管理病患記錄同意書。

## 性能考慮

### 優化技巧
- 使用適當的日誌等級以避免過多的日誌記錄而影響效能。
- 確保有效的資源管理，並妥善處置 `Signature` 和 `HttpClient` 實例。
- 處理大型文件或大量簽章操作時監控應用程式記憶體使用量。

### .NET 記憶體管理的最佳實踐
- 利用 `using` 語句自動處置非託管資源。
- 盡可能實現非同步日誌記錄以避免阻塞主執行緒執行。

## 結論

透過在 GroupDocs.Signature for .NET 中實作自訂日誌記錄，您可以顯著增強應用程式的穩健性和可維護性。本教學將幫助您了解如何將控制台和基於 API 的日誌記錄功能整合到您的簽名流程中。

**後續步驟：**
- 嘗試不同的日誌等級並觀察它們對調試效率的影響。
- 在 GroupDocs.Signature 的文檔中探索更多自訂選項。

準備好增強應用程式的日誌記錄功能了嗎？立即開始實現這些功能！

## 常見問題部分

### 問題 1：使用 GroupDocs.Signature 自訂日誌記錄有什麼好處？
自訂日誌記錄可以更好地洞察文件簽署流程，有助於排除故障並確保流程的完整性。

### 關鍵字推薦
- “在 GroupDocs.Signature 中實作自訂日誌記錄”
- “GroupDocs.Signature .NET 日誌解決方案”
- “增強文檔簽章可見性 .NET”