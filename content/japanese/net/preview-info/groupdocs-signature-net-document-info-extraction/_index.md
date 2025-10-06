---
"date": "2025-05-07"
"description": "GroupDocs.Signature for .NET を使用して、署名、メタデータなどを含む詳細なドキュメント情報を抽出する方法を学びます。このガイドでは、セットアップ、実装、ベストプラクティスについて説明します。"
"title": "マスターGroupDocs.Signature for .NET&#58; ドキュメント情報を効率的に抽出して表示"
"url": "/ja/net/preview-info/groupdocs-signature-net-document-info-extraction/"
"weight": 1
type: docs
---
# GroupDocs.Signature for .NET をマスターする: ドキュメント情報を効率的に抽出して表示する

## 導入

アプリケーション内のドキュメントから包括的な詳細情報を効率的に抽出したいとお考えですか？契約書、合意書、複数ページのPDFなどを管理する場合、堅牢なソリューションが不可欠です。 **.NET 用 GroupDocs.Signature** フォームフィールド、署名、メタデータなどの要素を取得・表示することで、ドキュメント分析を効率化するための強力な機能を提供します。このチュートリアルでは、これらの機能を活用してアプリケーションの機能を強化する方法について説明します。

**学習内容:**
- GroupDocs.Signature for .NET を使用して詳細なドキュメント情報を取得する方法
- さまざまな署名タイプとフォームフィールドの詳細を表示する
- メタデータとページ固有の属性の抽出

実装に進む前に前提条件を確認しましょう。

## 前提条件

GroupDocs.Signature for .NET を利用する前に、環境が正しく設定されていることを確認してください。このチュートリアルは、C# に精通していることと、ドキュメント処理の概念に関する基本的な知識があることを前提としています。

### 必要なライブラリと依存関係
- **.NET 用 GroupDocs.Signature**: 使用する主なライブラリ。
- **.NET Framework または .NET Core**: プロジェクトの設定によって異なります。

### 環境設定
Visual Studio または .NET プロジェクトをサポートする他の適切な IDE を使用した開発環境の準備ができていることを確認します。

### 知識の前提条件
- C# プログラミングの基本的な理解。
- ドキュメントの種類 (PDF、Word、Excel) とそのプロパティに関する知識。

## GroupDocs.Signature を .NET 用にセットアップする

GroupDocs.Signature for .NETを使用するには、ライブラリをインストールする必要があります。以下の方法があります。

### インストール手順

**.NET CLI の使用:**
```bash
dotnet add package GroupDocs.Signature
```

**パッケージ マネージャー コンソールの使用:**
```powershell
Install-Package GroupDocs.Signature
```

**NuGet パッケージ マネージャー UI:**
NuGet パッケージ マネージャーで「GroupDocs.Signature」を検索し、最新バージョンをインストールします。

### ライセンス取得
GroupDocs.Signature を最大限に活用するには、ライセンスの取得を検討してください。
- **無料トライアル**無料トライアルで機能をご確認ください。
- **一時ライセンス**延長テスト用の一時ライセンスを取得します。
- **購入**実稼働環境で使用する場合はフルライセンスを購入してください。

インストールしてライセンスを取得したら、以下に示すように GroupDocs.Signature 環境を設定してプロジェクトを初期化します。

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;

