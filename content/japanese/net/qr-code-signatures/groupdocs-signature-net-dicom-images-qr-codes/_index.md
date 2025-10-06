---
"date": "2025-05-07"
"description": "GroupDocs.Signature for .NETを使用して、DICOM画像にQRコードで署名する方法を学びます。このガイドでは、医用画像におけるQRコード署名の設定、実装、検証について説明します。"
"title": "GroupDocs.Signature for .NET を使用して DICOM 画像に QR コードで署名する方法 - 総合ガイド"
"url": "/ja/net/qr-code-signatures/groupdocs-signature-net-dicom-images-qr-codes/"
"weight": 1
type: docs
---
# GroupDocs.Signature for .NET を使用して DICOM 画像に QR コードで署名する方法: 総合ガイド

DICOMファイルを安全に認証する方法をお探しですか？この詳細なガイドでは、GroupDocs.Signature for .NETを使用してDICOM画像にQRコード署名を統合する方法を説明します。医療従事者、開発者、そしてデジタル医療文書を扱うすべての方に最適なこのチュートリアルでは、セットアップから実装までを網羅しています。

## 学習内容:
- GroupDocs.Signature for .NET を使用して開発環境をセットアップします。
- QR コードを使用して DICOM 画像に署名するための手順を説明します。
- DICOM ファイル内の QR コード署名を検証および検索する方法。
- レビュー目的で署名済みドキュメントのプレビューを生成する手法。
- パフォーマンスを最適化し、リソースを効果的に管理するためのベスト プラクティス。

まずは前提条件から始めましょう！

## 前提条件

GroupDocs.Signature for .NET を使用するには、環境の準備が整っていることを確認してください。必要なものは以下のとおりです。

### 必要なライブラリとバージョン
- **.NET 用 GroupDocs.Signature**.NET フレームワークとの互換性を確保します。

### 環境設定要件
- Windows または Linux 上の開発環境。
- Visual Studio または他の .NET 互換 IDE がインストールされています。

### 知識の前提条件
- C# プログラミングの基本的な理解。
- .NET アプリケーションにおけるファイル I/O に関する知識。

## GroupDocs.Signature を .NET 用にセットアップする

好みの方法で GroupDocs.Signature ライブラリをインストールします。

**.NET CLI の使用:**
```bash
dotnet add package GroupDocs.Signature
```

**パッケージマネージャー:**
```powershell
Install-Package GroupDocs.Signature
```

**NuGet パッケージ マネージャー UI:**
- 「GroupDocs.Signature」を検索し、最新バージョンをインストールしてください。

### ライセンス取得

まずは無料トライアルで機能をご確認ください。さらに長期間ご利用いただくには、一時ライセンスまたはフルライセンスのご購入をご検討ください。 [グループドキュメント](https://purchase。groupdocs.com/buy).

インストールしたら、ライブラリを初期化します。

```csharp
using GroupDocs.Signature;
// DICOM ファイル パスを使用して Signature オブジェクトを初期化します。
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample.dicom");
```

## 実装ガイド

### QRコードでDICOM画像に署名する

#### 概要
QR コード署名を追加して、医療文書の信頼性と追跡可能性を確保します。

**ステップ1: 署名オブジェクトの初期化**

```csharp
string filePath = "YOUR_DOCUMENT_DIRECTORY\\sample.dicom";
using (Signature signature = new Signature(filePath))
{
    // 署名操作を続行します...
}
```

**ステップ2：QRコードサインオプションを作成する**

テキスト、サイズ、配置などのプロパティを構成します。

```csharp
QrCodeSignOptions options = new QrCodeSignOptions("Patient #36363393. R: No-Issues")
{
    AllPages = true,
    Width = 100,
    Height = 100,
    VerticalAlignment = VerticalAlignment.Bottom,
    HorizontalAlignment = HorizontalAlignment.Right,
    Margin = new Padding() { Right = 5, Left = 5 }
};
```

**ステップ3: XMPメタデータを追加する**

追加のメタデータを使用してドキュメントを強化します。

```csharp
DicomSaveOptions dicomSaveOptions = new DicomSaveOptions()
{
    XmpEntries = new List<DicomXmpEntry>() { new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4") }
};
```

**ステップ4：文書に署名する**

署名を実行して保存します。

```csharp
SignResult signResult = signature.Sign("YOUR_OUTPUT_DIRECTORY\\SignedDicom", options, dicomSaveOptions);
```

### ドキュメント情報を取得

署名された DICOM ファイルからメタデータを取得して、データの整合性を確保します。

**概要：**
検証のためにドキュメント情報と XMP メタデータ署名にアクセスします。

**ステップ1: ドキュメント情報を取得する**

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    IDocumentInfo signedDocumentInfo = signature.GetDocumentInfo();
}
```

**ステップ2: XMPデータの反復処理と印刷**

メタデータの詳細を表示します。

```csharp
foreach (var item in signedDocumentInfo.MetadataSignatures)
{
    Console.WriteLine(item.ToString());
}
```

### DICOM署名の検証

DICOM 画像内の QR コード署名の信頼性を検証します。

**概要：**
署名が正しく本物であることを確認します。

**ステップ1: QRコード検証オプションを作成する**

QR コード内の特定のテキストに一致するオプションを設定します。

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true,
    Text = "Patient #36363393",
    MatchType = TextMatchType.Contains
};
```

