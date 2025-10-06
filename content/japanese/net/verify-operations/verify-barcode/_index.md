---
"description": "GroupDocs.Signatureを使用して、.NETアプリケーションに堅牢なバーコード検証を実装します。ドキュメントの真正性を確保するための完全なコード例とベストプラクティスをご紹介します。"
"linktitle": "バーコード検証"
"second_title": "GroupDocs.Signature .NET API"
"title": "文書内のバーコード署名を検証する"
"url": "/ja/net/verify-operations/verify-barcode/"
"weight": 10
type: docs
---
## 導入

バーコードは現代のドキュメント管理システムに不可欠な要素となり、エンコードされた情報への迅速なアクセスを可能にすると同時に、セキュリティ機能としても機能します。GroupDocs.Signature for .NETは、ドキュメント内のバーコード署名を検証し、その真正性と整合性を保証するための強力なAPIを提供します。

この包括的なチュートリアルでは、GroupDocs.Signatureを使用して.NETアプリケーションにバーコード検証を実装するプロセスを解説します。ビジネス文書、証明書、契約書など、バーコードを認証に利用するあらゆる種類の文書を扱う場合でも、このガイドは堅牢な検証機能を実装するのに役立ちます。

## 前提条件

バーコード検証機能を実装する前に、次の前提条件が満たされていることを確認してください。

