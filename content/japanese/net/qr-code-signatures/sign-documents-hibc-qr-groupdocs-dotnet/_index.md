---
"date": "2025-05-07"
"description": "GroupDocs.Signature for .NET を使用して、HIBC QRコードでPDF文書に署名する方法を学びます。このガイドでは、QRコード、Aztecコード、DataMatrixコードを含むLICコードとPASコードについて説明します。"
"title": "GroupDocs.Signature for .NET を使用して HIBC QR コードでドキュメントに署名する方法 - 包括的なガイド"
"url": "/ja/net/qr-code-signatures/sign-documents-hibc-qr-groupdocs-dotnet/"
"weight": 1
type: docs
---
# GroupDocs.Signature for .NET を使用して HIBC QR コードでドキュメントに署名する方法

## 導入

今日のめまぐるしく変化するビジネス環境において、文書の真正性と完全性を確保することは極めて重要です。医薬品、ヘルスケア製品、物流など、どのような分野であっても、文書の署名と追跡を安全に行うことで、時間を節約し、ミスを防ぐことができます。 **.NET 用 GroupDocs.Signature**は、HIBC QR コードをドキュメントにシームレスに統合できるようにすることで、ドキュメント管理プロセスを効率化するように設計された強力なライブラリです。

このチュートリアルでは、GroupDocs.Signature for .NET を活用して、QR コード、Aztec コード、DataMatrix といった様々な種類の HIBC QR コード（LIC（ライセンス）および PAS（製品認証システム））で PDF ドキュメントに署名する方法を学びます。このチュートリアルを終える頃には、これらのソリューションを .NET アプリケーションに実装する方法をしっかりと理解できるようになります。

**学習内容:**
- GroupDocs.Signature for .NET の設定方法
- HIBC LIC QRコード、Aztecコード、およびDataMatrixの実装
- HIBC PAS QRコード、Aztecコード、DataMatrixの追加
- 実用的なユースケースと統合の可能性

これらの機能を実装する前に、前提条件について詳しく見ていきましょう。

## 前提条件

コーディングを始める前に、以下のものを用意しておいてください。

- **.NET環境**システムに .NET がインストールされていることを確認してください (.NET Core または .NET 5/6+ が望ましい)。
- **.NET 用 GroupDocs.Signature**: このライブラリがメインツールになります。NuGet経由でインストールできます。
- **基本的なプログラミング知識**C# および .NET でのファイルの処理に精通していることが推奨されます。

### 必要なライブラリ

GroupDocs.Signature for .NET を使用するには、次のいずれかの方法でパッケージを追加する必要があります。

**.NET CLI**
```bash
dotnet add package GroupDocs.Signature
```

**パッケージマネージャー**
```powershell
Install-Package GroupDocs.Signature
```

**NuGet パッケージ マネージャー UI**
「GroupDocs.Signature」を検索し、最新バージョンをインストールしてください。

### ライセンス取得

テスト目的では、無料のトライアルライセンスをご利用いただけます。長期間ご利用いただく場合は、サブスクリプションのご購入、または一時ライセンスの申請をご検討ください。

- **無料トライアル**： アクセス [ここ](https://releases.groupdocs.com/signature/net/)
- **一時ライセンス**リクエスト [このリンク](https://purchase.groupdocs.com/temporary-license/)

### 環境設定

プロジェクトが適切な .NET バージョンをターゲットにし、GroupDocs.Signature にアクセスできることを確認して環境を設定します。アプリケーション内で以下のように初期化します。

```csharp
using GroupDocs.Signature;
```

## GroupDocs.Signature を .NET 用にセットアップする

GroupDocs.Signature for .NET の使用を開始するには、ライブラリをインストールし、プロジェクト内で基本的なセットアップを構成する必要があります。

### インストール

上記のいずれかの方法で、GroupDocs.Signature をプロジェクトに追加してください。インストールが完了したら、コードファイルで参照して、プロジェクトで使用できるように設定されていることを確認してください。

### ライセンスの初期化

ライセンスを取得したら、次のように初期化します。

```csharp
SignatureConfig signConfig = new SignatureConfig();
signConfig.LicensePath = "path/to/your/license.lic";
Signature signature = new Signature("Sample.pdf", signConfig);
```

この設定により、GroupDocs.Signature のすべての機能に制限なくアクセスできるようになります。

## 実装ガイド

それでは、GroupDocs.Signature for .NET で HIBC QR コードを使用して各機能を実装してみましょう。

### HIBC LIC QRコードで文書に署名する

#### 概要

HIBC LIC QRコードで文書に署名することで、ライセンス管理におけるコンプライアンスとトレーサビリティを確保できます。このセクションでは、PDF文書にQRコードを作成し、埋め込む方法について説明します。

#### 実装手順

##### ステップ1: ソースパスと出力パスを構成する

ソース ドキュメントの場所と署名された出力を保存する場所を定義します。

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICQR");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICQR.pdf");
```

##### ステップ2：QRコードサインオプションを作成する

特定のテキストと設定で QR コードを構成します。

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcLic_QR_Options = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR)
    {
        Left = 1,
        Top = 1,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    // これらのオプションを使用してドキュメントに署名します。
    signature.Sign(destinFilePath, hibcLic_QR_Options);
}
```

**説明**： 
- `QrCodeSignOptions` QRコードの外観と内容を設定します。ここでは、HIBC LIC QRコードの種類を指定し、ドキュメント上の位置を指定します。
- `ReturnContent` true に設定すると、署名されたドキュメントのレンダリングされた画像を取得できます。

#### トラブルシューティングのヒント

- ドキュメント パスが正しく指定されていることを確認します。
- GroupDocs.Signature の全機能を利用するために適切なライセンスが付与されていることを確認します。

### HIBC LIC Aztecコードで文書に署名する

#### 概要

Aztecコードは、高密度情報保存に適した別の形式のエンコード方式を提供します。このセクションでは、GroupDocs.Signatureを使用してAztecコードをドキュメントに埋め込む方法について説明します。

#### 実装手順

##### ステップ1: パスを構成する

前の機能と同様に、ファイル パスを定義します。

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICAztec");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICAztec.pdf");
```

##### ステップ2: Aztecコードオプションを構成する

GroupDocs.Signature を使用して Aztec コードを設定します。

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcLic_AZ_Options = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec)
    {
        Left = 1,
        Top = 200,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    signature.Sign(destinFilePath, hibcLic_AZ_Options);
}
```

