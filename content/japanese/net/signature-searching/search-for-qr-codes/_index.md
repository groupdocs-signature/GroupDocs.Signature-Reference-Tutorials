---
"description": "この包括的なステップバイステップ ガイドとコード例を使用して、GroupDocs.Signature for .NET を使用してドキュメント内の QR コードを効率的に検索する方法を学びます。"
"linktitle": "QRコードを検索"
"second_title": "GroupDocs.Signature .NET API"
"title": "ドキュメント内のQRコード署名を検索する"
"url": "/ja/net/signature-searching/search-for-qr-codes/"
"weight": 15
---

## 導入

今日のデジタルドキュメントエコシステムにおいて、QRコード署名は情報の埋め込み、認証、そしてドキュメントセキュリティの強化に欠かせないツールとなっています。GroupDocs.Signature for .NETは、様々な形式のドキュメントからQRコードを検索・抽出するための強力なAPIを開発者に提供し、.NETアプリケーションにおける高度なドキュメント分析・検証機能を実現します。

この包括的なチュートリアルでは、GroupDocs.Signature for .NET を使用して QR コード検索機能を実装するプロセスをガイドし、明確な説明、ステップバイステップの手順、独自のアプリケーションに統合できる実用的なコード例を提供します。

## 前提条件

QR コード署名の検索を始める前に、次の前提条件を満たしていることを確認してください。

1. GroupDocs.Signature for .NET SDK: SDKをダウンロードしてインストールします。 [ダウンロードページ](https://releases。groupdocs.com/signature/net/).

2. 開発環境: .NET Framework または .NET Core がインストールされた Visual Studio などの .NET 開発環境をセットアップします。

3. 基本知識: C# プログラミングと .NET 開発の概念に関する知識。

4. サンプル ドキュメント: 検証およびテスト用の QR コードを含むテスト ドキュメントを準備します。

## 名前空間のインポート

まず、GroupDocs.Signature 機能にアクセスするために必要な名前空間をインポートします。

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;
```

それでは、QR コードを検索するプロセスを、明確でわかりやすい手順に分解してみましょう。

## ステップ1: ドキュメントパスを定義する

まず、検索する QR コードを含むドキュメントへのパスを指定します。

```csharp
string filePath = "sample_multiple_signatures.docx";
```

## ステップ2: 署名オブジェクトの初期化

インスタンスを作成する `Signature` ドキュメントパスを渡してクラスを作成します:

```csharp
using (Signature signature = new Signature(filePath))
{
    // QRコード検索コードがここに追加されます
}
```

## ステップ3: QRコード署名を検索する

使用 `Search` 適切な署名タイプを使用してドキュメント内の QR コードを検索する方法:

```csharp
// 文書内のQRコード署名を検索する
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

## ステップ4: 処理と結果の表示

見つかった QR コード署名を反復処理し、そのプロパティにアクセスします。

```csharp
// 見つかったQRコードに関する情報を表示する
Console.WriteLine($"\nSource document contains {signatures.Count} QR code signature(s):");

foreach (var qrCodeSignature in signatures)
{
    Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
    Console.WriteLine($"Content: {qrCodeSignature.Text}");
    Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
    Console.WriteLine();
}
```

## 完全な例

以下は、ドキュメント内の QR コードを検索する完全なプロセスを示す包括的な実例です。

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;

namespace QrCodeSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // ドキュメントパス - ファイルパスを更新します
            string filePath = "sample_multiple_signatures.docx";
            
            // 署名インスタンスを初期化する
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // 文書内のQRコード署名を検索する
                    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
                    
                    // 検索結果を表示
                    Console.WriteLine($"\nSource document ['{filePath}'] contains {signatures.Count} QR code signature(s):");
                    
                    foreach (var qrCodeSignature in signatures)
                    {
                        Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
                        Console.WriteLine($"Content: {qrCodeSignature.Text}");
                        Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
                        Console.WriteLine();
                    }
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"Error occurred: {ex.Message}");
                }
            }
            
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## 高度なQRコード検索テクニック

### 特定の条件で検索する

よりターゲットを絞った検索には、 `QrCodeSearchOptions` 検索条件をカスタマイズするには:

```csharp
// 特定の条件でQRコード検索オプションを作成する
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    // 特定のページのみを検索する
    AllPages = false,
    PageNumber = 1,
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } },
    
    // QRコードの内容でフィルタリング
    Text = "Invoice",
    MatchType = TextMatchType.Contains,
    
    // 特定のQRコードタイプでフィルタリング
    EncodeType = QrCodeTypes.QR,
    
    // 検索する特定のエリアを定義する
    Rectangle = new Rectangle(100, 100, 400, 400)
};

// 特定のオプションで検索
List<QrCodeSignature> filteredSignatures = signature.Search<QrCodeSignature>(options);
```

### QRコードデータの処理

アプリケーション要件に基づいて、QR コード データのカスタム処理を実装できます。