public class GetDocumentInfoFeature
{
    public static void Run()
    {
        // 分析したいドキュメントのファイルパスを定義します
        string filePath = "YOUR_DOCUMENT_DIRECTORY\Sample_Signed_Multi_Document.pdf";  // 実際のドキュメントパスに置き換えます
        
        SignatureSettings signatureSettings = new SignatureSettings
        {
            IncludeStandardMetadataSignatures = true
        };

        using (Signature signature = new Signature(filePath, signatureSettings))
        {
            IDocumentInfo documentInfo = signature.GetDocumentInfo();
            // さらなる操作はここで実行されます...
        }
    }
}
```

## 実装ガイド

セットアップが完了したら、GroupDocs.Signature for .NET のさまざまな機能を実装する方法を調べてみましょう。

### 基本的なドキュメントプロパティを取得して表示する

**概要**ファイル形式、サイズ、ページ数などの重要なプロパティを抽出します。

#### ステップバイステップの実装:
1. **署名オブジェクトの初期化**インスタンスを作成する `Signature` ドキュメントのパスを持つクラス。
2. **GetDocumentInfo メソッド**使用 `GetDocumentInfo()` ドキュメントの詳細情報を取得する方法。
3. **ドキュメントのプロパティを表示**フォーマット、拡張子、サイズなどの基本的なプロパティを出力します。 `Console.WriteLine` デバッグまたはログ記録の目的のため。

```csharp
IDocumentInfo documentInfo = signature.GetDocumentInfo();
Console.WriteLine($"Document properties {Path.GetFileName(filePath)}:");
Console.WriteLine($" - format : {documentInfo.FileType.FileFormat}");
Console.WriteLine($" - extension : {documentInfo.FileType.Extension}");
Console.WriteLine($" - size : {documentInfo.Size}");
Console.WriteLine($" - page count : {documentInfo.PageCount}");
```

### 各ドキュメントページに関する情報を表示する

**概要**ドキュメント内の各ページに関する情報を取得して表示することで、さらに深く掘り下げることができます。

#### ステップバイステップの実装:
1. **ページを反復処理する**ループスルー `documentInfo.Pages` 幅や高さなどの個々のページの詳細にアクセスします。

```csharp
foreach (PageInfo pageInfo in documentInfo.Pages)
{
    Console.WriteLine($" - page-{pageInfo.PageNumber} Width {pageInfo.Width}, Height {pageInfo.Height}");
}
```

### フォームフィールドの署名情報を表示する

**概要**ドキュメント内のフォーム フィールドに関連する情報を抽出して表示します。

#### ステップバイステップの実装:
1. **アクセスフォームフィールド**： 使用 `documentInfo.FormFields` ドキュメント内に存在するすべてのフォーム フィールド署名を取得します。
2. **各フォームフィールドの詳細を表示する**各フォーム フィールドを反復処理し、そのタイプ、名前、値を出力します。

```csharp
Console.WriteLine($"Document Form Fields information: count = {documentInfo.FormFields.Count}");
foreach (FormFieldSignature formField in documentInfo.FormFields)
{
    Console.WriteLine($" - type #{formField.Type}: Name: {formField.Name} Value: {formField.Value}");
}
```

### さまざまな署名情報を表示する

**概要**テキスト、画像、デジタル、バーコード、QR コード、フォーム フィールド、メタデータ署名の情報を取得して表示します。

#### 実装手順:
- **テキスト署名**： アクセス `documentInfo.TextSignatures` 各テキスト署名の ID、場所、サイズ、作成日などの詳細を取得します。

```csharp
Console.WriteLine($"Document Text signatures: {documentInfo.TextSignatures.Count}");
foreach (TextSignature textSignature in documentInfo.TextSignatures)
{
    Console.WriteLine($" - #{textSignature.SignatureId}: Text: {textSignature.Text} Location: {textSignature.Left}x{textSignature.Top}. Size: {textSignature.Width}x{textSignature.Height}. CreatedOn/ModifiedOn: {textSignature.CreatedOn.ToShortDateString()} / {textSignature.ModifiedOn.ToShortDateString()}");
}
```

- **画像署名**テキスト署名と同様に、 `documentInfo.ImageSignatures` 画像署名のサイズや形式などの詳細。

```csharp
Console.WriteLine($"Document Image signatures: {documentInfo.ImageSignatures.Count}");
foreach (ImageSignature imageSignature in documentInfo.ImageSignatures)
{
    Console.WriteLine($" - #{imageSignature.SignatureId}: Size: {imageSignature.Size} bytes, Format: {imageSignature.Format}. CreatedOn/ModifiedOn: {imageSignature.CreatedOn.ToShortDateString()} / {imageSignature.ModifiedOn.ToShortDateString()}");
}
```

- **デジタル署名**デジタル署名には、 `documentInfo.DigitalSignatures` 署名 ID とタイムスタンプを抽出します。

```csharp
Console.WriteLine($"Document Digital signatures: {documentInfo.DigitalSignatures.Count}");
foreach (DigitalSignature digitalSignature in documentInfo.DigitalSignatures)
{
    Console.WriteLine($" - #{digitalSignature.SignatureId}. CreatedOn/ModifiedOn: {digitalSignature.CreatedOn.ToShortDateString()} / {digitalSignature.ModifiedOn.ToShortDateString()}");
}
```

- **バーコードとQRコードの署名**： 使用 `documentInfo.BarcodeSignatures` そして `documentInfo.QrCodeSignatures` それぞれバーコードとQRコードの詳細を収集します。

```csharp
Console.WriteLine($"Document Barcode signatures: {documentInfo.BarcodeSignatures.Count}");
foreach (BarcodeSignature barcodeSignature in documentInfo.BarcodeSignatures)
{
    Console.WriteLine($" - #{barcodeSignature.SignatureId}: Type: {barcodeSignature.EncodeType?.TypeName}. Text: {barcodeSignature.Text}");
}

Console.WriteLine($"Document QR Code signatures: {documentInfo.QrCodeSignatures.Count}");
foreach (QrCodeSignature qrCodeSignature in documentInfo.QrCodeSignatures)
{
    Console.WriteLine($" - #{qrCodeSignature.SignatureId}: Type: {qrCodeSignature.EncodeType?.TypeName}. Text: {qrCodeSignature.Text}");
}
```

### 結論

このチュートリアルでは、GroupDocs.Signature for .NETを活用して、包括的なドキュメント情報を効率的に抽出・表示する方法を学習しました。このスキルセットにより、アプリケーションのドキュメント管理能力が強化され、正確かつ容易になります。

**次のステップ:**
- GroupDocs.Signature の追加機能をご覧ください。
- アプリケーション内で署名検証を実装します。
- この機能を大規模なワークフローに統合して、ドキュメント処理を自動化します。