**説明**： 
- その `QrCodeSignOptions` ここでも Aztec コード タイプで使用されています。
- ポジショニング（`Top`、 `Left`) およびコンテンツ取得設定は QR コードと同様です。

#### トラブルシューティングのヒント

- ファイル パスが正確であることを確認します。
- GroupDocs.Signature のバージョンが Aztec コード タイプをサポートしていることを確認します。

### HIBC LIC DataMatrixで文書に署名する

#### 概要

DataMatrixコードは、データを保存するための堅牢な方法を提供します。このセクションでは、DataMatrixをPDFドキュメントに統合する方法を説明します。

#### 実装手順

##### ステップ1: ファイルパスを設定する

前と同様に、ファイルの保存場所を指定します。

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICDataMatrix");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICDataMatrix.pdf");
```

##### ステップ2: DataMatrix署名オプションを作成する

DataMatrix コードを構成し、適用します。

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcLic_DM_Options = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix)
    {
        Left = 1,
        Top = 400,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    signature.Sign(destinFilePath, hibcLic_DM_Options);
}
```

**説明**： 
- `QrCodeSignOptions` DataMatrix コードの外観と内容を設定するために使用されます。
- ポジショニング（`Top`、 `Left`) および取得設定は、以前のコードと同じパターンに従います。

#### トラブルシューティングのヒント

- すべてのファイル パスが正しく指定されていることを確認します。
- GroupDocs.Signature がお使いのバージョンで DataMatrix コード タイプをサポートしていることを確認します。

### HIBC PAS QRコードで文書に署名する

#### 概要

HIBC PAS QRコードで文書に署名すると、製品の追跡とトレーサビリティが向上します。このセクションでは、GroupDocs.Signatureを使用してPDFにPAS QRコードを埋め込む方法について説明します。

#### 実装手順

##### ステップ1: ソースパスと出力パスを構成する

ソース ドキュメントの場所と署名された出力を保存する場所を定義します。

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCPASQR");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCPASQR.pdf");
```

##### ステップ2：QRコードサインオプションを作成する

特定のテキストと設定で PAS QR コードを構成します。

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcPas_QR_Options = new QrCodeSignOptions("PAS123456789012", QrCodeTypes.HIBCPASQR)
    {
        Left = 1,
        Top = 500,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    // これらのオプションを使用してドキュメントに署名します。
    signature.Sign(destinFilePath, hibcPas_QR_Options);
}
```

**説明**： 
- `QrCodeSignOptions` HIBC PAS QR コード タイプ用に設定され、ドキュメント上に配置されます。
- `ReturnContent` true に設定すると、署名されたドキュメントのレンダリングされた画像が取得されます。

#### トラブルシューティングのヒント

- すべてのパスが正しく指定されていることを確認してください。
- お使いのバージョンで GroupDocs.Signature が PAS QR コード タイプをサポートしていることを確認します。

### 結論

このガイドに従うことで、GroupDocs.Signature for .NETを使用して、HIBC LICおよびPAS QRコードをPDF文書に効率的に統合できます。このプロセスにより、様々な業界において文書のセキュリティ、トレーサビリティ、コンプライアンスが向上します。詳細なカスタマイズと高度な機能については、 [GroupDocsドキュメント](https://docs。groupdocs.com/signature/net/).