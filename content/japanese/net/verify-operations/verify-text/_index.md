---
"description": "GroupDocs.Signature を使って、.NET アプリケーションにおけるテキスト署名検証をマスターしましょう。完全なコード例とベストプラクティスを網羅した、ステップバイステップの実装ガイドです。"
"linktitle": "テキストを確認"
"second_title": "GroupDocs.Signature .NET API"
"title": "文書内のテキスト署名を検証する"
"url": "/ja/net/verify-operations/verify-text/"
"weight": 13
---

## 導入

テキスト署名は、デジタル署名や電子署名よりもシンプルな場合が多いものの、文書管理と検証において重要な役割を果たします。透かし、フッターテキスト、特定のコンテンツパターンなど、テキスト署名の存在と整合性を検証することは、文書検証プロセスにおいて重要な要素です。

GroupDocs.Signature for .NETは、幅広い形式のドキュメント内のテキスト署名を検証するための強力なAPIを提供します。この包括的なチュートリアルでは、.NETアプリケーションにテキスト検証機能を実装し、ドキュメントの整合性と真正性を維持する方法について説明します。

## 前提条件

テキスト検証機能を実装する前に、次の前提条件が満たされていることを確認してください。

1. GroupDocs.Signature for .NET: ライブラリをダウンロードしてインストールします。 [ダウンロードページ](https://releases。groupdocs.com/signature/net/).
2. .NET 開発環境: Visual Studio または互換性のある .NET 開発環境。
3. 基本知識: C# プログラミングと .NET Framework の概念に関する知識。
4. テスト ドキュメント: 検証用のテキスト署名を含むドキュメント。

## 必要な名前空間をインポートする

まず、GroupDocs.Signature 機能にアクセスするために必要な名前空間をインポートします。

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

テキスト検証プロセスを明確で管理しやすいステップに分解してみましょう。

## ステップ1: ドキュメントパスを指定する

```csharp
// テキスト署名を含むドキュメントへのパス
string filePath = "sample_multiple_signatures.docx";
```

例のパスを、テキスト署名を含むドキュメントへの実際のパスに置き換えてください。

## ステップ2: 署名オブジェクトの初期化

```csharp
// ドキュメントパスを渡してSignatureクラスのインスタンスを作成する
using (Signature signature = new Signature(filePath))
{
    // 検証コードはここに実装されます
}
```

Signature クラスは、GroupDocs.Signature API のすべての操作のメイン エントリ ポイントです。

## ステップ3: テキスト検証オプションを構成する

```csharp
// テキスト検証オプションを定義する
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = true,                               // 文書の全ページをチェックする
    SignatureImplementation = TextSignatureImplementation.Native,
    Text = "signature",                            // 検証するテキスト
    MatchType = TextMatchType.Contains             // 一致基準を指定する
};
```

検証オプションを使用すると、検証プロセスの特定の基準を定義できます。
- `AllPages`: すべてのドキュメントページをチェックするにはtrueに設定します
- `SignatureImplementation`テキストの実装方法を指定します（ネイティブまたはステッカー）
- `Text`: 文書内で一致するテキストコンテンツ
- `MatchType`テキスト一致の方法 (Contains、Exact、StartsWith など)

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
    Console.WriteLine($"Document {filePath} contains valid text signatures!");
    
    // 成功した署名に関する情報を表示する
    foreach (TextSignature textSignature in result.Succeeded)
    {
        Console.WriteLine($"\nFound valid text signature:");
        Console.WriteLine($"Text: {textSignature.Text}");
        Console.WriteLine($"Location: Page {textSignature.PageNumber}, {textSignature.Left}x{textSignature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

このコードは、検証が成功したかどうかを確認し、検証されたテキスト署名に関する詳細情報を提供します。

## 完全な例

以下はテキスト署名の検証を示す完全な動作例です。

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
                    TextVerifyOptions options = new TextVerifyOptions()
                    {
                        AllPages = true,
                        SignatureImplementation = TextSignatureImplementation.Native,
                        Text = "signature",
                        MatchType = TextMatchType.Contains
                    };
                    
                    // 文書の署名を検証する
                    VerificationResult result = signature.Verify(options);
                    
                    // プロセス検証結果
                    if(result.IsValid)
                    {
                        Console.WriteLine($"\nDocument {filePath} was verified successfully!");
                        foreach (TextSignature item in result.Succeeded)
                        {
                            Console.WriteLine($"\nValid signature is found with text: {item.Text}");
                            Console.WriteLine($"Location: Page {item.PageNumber}, position {item.Left}x{item.Top}");
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

### 検証のための正規表現の使用

より柔軟なパターン マッチングを行うには、正規表現を使用できます。

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    Text = "Invoice\\s+#\\d{5,6}",  // 「請求書番号 12345」のようなパターンに一致します
    MatchType = TextMatchType.Regex
};
```

### 特定の文書領域内のテキストの検証

ドキュメントの特定の領域に検証を制限できます。

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = false,
    PageNumber = 1,  // 最初のページのみ確認
    
    // 検索するエリアを定義する（ポイント単位の座標）
    PagesSetup = new PagesSetup() 
    { 
        FirstPage = true,
        LastPage = false,
        OddPages = false,
        EvenPages = false 
    },
    
    // 長方形の面積（ミリメートル）
    Rectangle = new Rectangle(10, 10, 100, 30),
    
    Text = "Confidential"
};
```

### 複数のテキストパターンを同時に検証する

さまざまなテキスト パターンをチェックするために、複数の検証オプションを作成できます。

```csharp
// 検証オプションのリストを作成する
List<VerifyOptions> listOptions = new List<VerifyOptions>();

// 最初のテキスト検証を追加
listOptions.Add(new TextVerifyOptions()
{
    Text = "Confidential",
    MatchType = TextMatchType.Exact
});

// 2番目のテキスト認証を追加
listOptions.Add(new TextVerifyOptions()
{
    Text = "Do not copy",
    MatchType = TextMatchType.Contains
});

// 複数のオプションで検証する
VerificationResult result = signature.Verify(listOptions);
```

### 特定の外観を持つテキストの検証

特定の書式設定特性を持つテキストを検証することもできます。

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    Text = "APPROVED",
    MatchType = TextMatchType.Exact,
    
    // 特定の外観プロパティを確認する
    ForegroundColorRGB = System.Drawing.Color.Green,
    Font = new SignatureFont() { FontFamily = "Arial", FontSize = 12, Bold = true }
};
```

## テキスト検証のベストプラクティス

1. 適切な一致タイプを選択します。検証要件に基づいて、適切な一致タイプ (含む、完全、正規表現) を選択します。
2. パフォーマンスの最適化: 大きなドキュメントの場合は、ドキュメント全体ではなく特定のページを検証することを検討してください。
3. エラー処理: 予期しないシナリオを適切に管理するために適切なエラー処理を実装します。
4. 大文字と小文字の区別を考慮する: 特に重要な検証の場合は、テキストの一致で大文字と小文字の区別に注意してください。
5. 徹底的にテストする: さまざまなドキュメント形式とテキスト パターンを使用して検証をテストし、互換性を確認します。

## 一般的な問題のトラブルシューティング

### テキストが検出されませんでした
- テキストのフォーマットやエンコードが検出に影響していないか確認する
- テキストが画像ではなく通常のテキストとしてドキュメント内に実際に存在していることを確認します。
- 別の一致基準を試してください（「完全一致」ではなく「含む」）

### パフォーマンスの問題
- 特定のページまたは領域をターゲットにして検証を最適化します
- より具体的なテキストパターンを使用して誤検知を減らす

### 検証の失敗
- スペース、特殊文字、書式設定が一致に影響していないか確認します
- テキストがスキャンされた画像の一部ではないことを確認する（OCR が必要）
- テキストが追加されてからドキュメントが変更されていないことを確認する

## 結論

テキスト検証は、ドキュメント認証における多用途かつ実用的なアプローチであり、単独で使用することも、他の検証方法と組み合わせて使用することもできます。GroupDocs.Signature for .NET は、.NET アプリケーションに堅牢なテキスト検証機能を実装するための包括的で使いやすい API を提供します。

このステップバイステップのガイドに従うことで、次の方法を学習しました。
- テキスト検証プロセスを構成して初期化する
- さまざまな検証基準を指定する
- 検証結果の処理と解釈
- 高度な検証シナリオを実装する

これらの機能により、さまざまなドキュメント形式にわたってテキストの信頼性を検証できる、安全で信頼性の高いドキュメント処理システムを構築できます。

## よくある質問

### GroupDocs.Signature はスキャンされたドキュメント内のテキストを検証できますか?
GroupDocs.Signatureは、主にデジタルテキストの検証を目的として設計されています。スキャンした文書の場合は、まずOCR（光学文字認識）技術を使用してスキャンした画像をテキストに変換する必要があります。

### テキスト検証ではどのドキュメント形式がサポートされていますか?
GroupDocs.Signature は、PDF、Word 文書 (DOC、DOCX)、Excel スプレッドシート (XLS、XLSX)、PowerPoint プレゼンテーション (PPT、PPTX)、画像など、幅広いドキュメント形式をサポートしています。

### 書式設定されたテキスト (太字、斜体、特定のフォント) を検証できますか?
はい、GroupDocs.Signature には、フォント ファミリ、サイズ、スタイル (太字、斜体)、色などの特定の書式設定特性を使用してテキストを検証するオプションが用意されています。

### パスワードで保護された文書内のテキストを検証することは可能ですか?
はい、GroupDocs.Signature には、保護されたドキュメントを検証のために開くときにドキュメント パスワードを指定するオプションが用意されています。

### 透かしや背景のテキストを確認できますか?
はい、GroupDocs.Signature は、ドキュメント内での実装方法に応じて、透かしや背景テキストなど、さまざまな種類のテキスト署名を検証できます。

### 関連リソース
* [GroupDocs.Signature API リファレンス](https://reference.groupdocs.com/signature/net/)
* [GroupDocs.Signature ダウンロード](https://releases.groupdocs.com/signature/net/)
* [GitHub のコード例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [ドキュメント](https://docs.groupdocs.com/signature/net/)
* [製品ページ](https://products.groupdocs.com/signature/net/)
* [ブログ記事](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [サポートフォーラム](https://forum.groupdocs.com/c/signature/13)
* [一時ライセンス](https://purchase.groupdocs.com/temporary-license/)