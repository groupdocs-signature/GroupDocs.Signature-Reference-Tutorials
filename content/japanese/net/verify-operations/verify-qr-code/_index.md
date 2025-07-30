---
"description": "GroupDocs.Signature for .NETを使用してドキュメント内のQRコードを検証する方法を学びましょう。ドキュメント認証のためのコード例とベストプラクティスを網羅した完全なガイドです。"
"linktitle": "QRコードを確認する"
"second_title": "GroupDocs.Signature .NET API"
"title": "文書内のQRコードを検証する"
"url": "/ja/net/verify-operations/verify-qr-code/"
"weight": 12
---

## 導入

ドキュメントのセキュリティは、現代のビジネスオペレーションにおいて極めて重要です。QRコードは、ドキュメント内に情報を埋め込んで真正性を検証する方法として、ますます普及しています。GroupDocs.Signature for .NETは、様々な形式のドキュメントに埋め込まれたQRコードを検証するための、強力で柔軟なソリューションを提供します。

この包括的なチュートリアルでは、.NET アプリケーションに QR コード検証を実装し、ドキュメントの整合性と信頼性を維持するプロセスについて説明します。

## 前提条件

QR コード検証機能を実装する前に、次の前提条件が満たされていることを確認してください。

1. GroupDocs.Signature for .NET: ライブラリをダウンロードしてインストールします。 [ダウンロードページ](https://releases。groupdocs.com/signature/net/).
2. 開発環境: Visual Studio または互換性のある .NET 開発環境。
3. テスト ドキュメント: 検証目的で QR コード署名を含むドキュメント。
4. 基本知識: C# プログラミングと .NET Framework の概念に関する知識。

## 名前空間のインポート

まず、GroupDocs.Signature 機能にアクセスするために必要な名前空間をインポートします。

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## QRコード検証の手順

ドキュメント内の QR コードを検証するには、次の詳細な手順に従ってください。

### ステップ1: ドキュメントパスを指定する

```csharp
// QRコード署名を含むドキュメントへのパスを指定します
string filePath = "sample_multiple_signatures.docx";
```

必ず、例のパスをドキュメントへの実際のパスに置き換えてください。

### ステップ2: 署名オブジェクトの初期化

```csharp
// ドキュメントパスを渡してSignatureインスタンスを作成する
using (Signature signature = new Signature(filePath))
{
    // 検証コードはここに実装されます
}
```

Signature クラスは、GroupDocs.Signature API のすべての操作のメイン エントリ ポイントです。

### ステップ3: QRコード検証オプションを設定する

```csharp
// QRコード検証オプションを定義する
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true, // 文書の全ページをチェックする
    Text = "John",   // QRコード内の検証テキスト
    MatchType = TextMatchType.Contains // テキスト一致基準を指定する
};
```

検証オプションを使用すると、検証プロセスの特定の基準を定義できます。
- `AllPages`: すべてのドキュメントページをチェックするには true に設定します (デフォルトの動作)
- `Text`: QRコード内で一致するテキストコンテンツ
- `MatchType`テキスト一致の方法 (Contains、Exact、StartsWith など)

### ステップ4: 検証プロセスを実行する

```csharp
// 検証を実行する
VerificationResult result = signature.Verify(options);
```

これにより、指定したオプションに基づいて検証プロセスが実行されます。

### ステップ5：プロセス検証結果

```csharp
// 検証結果を確認し、それに応じて処理する
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid QR code signature!");
    
    // 成功した署名に関する情報を表示する
    foreach (QrCodeSignature signature in result.Succeeded)
    {
        Console.WriteLine($"Found valid QR Code signature with text: {signature.Text}");
        Console.WriteLine($"QR Code type: {signature.EncodeType.TypeName}");
        Console.WriteLine($"Location: Page {signature.PageNumber}, {signature.Left}x{signature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

検証結果を適切に処理することで、アプリケーションは検証結果に基づいて適切なアクションを実行できるようになります。

## 完全な例

QR コード検証を示す完全な動作例を次に示します。

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace GroupDocs.Signature.Examples
{
    class Program
    {
        static void Main(string[] args)
        {
            // ドキュメントパス
            string filePath = "sample_multiple_signatures.docx";
            
            // 署名インスタンスを初期化する
            using (Signature signature = new Signature(filePath))
            {
                // セットアップ検証オプション
                QrCodeVerifyOptions options = new QrCodeVerifyOptions()
                {
                    AllPages = true,
                    Text = "John",
                    MatchType = TextMatchType.Contains
                };
                
                // 文書の署名を検証する
                VerificationResult result = signature.Verify(options);
                
                // プロセス検証結果
                if (result.IsValid)
                {
                    Console.WriteLine($"Document {filePath} contains valid QR code signature!");
                    
                    foreach (QrCodeSignature qrSignature in result.Succeeded)
                    {
                        Console.WriteLine($"Found valid QR Code with text: {qrSignature.Text}");
                    }
                }
                else
                {
                    Console.WriteLine($"Document {filePath} failed verification process.");
                }
            }
        }
    }
}
```

## 高度な検証オプション

GroupDocs.Signature は、より複雑な検証シナリオ向けに追加のオプションを提供します。

### 特定のQRコードタイプの検証

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    EncodeType = QrCodeTypes.QR,  // 標準QRコードのみ検証する
    Text = "Confidential",
    MatchType = TextMatchType.Exact
};
```

### 特定のページでの確認

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = false,
    PageNumber = 2,  // 2ページ目のみ確認
    Text = "Approved"
};
```

