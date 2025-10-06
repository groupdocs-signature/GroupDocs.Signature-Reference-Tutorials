---
"description": "GroupDocs.Signature for .NET を使用して、ドキュメント内の複数の署名タイプを検索する方法を学びます。ドキュメントのセキュリティを強化するためのコード例を含む包括的なガイドです。"
"linktitle": "複数の署名を検索する"
"second_title": "GroupDocs.Signature .NET API"
"title": "文書内の複数の署名タイプを検索する"
"url": "/ja/net/signature-searching/search-for-multiple-signatures/"
"weight": 14
type: docs
---
## 導入

現代のドキュメント管理システムでは、単一のドキュメント内で複数の署名タイプを検索・検証する機能がますます重要になっています。組織では、ドキュメントのセキュリティを強化し、検証プロセスを効率化するために、デジタル署名、テキスト署名、バーコード、QRコードなど、様々な署名タイプを採用することがよくあります。GroupDocs.Signature for .NETは、開発者が様々なドキュメント形式に対応する包括的な署名検索機能を実装できる強力なフレームワークを提供します。

このチュートリアルでは、GroupDocs.Signature for .NET を使用してドキュメント内の複数の署名タイプを検索するプロセスを、詳細な説明と実用的なコード例とともに説明します。

## 前提条件

複数の署名検索機能の実装に取り掛かる前に、次の前提条件が満たされていることを確認してください。

1. 開発環境: システムにインストールされている Visual Studio または任意の推奨 .NET 開発環境。
  
2. GroupDocs.Signature for .NET: GroupDocs.Signature for .NETライブラリを以下のサイトからダウンロードしてインストールします。 [ここ](https://releases。groupdocs.com/signature/net/).

3. 基本的な C# の知識: C# プログラミング言語と .NET フレームワークの概念に関する知識。

4. サンプル ドキュメント: テスト目的でさまざまな種類の署名を含むテスト ドキュメントを準備します。

## 名前空間のインポート

まず、GroupDocs.Signature 機能にアクセスするために必要な名前空間をインポートします。

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

ここで、複数の署名タイプを検索するプロセスを、明確で管理しやすい手順に分解してみましょう。

## ステップ1：ドキュメントを読み込む

まず、検索する署名を含むドキュメントを読み込みます。

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // マルチ署名検索コードがここに追加されます
}
```

## ステップ2: さまざまな署名タイプの検索オプションを定義する

検索する署名の種類ごとに検索オプションを作成します。

```csharp
// テキスト署名の検索オプションを定義する
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,  // すべてのページを検索
    Text = "Signature",  // オプション: 検索するテキスト
    MatchType = TextMatchType.Contains  // 一致基準
};

// デジタル署名の検索オプションを定義する
DigitalSearchOptions digitalOptions = new DigitalSearchOptions
{
    AllPages = true
};

// バーコード署名の検索オプションを定義する
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
{
    AllPages = true,
    Text = "123456",  // オプション: 一致するバーコードテキスト
    MatchType = TextMatchType.Exact  // 一致基準
};

// QRコード署名の検索オプションを定義する
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
{
    AllPages = true,
    Text = "John",  // オプション: 一致するQRコードテキスト
    MatchType = TextMatchType.Contains  // 一致基準
};

// メタデータ署名の検索オプションを定義する
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```

## ステップ3: コレクションにオプションを追加する

すべての検索オプションをコレクションに追加します。

```csharp
// すべての検索オプションを保持するリストを作成する
List<SearchOptions> searchOptions = new List<SearchOptions>
{
    textOptions,
    digitalOptions,
    barcodeOptions,
    qrCodeOptions,
    metadataOptions
};
```

## ステップ4: 検索を実行し、結果を処理する

組み合わせた検索オプションを使用して検索を実行し、結果を処理します。

```csharp
// 定義されたオプションを使用してすべての署名タイプを検索します
SearchResult result = signature.Search(searchOptions);