**ステップ2: 署名を検証する**

署名が基準を満たしているかどうかを確認します。

```csharp
VerificationResult result = signature.Verify(options);

if (result.IsValid)
{
    Console.WriteLine($"DICOM {filePath} has {result.Succeeded.Count} successfully verified signatures!");
}
```

### DICOM で署名を検索する

署名された DICOM 画像内で QR コード署名を見つけます。

**概要：**
すべての QR コード署名を効率的に見つけて、ドキュメントの信頼性を管理します。

**ステップ1: QRコード署名を検索する**

```csharp
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

**ステップ2: 署名の詳細を繰り返して印刷する**

見つかった各署名の詳細を確認します。

```csharp
foreach (var QrCodeSignature in signatures)
{
    Console.WriteLine($"QRCode signature found at page {QrCodeSignature.PageNumber} with type {QrCodeSignature.EncodeType.TypeName} and text {QrCodeSignature.Text}");
}
```

### 署名されたDICOMのプレビューを生成する

検証用の視覚的なプレビューを作成します。

**概要：**
専用のソフトウェアを使用せずにコンテンツを確認するための画像プレビューを生成します。

**ステップ1: ストリームメソッドを定義する**

プレビュー生成中にファイル ストリームを管理する方法を設定します。

```csharp
Stream CreatePageStream(PreviewPageData pageData)
{
    string imageFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignDicomImageAdvanced", $"preview-{pageData.PageNumber}.jpg");
    var folder = Path.GetDirectoryName(imageFilePath);
    if (!Directory.Exists(folder))
    {
        Directory.CreateDirectory(folder);
    }
    return new FileStream(imageFilePath, FileMode.Create);
}

void ReleasePageStream(PreviewPageData pageData, Stream pageStream)
{
    pageStream.Dispose();
}
```

**ステップ2: プレビューを生成する**

プレビュー生成プロセスを実行します。

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    PreviewOptions previewOption = new PreviewOptions(CreatePageStream, ReleasePageStream)
    {
        PreviewFormat = PreviewOptions.PreviewFormats.PNG,
    };

    signature.GeneratePreview(previewOption);
}
```

## 実用的な応用

1. **医療記録管理**コンプライアンスのために QR コード署名を使用して患者記録を認証します。
2. **医療システムにおける監査証跡**QR コードを使用してドキュメントの変更を追跡し、信頼性を検証します。
3. **安全なデータ共有**デジタル署名を埋め込むことで医療画像の安全な共有を実現します。
4. **コンプライアンス検証**法的要件を満たすために、DICOM ファイルの整合性を定期的に検証します。
5. **EHRシステムとの統合**署名された DICOM ファイルを電子健康記録 (EHR) システムにシームレスに統合し、操作を効率化します。