```csharp
foreach (var qrCode in signatures)
{
    // コンテンツに基づいてQRコードデータを抽出して処理する
    string qrContent = qrCode.Text;
    
    if (qrContent.StartsWith("URL:"))
    {
        // URLデータを処理する
        string url = qrContent.Substring(4);
        Console.WriteLine($"Found URL in QR code: {url}");
    }
    else if (qrContent.StartsWith("CONTACT:"))
    {
        // 連絡先情報の処理
        string contact = qrContent.Substring(8);
        Console.WriteLine($"Found contact information in QR code: {contact}");
    }
    else if (qrContent.StartsWith("INVOICE:"))
    {
        // 請求書情報を処理する
        string invoiceData = qrContent.Substring(8);
        Console.WriteLine($"Found invoice information in QR code: {invoiceData}");
        
        // 請求書データを解析して検証する
        if (ValidateInvoiceData(invoiceData))
        {
            Console.WriteLine("Invoice data is valid!");
        }
        else
        {
            Console.WriteLine("Warning: Invalid invoice data detected!");
        }
    }
}

// 検証方法の例
static bool ValidateInvoiceData(string data)
{
    // 検証ロジックを実装する
    return !string.IsNullOrEmpty(data) && data.Contains("ID") && data.Contains("Amount");
}
```

### セキュリティ検証の実装

QRコードは認証目的でよく使用されます。基本的なセキュリティ検証の実装方法は次のとおりです。

```csharp
// ドキュメントに有効な認証QRコードが含まれているかどうかを確認します
bool hasValidAuthQrCode = false;

foreach (var qrCode in signatures)
{
    if (qrCode.Text.StartsWith("AUTH:"))
    {
        string authCode = qrCode.Text.Substring(5);
        
        // 認証コードを検証する（例：データベースまたは事前定義されたリストと照合）
        if (VerifyAuthCode(authCode))
        {
            hasValidAuthQrCode = true;
            Console.WriteLine("Document contains valid authentication QR code!");
            break;
        }
    }
}

if (!hasValidAuthQrCode)
{
    Console.WriteLine("Warning: Document does not contain a valid authentication QR code!");
}

// 検証方法の例
static bool VerifyAuthCode(string code)
{
    // 検証ロジックを実装する
    // これは、データベース検索、API呼び出し、または事前定義された値との比較である可能性があります。
    return code == "A7B82C3D" || code == "X9Y8Z7W6";
}
```

### QRコード画像の抽出

ドキュメントから QR コード イメージを抽出して、さらに処理したり表示したりできます。

```csharp
// QRコード画像をディスクに保存する
foreach (var qrCode in signatures)
{
    if (qrCode.Content != null)
    {
        // ページ番号と位置に基づいて一意のファイル名を作成します
        string outputPath = $"QrCode_P{qrCode.PageNumber}_X{qrCode.Left}_Y{qrCode.Top}.png";
        
        // 画像データを保存する
        File.WriteAllBytes(outputPath, qrCode.Content);
        Console.WriteLine($"Saved QR code image to {outputPath}");
    }
}
```

## 結論

この包括的なガイドでは、GroupDocs.Signature for .NET を使用してドキュメント内のQRコード署名を検索する方法について解説しました。基本的な検索方法から高度なテクニックまで、.NETアプリケーションで堅牢なQRコード処理を実装するための知識を習得できます。GroupDocs.Signature APIは、QRコードを含む様々な署名タイプを、様々なドキュメント形式で処理するための強力で柔軟なフレームワークを提供します。

これらの機能を利用することで、.NET アプリケーション内でドキュメント検証プロセスを強化し、認証システムを実装し、QR コードに埋め込まれた貴重な情報を抽出することができます。

## よくある質問

### GroupDocs.Signature ではどの QR コード形式がサポートされていますか?

GroupDocs.Signatureは、標準QRコード、マイクロQRコード、その他の一般的なQRコード規格を含む、様々なQRコード形式をサポートしています。特定の形式にアクセスするには、 `EncodeType` の財産 `QrCodeSignature` 物体。

### パスワードで保護された文書内の QR コードを検索できますか?

はい、GroupDocs.Signatureは、初期化時にパスワードを入力することで、パスワードで保護された文書内のQRコードの検索をサポートします。 `Signature` 物体：

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // QRコードを検索する
}
```

### QR コードをその内容に基づいてフィルタリングするにはどうすればよいですか?

コンテンツに基づいてQRコードをフィルタリングすることができます。 `Text` そして `MatchType` の特性 `QrCodeSearchOptions`：

```csharp
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    Text = "Invoice",
    MatchType = TextMatchType.Contains // その他のオプション: Exact、StartsWith、EndsWith
};
```

### GroupDocs.Signature は破損した QR コードや部分的にしか見えない QR コードを検出できますか?

GroupDocs.Signatureは、部分的にしか見えないQRコードもある程度検出できますが、ひどく損傷したQRコードは認識できない場合があります。検出精度は、文書内のQRコードの品質と視認性に依存します。

### QR コード検索ではどのようなドキュメント形式がサポートされていますか?

GroupDocs.Signature は、PDF、Microsoft Office ドキュメント (Word、Excel、PowerPoint)、画像 (JPEG、PNG、TIFF) など、さまざまなドキュメント形式での QR コード検索をサポートしています。

## 参照

* [APIリファレンス](https://reference.groupdocs.com/signature/net/)
* [GitHub のコード例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [製品ドキュメント](https://docs.groupdocs.com/signature/net/)
* [製品ページ](https://products.groupdocs.com/signature/net/)
* [最新バージョンをダウンロード](https://releases.groupdocs.com/signature/net/)
* [ブログ記事](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [無料サポートフォーラム](https://forum.groupdocs.com/c/signature/13)
* [一時ライセンス](https://purchase.groupdocs.com/temporary-license/)