// 署名が見つかったかどうかを確認する
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
    
    // 見つかった署名を反復処理する
    foreach (var foundSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}, ID: {foundSignature.SignatureId}");
        
        // プロセス固有の署名タイプ
        if (foundSignature is TextSignature textSignature)
        {
            Console.WriteLine($"Text: '{textSignature.Text}'");
        }
        else if (foundSignature is BarcodeSignature barcodeSignature)
        {
            Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
        }
        else if (foundSignature is QrCodeSignature qrCodeSignature)
        {
            Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
        }
        else if (foundSignature is DigitalSignature digitalSignature)
        {
            Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
        }
        else if (foundSignature is MetadataSignature metadataSignature)
        {
            Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
        }
    }
}
else
{
    Console.WriteLine("No signatures were found in the document.");
}
```

## 完全な例

以下は、ドキュメント内の複数の署名タイプを検索する完全な動作例です。

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace MultiSignatureSearch
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
                try
                {
                    // テキスト署名の検索オプションを定義する
                    TextSearchOptions textOptions = new TextSearchOptions
                    {
                        AllPages = true,
                        MatchType = TextMatchType.Contains
                    };

                    // デジタル署名の検索オプションを定義する
                    DigitalSearchOptions digitalOptions = new DigitalSearchOptions
                    {
                        AllPages = true
                    };

                    // バーコード署名の検索オプションを定義する
                    BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
                    {
                        AllPages = true
                    };

                    // QRコード署名の検索オプションを定義する
                    QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
                    {
                        AllPages = true
                    };

                    // メタデータ署名の検索オプションを定義する
                    MetadataSearchOptions metadataOptions = new MetadataSearchOptions();

                    // すべての検索オプションを保持するリストを作成する
                    List<SearchOptions> searchOptions = new List<SearchOptions>
                    {
                        textOptions,
                        digitalOptions,
                        barcodeOptions,
                        qrCodeOptions,
                        metadataOptions
                    };

                    // すべての署名タイプを検索
                    SearchResult result = signature.Search(searchOptions);

                    // 署名が見つかったかどうかを確認する
                    if (result.Signatures.Count > 0)
                    {
                        Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
                        
                        // 署名タイプ別の処理結果
                        foreach (var foundSignature in result.Signatures)
                        {
                            Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}");
                            
                            // プロセス固有の署名タイプ
                            switch (foundSignature.SignatureType)
                            {
                                case SignatureType.Text:
                                    var textSignature = foundSignature as TextSignature;
                                    Console.WriteLine($"Text: '{textSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Barcode:
                                    var barcodeSignature = foundSignature as BarcodeSignature;
                                    Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.QrCode:
                                    var qrCodeSignature = foundSignature as QrCodeSignature;
                                    Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Digital:
                                    var digitalSignature = foundSignature as DigitalSignature;
                                    Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
                                    break;
                                    
                                case SignatureType.Metadata:
                                    var metadataSignature = foundSignature as MetadataSignature;
                                    Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
                                    break;
                            }
                            
                            Console.WriteLine(); // 署名の間に改行を追加する
                        }
                    }
                    else
                    {
                        Console.WriteLine("No signatures were found in the document.");
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

## 高度なマルチ署名検索技術

### 検索結果のフィルタリング

高度なフィルタリングを実装して検索結果を絞り込むことができます。

```csharp
// ページ番号で結果をフィルタリング
var signaturesOnFirstPage = result.Signatures.FindAll(s => s.PageNumber == 1);

// 署名の種類で結果をフィルタリングする
var digitalSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.Digital);
var qrCodeSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.QrCode);

// 特定のコンテンツを含むテキスト署名をフィルタリングする
var approvalSignatures = result.Signatures
    .FindAll(s => s is TextSignature && ((TextSignature)s).Text.Contains("Approved"));
