---
"date": "2025-05-08"
"description": "了解如何使用 GroupDocs.Signature for Java 對 PDF 進行數位簽名，包括文字欄位、複選框和數位簽名。有效率簡化您的文件簽名流程。"
"title": "掌握 Java 中的 PDF 數位簽章－使用 GroupDocs.Signature 進行文字、複選框和數位欄位簽名"
"url": "/zh-hant/java/digital-signatures/sign-pdfs-groupdocs-signature-java/"
"weight": 1
---

# 掌握 Java 中的 PDF 數位簽章：使用 GroupDocs.Signature 進行文字、複選框和數位字段

## 介紹

需要對 PDF 進行數位簽名，但想要的不僅僅是圖片或數位憑證？無論您是批准合約、簽署文件或新增結構化同意，GroupDocs.Signature for Java 都能為您提供解決方案。該庫支援將文字表單欄位簽章、複選框簽章和數位簽章無縫整合到您的 PDF 中。

在本教程中，我們將探索如何使用 GroupDocs.Signature for Java 來簽署 PDF 文檔，這些文檔包含各種表單欄位類型—文字、複選框和數字。您將學習如何在 Java 應用程式中有效地實現這些功能。 

**您將學到什麼：**
- 如何為 Java 設定 GroupDocs.Signature
- 實作文字表單欄位簽名
- 新增複選框表單欄位簽名
- 集成數位表單欄位簽名
- 優化性能並與其他系統集成

在深入實施之前，讓我們先來了解一些先決條件。

## 先決條件

要學習本教程，您需要：
- **Java 開發工具包 (JDK)**：確保您的系統上安裝了 JDK 8 或更高版本。
- **整合開發環境**：任何 Java IDE（如 IntelliJ IDEA、Eclipse 或 NetBeans）都可以正常運作。
- **GroupDocs.Signature Java 函式庫**：透過 Maven、Gradle 或直接下載取得。

### 環境設定要求

確保您的開發環境設定了必要的依賴項和函式庫，以有效使用 GroupDocs.Signature 的功能。

### 知識前提

對 Java 程式設計的基本了解和熟悉以程式設計方式處理 PDF 將有助於學習本教學。

## 為 Java 設定 GroupDocs.Signature

若要開始在專案中使用 GroupDocs.Signature for Java，請將該程式庫新增至相依性。操作方法如下：

**Maven：**

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Gradle：**

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**直接下載**