1. GroupDocs.Signature for .NET: ライブラリをダウンロードしてインストールします。 [ダウンロードページ](https://releases。groupdocs.com/signature/net/).
2. .NET 開発環境: Visual Studio または互換性のある .NET 開発環境。
3. 基本知識: C# プログラミングと .NET Framework の概念に関する知識。
4. テスト ドキュメント: 検証目的でバーコード署名を含むドキュメント。

## 必要な名前空間をインポートする

まず、GroupDocs.Signature 機能にアクセスするために必要な名前空間をインポートします。

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

バーコード検証プロセスを明確で管理しやすいステップに分解してみましょう。

## ステップ1: ドキュメントパスを指定する

```csharp
// バーコード署名を含む文書へのパス
string filePath = "sample_multiple_signatures.docx";
```

例のパスを、バーコード署名を含むドキュメントへの実際のパスに置き換えてください。

## ステップ2: 署名オブジェクトの初期化

```csharp
// ドキュメントパスを渡してSignatureクラスのインスタンスを作成する
using (Signature signature = new Signature(filePath))
{
    // 検証コードはここに実装されます
}
```

Signature クラスは、GroupDocs.Signature API のすべての操作のメイン エントリ ポイントです。

## ステップ3: バーコード検証オプションを構成する

```csharp
// バーコード検証オプションを定義する
BarcodeVerifyOptions options = new BarcodeVerifyOptions()
{
    AllPages = true,           // 文書の全ページをチェックする
    Text = "12345",            // バーコード内で一致するテキスト
    MatchType = TextMatchType.Contains // テキスト一致基準を指定する
};
```

検証オプションを使用すると、検証プロセスの特定の基準を定義できます。
- `AllPages`: すべてのドキュメントページをチェックするにはtrueに設定します
- `Text`バーコード内で一致するテキストコンテンツ
- `MatchType`テキストマッチングの方法（Contains、Exact、StartsWith、EndsWith）

## ステップ4: 検証プロセスを実行する

```csharp
// 検証を実行する
VerificationResult result = signature.Verify(options);
```

これにより、指定したオプションに基づいて検証プロセスが実行されます。

## ステップ5：プロセス検証結果

```csharp
// 検証結果を確認し、それに応じて処理する
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid barcode signatures!");
    
    // 成功した署名に関する情報を表示する
    foreach (BarcodeSignature barcodeSignature in result.Succeeded)
    {
        Console.WriteLine($"\nFound valid barcode signature:");
        Console.WriteLine($"Text: {barcodeSignature.Text}");
        Console.WriteLine($"Type: {barcodeSignature.EncodeType.TypeName}");
        Console.WriteLine($"Location: Page {barcodeSignature.PageNumber}, {barcodeSignature.Left}x{barcodeSignature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

このコードは、検証が成功したかどうかを確認し、検証されたバーコード署名に関する詳細情報を提供します。

## 完全な例

以下はバーコード検証を示す完全な動作例です。

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
            
            try
            {
                // 署名インスタンスを初期化する
                using (Signature signature = new Signature(filePath))
                {
                    // セットアップ検証オプション
                    BarcodeVerifyOptions options = new BarcodeVerifyOptions()
                    {
                        AllPages = true,
                        Text = "12345",
                        MatchType = TextMatchType.Contains
                    };
                    
                    // 文書の署名を検証する
                    VerificationResult result = signature.Verify(options);
                    
                    // プロセス検証結果
                    if (result.IsValid)
                    {
                        Console.WriteLine($"Document {filePath} contains valid barcode signatures!");
                        
                        foreach (BarcodeSignature item in result.Succeeded)
                        {
                            Console.WriteLine($"\nValid signature found with text: {item.Text}");
                            Console.WriteLine($"Barcode type: {item.EncodeType.TypeName}");
                            Console.WriteLine($"Page: {item.PageNumber}");
                        }
                    }
                    else
                    {
                        Console.WriteLine($"\nDocument {filePath} failed verification process.");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
            }
        }
    }
}
```

## 高度な検証シナリオ

GroupDocs.Signature は、より複雑な検証シナリオ向けに追加のオプションを提供します。

### 特定のバーコードタイプの検証

探しているバーコードの種類がわかっている場合は、その種類に検証を制限できます。

```csharp
BarcodeVerifyOptions options = new BarcodeVerifyOptions()
{
    EncodeType = BarcodeTypes.Code128,  // Code128バーコードのみを検証する
    Text = "PROD-12345",
    MatchType = TextMatchType.Exact
};
```

### 特定のページのバーコードの検証

複数ページのドキュメントの場合、検証を特定のページに制限できます。

```csharp
BarcodeVerifyOptions options = new BarcodeVerifyOptions()
{
    AllPages = false,
    PageNumber = 2,  // 2ページ目のみ確認
    Text = "INV-2023"
};
```

### 検証のための正規表現の使用

より柔軟なパターン マッチングを行うには、正規表現を使用できます。

```csharp
BarcodeVerifyOptions options = new BarcodeVerifyOptions()
{
    Text = "INV-\\d{4}-\\d{2}",  // INV-2023-01のような請求書番号を一致させる
    MatchType = TextMatchType.Regex
};
```

### 複数のバーコードタイプを同時に検証

さまざまなバーコード タイプをチェックするために、複数の検証オプションを作成できます。

```csharp
// 検証オプションのリストを作成する
List<VerifyOptions> listOptions = new List<VerifyOptions>();

// QRコード認証を追加
listOptions.Add(new BarcodeVerifyOptions()
{
    EncodeType = BarcodeTypes.QR,
    Text = "Security"
});

// Code128認証を追加
listOptions.Add(new BarcodeVerifyOptions()
{
    EncodeType = BarcodeTypes.Code128,
    Text = "12345"
});

// 複数のオプションで検証する
VerificationResult result = signature.Verify(listOptions);
```

## バーコード検証のベストプラクティス

1. エラー処理: 予期しないシナリオを適切に管理するために、常に適切なエラー処理を実装します。
2. パフォーマンスの最適化: 大きなドキュメントの場合は、ドキュメント全体ではなく特定のページを検証することを検討してください。
3. ログ記録: 監査の目的で検証の試行と結果を追跡するためのログ記録を実装します。
4. セキュリティに関する考慮事項: 検証基準がセキュリティ インフラストラクチャの一部である場合は特に、検証基準を安全に保存します。
5. テスト: さまざまなドキュメント形式とバーコード タイプで検証をテストし、互換性を確認します。

## 一般的な問題のトラブルシューティング

### バーコードが検出されません
- 文書内でバーコードがはっきりと見えることを確認してください
- バーコードタイプがGroupDocs.Signatureでサポートされているかどうかを確認します
- バーコードが歪んでいたり破損していないことを確認してください

### 検証の失敗
- 検証基準（テキスト、バーコードの種類）が正しいことを確認します
- MatchType がユースケースに適しているかどうかを確認します
- バーコードが適用されてから文書が変更されていないことを確認します

### パフォーマンスの問題
- バーコードが期待される特定のページをターゲットにして検証を最適化します
- 事前にわかっている場合は、特定のバーコードタイプに検証を制限する

## 結論

バーコード検証は、現代のドキュメント管理システムにおいて、ドキュメントの真正性と整合性を確保するために不可欠なツールです。GroupDocs.Signature for .NETは、.NETアプリケーションに堅牢なバーコード検証機能を実装するための包括的で使いやすいAPIを提供します。

このステップバイステップのガイドに従うことで、次の方法を学習しました。
- 検証プロセスを構成して初期化する
- さまざまな検証基準を指定する
- 検証結果の処理と解釈
- 高度な検証シナリオを実装する

これらの機能により、さまざまなドキュメント形式にわたってバーコードの信頼性を検証できる、安全で信頼性の高いドキュメント処理システムを構築できます。

## よくある質問

### バーコード検証ではどのドキュメント形式がサポートされていますか?
GroupDocs.Signature は、PDF、Word 文書 (DOC、DOCX)、Excel スプレッドシート (XLS、XLSX)、PowerPoint プレゼンテーション (PPT、PPTX)、画像など、幅広いドキュメント形式をサポートしています。

### GroupDocs.Signature は単一のドキュメント内の複数のバーコードを検証できますか?
はい、GroupDocs.Signatureは1つの文書内の複数のバーコードを検証できます。検証結果には、一致するすべてのバーコードが含まれます。

### 検証にサポートされているバーコードの種類は何ですか?
GroupDocs.Signature は、Code39、Code128、EAN13、EAN8、QR コード、DataMatrix、PDF417 など、多数のバーコード タイプをサポートしています。

### パスワードで保護された文書内のバーコードを検証できますか?
はい、GroupDocs.Signature には、保護されたドキュメントを検証のために開くときにドキュメント パスワードを指定するオプションが用意されています。

### テキストではなくバイナリデータを含むバーコードを検証することは可能ですか?
はい、GroupDocs.Signatureは、バイナリデータでバーコードを検証するオプションを提供しています。 `BinaryData` 検証オプションのプロパティ。

### 関連リソース
* [GroupDocs.Signature API リファレンス](https://reference.groupdocs.com/signature/net/)
* [GroupDocs.Signature ダウンロード](https://releases.groupdocs.com/signature/net/)
* [GitHub のコード例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [ドキュメント](https://docs.groupdocs.com/signature/net/)
* [製品ページ](https://products.groupdocs.com/signature/net/)
* [ブログ記事](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [サポートフォーラム](https://forum.groupdocs.com/c/signature/13)
* [一時ライセンス](https://purchase.groupdocs.com/temporary-license/)