```

### 複数の署名の検証

さまざまな署名タイプに対する検証ロジックを実装します。

```csharp
bool ValidateAllSignatures(SearchResult result)
{
    bool isDocumentValid = true;
    
    // 文書に有効なデジタル署名があるかどうかを確認する
    bool hasValidDigitalSignature = result.Signatures
        .Any(s => s is DigitalSignature && ((DigitalSignature)s).IsValid);
    
    if (!hasValidDigitalSignature)
    {
        Console.WriteLine("Warning: Document does not contain a valid digital signature");
        isDocumentValid = false;
    }
    
    // ドキュメントに必要なQRコードがあるかどうかを確認する
    bool hasRequiredQRCode = result.Signatures
        .Any(s => s is QrCodeSignature && ((QrCodeSignature)s).Text.Contains("Auth-Code"));
    
    if (!hasRequiredQRCode)
    {
        Console.WriteLine("Warning: Document does not contain the required authentication QR code");
        isDocumentValid = false;
    }
    
    return isDocumentValid;
}
```

### カスタム処理による検索

検索操作のカスタム処理ロジックを定義できます。

```csharp
// カスタム処理で検索オプションを作成する
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,
    
    // デリゲートを使用してカスタム処理を定義する
    ProcessCompleted = (signature) =>
    {
        // カスタム検証ロジック - 指定されたページの署名のみを受け入れる
        TextSignature textSignature = signature as TextSignature;
        return textSignature != null && (textSignature.PageNumber == 1 || textSignature.PageNumber == 2);
    }
};
```

## 結論

この包括的なガイドでは、GroupDocs.Signature for .NET を使用してドキュメント内の複数の署名タイプを検索する方法について説明しました。異なる署名タイプに対する検索オプションの設定から結果の処理と検証まで、.NETアプリケーションに堅牢な署名検索機能を実装するための知識が得られます。

複数の署名タイプを同時に検索できる機能により、ドキュメント検証プロセスが強化され、セキュリティ対策が強化され、ドキュメント検証ワークフローが効率化されます。GroupDocs.Signatureは、様々なドキュメント形式にわたる様々な署名タイプを扱うための強力で柔軟なフレームワークを提供し、ドキュメント処理アプリケーションに最適です。

## よくある質問

### パスワードで保護された文書内の署名を検索できますか?

はい、GroupDocs.Signatureはパスワードで保護された文書内の署名の検索をサポートしています。初期化時にパスワードを入力してください。 `Signature` 物体：

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // 署名を検索する
}
```

### 署名検索ではどのドキュメント形式がサポートされていますか?

GroupDocs.Signature は、PDF、Microsoft Office ドキュメント (Word、Excel、PowerPoint)、OpenOffice 形式、画像など、幅広いドキュメント形式をサポートしています。

### ドキュメント内の特定のページに検索を制限できますか?

はい、各検索オプション タイプには、検索するページを指定できるプロパティがあります。

```csharp
TextSearchOptions options = new TextSearchOptions
{
    AllPages = false,  // すべてのページを検索しない
    PageNumber = 1,    // 1ページ目のみ検索
    
    // または複数のページを指定
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } }
};
```

### 大きなドキュメントを検索するときにパフォーマンスを最適化するにはどうすればよいでしょうか?

大きなドキュメントの場合は、次の方法でパフォーマンスを最適化できます。

1. 特定のページまたはページ範囲に検索を制限する
2. より具体的な検索条件を使用して、一致する可能性のある数を減らす
3. 結果表示にページ区切りを実装する
4. 同時に結果を取得する必要がない場合は、一度に 1 つの署名タイプを検索する

### GroupDocs.Signature を拡張してカスタム署名タイプをサポートできますか?

GroupDocs.Signature は一般的な署名タイプに対する組み込みサポートを提供しますが、次の方法で機能を拡張できます。

1. 派生したカスタム検索オプションクラスの作成 `SearchOptions`
2. カスタム処理ロジックを実装するには、 `ProcessCompleted` 代表者
3. 複数のシグネチャ検索と高度なビジネスロジックを組み合わせたラッパークラスの開発

## 参照

* [APIリファレンス](https://reference.groupdocs.com/signature/net/)
* [GitHub のコード例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [製品ドキュメント](https://docs.groupdocs.com/signature/net/)
* [製品ページ](https://products.groupdocs.com/signature/net/)
* [最新バージョンをダウンロード](https://releases.groupdocs.com/signature/net/)
* [ブログ記事](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [無料サポートフォーラム](https://forum.groupdocs.com/c/signature/13)
* [一時ライセンス](https://purchase.groupdocs.com/temporary-license/)