您也可以從下載最新版本 [GroupDocs.Signature Java 版本](https://releases。groupdocs.com/signature/java/).

### 許可證取得步驟

- **免費試用**：從免費試用開始探索其功能。
- **臨時執照**：取得臨時許可證以無限制地測試全部功能。
- **購買**：如果它適合您的長期需求，請考慮購買許可證。

將 GroupDocs.Signature 新增至專案後，初始化 `Signature` 對像如下：

```java
import com.groupdocs.signature.Signature;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
Signature signature = new Signature(filePath);
```

## 實施指南

讓我們將實作分解為具體功能——文字表單欄位、複選框表單欄位和數位表單欄位簽章。

### 文字表單欄位簽名

#### 概述

使用文字表單欄位簽署 PDF 可讓您新增可編輯欄位供使用者輸入。這對於需要使用者輸入資料的文件非常有用。

**設定文字表單欄位簽名：**
1. **實例化簽章對象**
   ```java
   String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
   Signature signature = new Signature(filePath);
   ```
2. **建立 TextFieldSignature**
   ```java
   import com.groupdocs.signature.domain.signatures.formfield.TextFormFieldSignature;

   TextFormFieldSignature textSignature = new TextFormFieldSignature("tbData1", "Value-1");
   ```
3. **配置 FormFieldSignOptions**
   ```java
   import com.groupdocs.signature.options.sign.FormFieldSignOptions;
   import com.groupdocs.signature.domain.Padding;
   import com.groupdocs.signature.domain.enums.HorizontalAlignment;
   import com.groupdocs.signature.domain.enums.VerticalAlignment;

   FormFieldSignOptions optionsTextFF = new FormFieldSignOptions(textSignature);
   optionsTextFF.setHorizontalAlignment(HorizontalAlignment.Left);
   optionsTextFF.setVerticalAlignment(VerticalAlignment.Top);
   optionsTextFF.setMargin(new Padding(10, 20, 0, 0));
   optionsTextFF.setHeight(10);
   optionsTextFF.setWidth(100);
   ```
4. **簽署文件**
   ```java
   import java.util.ArrayList;
   import java.util.List;

   List<com.groupdocs.signature.options.sign.SignOptions> listOptions = new ArrayList<>();
   listOptions.add(optionsTextFF);

   SignResult signResult = signature.sign("YOUR_OUTPUT_DIRECTORY/SignTextFormFieldSignature_" + Paths.get(filePath).getFileName().toString(), listOptions);
   ```
### 複選框表單欄位簽名

#### 概述

複選框表單欄位非常適合需要使用者選擇或同意的文件。此功能簡化了互動式複選框的新增。

**設定複選框表單欄位簽名：**
1. **實例化簽章對象**
   ```java
   String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
   Signature signature = new Signature(filePath);
   ```
2. **建立 CheckboxFormFieldSignature**
   ```java
   import com.groupdocs.signature.domain.signatures.formfield.CheckboxFormFieldSignature;

   CheckboxFormFieldSignature chbSignature = new CheckboxFormFieldSignature("chbData1", true);
   ```
3. **配置 FormFieldSignOptions**
   ```java
   FormFieldSignOptions optionsTextCHB = new FormFieldSignOptions(chbSignature);
   optionsTextCHB.setHorizontalAlignment(HorizontalAlignment.Center);
   optionsTextCHB.setVerticalAlignment(VerticalAlignment.Top);
   optionsTextCHB.setMargin(new Padding(0, 0, 0, 0));
   optionsTextCHB.setHeight(10);
   optionsTextCHB.setWidth(100);
   ```
4. **簽署文件**
   ```java
   List<com.groupdocs.signature.options.sign.SignOptions> listOptions = new ArrayList<>();
   listOptions.add(optionsTextCHB);

   SignResult signResult = signature.sign("YOUR_OUTPUT_DIRECTORY/SignCheckboxFormFieldSignature_" + Paths.get(filePath).getFileName().toString(), listOptions);
   ```
### 數位表單欄位簽名

#### 概述

數位表單欄位允許使用數位憑證進行安全簽名，確保文件的真實性和完整性。

**設定數位表單欄位簽章：**
1. **實例化簽章對象**
   ```java
   String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
   Signature signature = new Signature(filePath);
   ```
2. **建立 DigitalFormFieldSignature**
   ```java
   import com.groupdocs.signature.domain.signatures.formfield.DigitalFormFieldSignature;

   DigitalFormFieldSignature digitalSignature = new DigitalFormFieldSignature("dgData1");
   ```
3. **配置 FormFieldSignOptions**
   ```java
   FormFieldSignOptions optionsTextDIG = new FormFieldSignOptions(digitalSignature);
   optionsTextDIG.setHorizontalAlignment(HorizontalAlignment.Right);
   optionsTextDIG.setVerticalAlignment(VerticalAlignment.Center);
   optionsTextDIG.setMargin(new Padding(0, 50, 0, 0));
   optionsTextDIG.setHeight(50);
   optionsTextDIG.setWidth(50);
   ```
4. **簽署文件**
   ```java
   List<com.groupdocs.signature.options.sign.SignOptions> listOptions = new ArrayList<>();
   listOptions.add(optionsTextDIG);

   SignResult signResult = signature.sign("YOUR_OUTPUT_DIRECTORY/SignDigitalFormFieldSignature_" + Paths.get(filePath).getFileName().toString(), listOptions);
   ```
## 實際應用

GroupDocs.Signature for Java 功能多樣，可應用於多種實際場景：
- **合約管理**：使用文字欄位、複選框和數位簽章自動簽署合約。
- **審批工作流程**：在您的組織內實施數位審批系統。
- **客戶協議**：透過安全的數位簽章簡化客戶協議。

本指南內容全面，確保您能夠自信地使用 GroupDocs.Signature 在 Java 應用程式中實現數位簽章。如需進一步探索，您可以考慮將這些功能整合到更大型的文件管理系統或自動化工作流程中。