### 検証のための正規表現の使用

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    Text = "INV-\\d{6}",  // 請求書番号を一致させる（例：INV-123456）
    MatchType = TextMatchType.Regex
};
```

## QRコード検証のベストプラクティス

1. 入力を常に検証する: 処理する前に、ドキュメント パスと検証基準が有効であることを確認します。
2. エラー処理を実装する: 検証中に発生する可能性のある例外を処理するには、try-catch ブロックを使用します。
3. パフォーマンスを考慮する: 大きなドキュメントの場合は、ドキュメント全体ではなく特定のページを検証することを検討してください。
4. 検証結果をログに記録する: 監査の目的で検証プロセスのログを保持します。
5. さまざまなドキュメント形式でテストする: 必要なすべてのドキュメント形式で検証が機能することを確認します。

## 結論

ドキュメント内のQRコードの検証は、ドキュメントの真正性と整合性を確保する上で不可欠です。GroupDocs.Signature for .NETは、.NETアプリケーションにQRコード検証を実装するための包括的でユーザーフレンドリーなAPIを提供します。

このチュートリアルでは、次の方法を学習しました。
- 検証プロセスを構成して初期化する
- さまざまな検証基準を指定する
- 検証結果の処理と解釈
- 高度な検証オプションを実装する

この知識により、ドキュメント管理システムのセキュリティと信頼性を強化できます。

## よくある質問

### GroupDocs.Signature は、1 つのドキュメント内の複数の QR コードを検証できますか?
はい、GroupDocs.Signatureは1つの文書内の複数のQRコードを検証できます。検証結果には、一致するすべてのQRコードが含まれます。

### QR コード検証ではどのドキュメント形式がサポートされていますか?
GroupDocs.Signature は、PDF、Word (DOC、DOCX)、Excel (XLS、XLSX)、PowerPoint (PPT、PPTX)、画像など、幅広いドキュメント形式をサポートしています。

### 特定の暗号化またはフォーマットを持つ QR コードを検証できますか?
はい、GroupDocs.Signature には、特定のエンコード タイプとコンテンツ フォーマット パターンを使用して QR コードを検証するオプションが用意されています。

### サードパーティアプリケーションで作成されたQRコードを検証することは可能ですか?
はい、GroupDocs.Signature は、標準の QR コード形式に従っている限り、ほとんどのアプリケーションで生成された標準の QR コードを検証できます。

### テキストではなくバイナリデータを含む QR コードをどのように処理すればよいですか?
GroupDocs.Signatureは、バイナリデータでQRコードを検証するためのオプションを提供します。 `BinaryData` 検証オプションのプロパティ。

### 関連リソース
* [GroupDocs.Signature API リファレンス](https://reference.groupdocs.com/signature/net/)
* [GroupDocs.Signature ダウンロード](https://releases.groupdocs.com/signature/net/)
* [GitHub のコード例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [ドキュメント](https://docs.groupdocs.com/signature/net/)
* [製品ページ](https://products.groupdocs.com/signature/net/)
* [ブログ記事](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [サポートフォーラム](https://forum.groupdocs.com/c/signature/13)
* [一時ライセンス](https://purchase.groupdocs.com/temporary-license/)