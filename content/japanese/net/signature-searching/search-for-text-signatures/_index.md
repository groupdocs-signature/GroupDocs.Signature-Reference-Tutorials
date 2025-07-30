---
"description": "包括的なステップバイステップ ガイドとコード例を使用して、GroupDocs.Signature for .NET を使用してドキュメント内のテキスト署名を効率的に検索する方法を学びます。"
"linktitle": "テキスト署名の検索"
"second_title": "GroupDocs.Signature .NET API"
"title": "文書内のテキスト署名を検索する"
"url": "/ja/net/signature-searching/search-for-text-signatures/"
"weight": 16
---

## 導入

テキスト署名は、ドキュメントの作成者、承認、または検証を示す一般的な方法です。デジタルドキュメント管理において、テキスト署名をプログラムで検索・抽出する機能は、ドキュメントの検証、ワークフローの自動化、コンプライアンス検証に不可欠です。GroupDocs.Signature for .NETは、さまざまなドキュメント形式と高度な検索機能をサポートし、.NETアプリケーションにテキスト署名検索機能を実装するための包括的なソリューションを提供します。

このチュートリアルでは、GroupDocs.Signature for .NET を使用してドキュメント内のテキスト署名を検索するプロセスを、詳細な説明、ステップバイステップの手順、実用的なコード例とともに説明します。

## 前提条件

テキスト署名の検索を始める前に、次の前提条件を満たしていることを確認してください。

1. GroupDocs.Signature for .NETライブラリ: ライブラリをダウンロードしてインストールします。 [リリースページ](https://releases。groupdocs.com/signature/net/).

2. 開発環境: Visual Studio や .NET をサポートする互換性のある IDE などの適切な開発環境をセットアップします。

3. サンプル ドキュメント: 検証およびテスト用のテキスト署名を含むテスト ドキュメントを準備します。

4. 基本的な C# の知識: C# プログラミング言語と .NET フレームワークの概念に関する知識。

## 名前空間のインポート

まず、GroupDocs.Signature 機能にアクセスするために必要な名前空間をインポートします。

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

ここで、テキスト署名を検索するプロセスを明確で管理しやすいステップに分解してみましょう。

## ステップ1：ドキュメントを読み込む

まず、ドキュメントパスを定義し、 `Signature` 物体：

```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);

using (Signature signature = new Signature(filePath))
{
    // テキスト署名検索コードがここに追加されます
}
```

## ステップ2: 検索オプションを設定する

作成と構成 `TextSearchOptions` テキスト署名の検索方法を指定します。

```csharp
// テキスト検索オプションを設定する
TextSearchOptions options = new TextSearchOptions
{
    // すべてのページを検索
    AllPages = true,
    
    // オプション: 一致するテキストを指定する
    // テキスト = "承認済み"、
    
    // オプション: 一致タイプを指定
    // マッチタイプ = TextMatchType.Contains
};
```

## ステップ3: テキスト署名検索を実行する

設定されたオプションを使用して検索操作を実行します。

```csharp
// テキスト署名を検索する
List<TextSignature> signatures = signature.Search<TextSignature>(options);
```

## ステップ4: 処理と結果の表示

見つかったテキスト署名を反復処理し、その詳細を表示します。

```csharp
// 検索結果を表示
Console.WriteLine($"\nSource document '{fileName}' contains {signatures.Count} text signature(s):");

foreach (TextSignature textSignature in signatures)
{
    Console.WriteLine($"Text signature found at page {textSignature.PageNumber} with text '{textSignature.Text}'");
    Console.WriteLine($"Location: X={textSignature.Left}, Y={textSignature.Top}, Width={textSignature.Width}, Height={textSignature.Height}");
    Console.WriteLine($"Signature type: {textSignature.SignatureImplementation}");
    Console.WriteLine();
}
```

## 完全な例

ドキュメント内のテキスト署名を検索する方法を示す完全な動作例を次に示します。

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace TextSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // ドキュメントパス - ファイルパスを更新します
            string filePath = "sample_multiple_signatures.docx";
            string fileName = Path.GetFileName(filePath);
            
            // 署名インスタンスを初期化する
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // テキスト検索オプションを設定する
                    TextSearchOptions options = new TextSearchOptions
                    {
                        // すべてのページを検索
                        AllPages = true
                    };
                    
                    // テキスト署名を検索する
                    List<TextSignature> signatures = signature.Search<TextSignature>(options);
                    
                    // 検索結果を表示
                    Console.WriteLine($"\nSource document '{fileName}' contains {signatures.Count} text signature(s):");
                    
                    foreach (TextSignature textSignature in signatures)
                    {
                        Console.WriteLine($"Text signature found at page {textSignature.PageNumber} with text '{textSignature.Text}'");
                        Console.WriteLine($"Location: X={textSignature.Left}, Y={textSignature.Top}, Width={textSignature.Width}, Height={textSignature.Height}");
                        Console.WriteLine($"Signature type: {textSignature.SignatureImplementation}");
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

## 高度なテキスト署名検索技術

### 特定のテキスト条件による検索

よりターゲットを絞った検索を行うには、 `TextSearchOptions` 特定のテキストコンテンツでフィルタリングするには:

```csharp
// 特定のテキスト条件で検索オプションを作成する
TextSearchOptions options = new TextSearchOptions
{
    // すべてのページを検索
    AllPages = true,
    
    // 特定のテキストを検索する
    Text = "Approved",
    
    // 一致タイプを指定する（含む、完全一致、開始、終了）
    MatchType = TextMatchType.Contains,
    
    // 大文字と小文字を区別した検索
    MatchCase = true
};
```

### 特定の文書領域での検索

検索をドキュメントの特定の領域に限定することができます。

```csharp
// 特定のドキュメント領域の検索オプションを作成する
TextSearchOptions options = new TextSearchOptions
{
    // 特定のページのみを検索する
    AllPages = false,
    PageNumber = 1,
    
    // または複数のページを指定
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } },
    
    // 検索する特定のエリアを定義する
    Rectangle = new Rectangle(100, 100, 400, 200)
};
```

### 高度なテキストフィルタリング

より複雑な検索要件に対応するカスタム フィルタリング ロジックを実装します。

```csharp
// カスタム処理で検索オプションを作成する
TextSearchOptions options = new TextSearchOptions
{
    AllPages = true,
    
    // デリゲートを使用してカスタム処理を定義する
    ProcessCompleted = (TextSignature signature) =>
    {
        // カスタム検証ロジック
        bool isValid = signature.Text.Length > 5 && 
                      (signature.Text.Contains("Approved") || signature.Text.Contains("Verified"));
        
        return isValid;
    }
};
```

### さまざまなテキストスタイルの検索

フォントとスタイルのプロパティを使用してテキスト署名をフィルタリングします。

```csharp
// 特定のテキストの外観をターゲットにした検索オプションを作成する
TextSearchOptions options = new TextSearchOptions
{
    // フォント名でフィルタリング
    FontName = "Arial",
    
    // フォントサイズの範囲でフィルタリング
    MinFontSize = 10,
    MaxFontSize = 14,
    
    // フォント色でフィルタリング
    ForeColor = System.Drawing.Color.Blue
};
```

### 署名メタデータの抽出

テキスト署名に関連付けられたメタデータを抽出して処理します。

```csharp
foreach (TextSignature signature in signatures)
{
    // アクセス署名メタデータ
    if (signature.Metadata != null && signature.Metadata.Count > 0)
    {
        Console.WriteLine("Signature Metadata:");
        
        foreach (var item in signature.Metadata)
        {
            Console.WriteLine($"  {item.Key}: {item.Value}");
        }
    }
    
    // 署名の作成日と変更日を確認する
    if (signature.CreatedOn.HasValue)
    {
        Console.WriteLine($"Created on: {signature.CreatedOn.Value}");
    }
    
    if (signature.ModifiedOn.HasValue)
    {
        Console.WriteLine($"Modified on: {signature.ModifiedOn.Value}");
    }
}
```

## 結論

この包括的なガイドでは、GroupDocs.Signature for .NETを使用してドキュメント内のテキスト署名を検索する方法について解説しました。基本的な検索操作から高度なテクニックまで、.NETアプリケーションに堅牢なテキスト署名機能を実装するための知識が得られます。

GroupDocs.Signature は、テキスト署名を操作するための強力で柔軟なフレームワークを提供し、高度なドキュメント検証システム、自動化されたワークフロー ソリューション、コンプライアンス検証ツールを構築できるようにします。

## よくある質問

### パスワードで保護された文書内のテキスト署名を検索できますか?

はい、GroupDocs.Signatureはパスワードで保護された文書内のテキスト署名の検索をサポートしています。初期化時にパスワードを入力してください。 `Signature` 物体：

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // テキスト署名を検索する
}
```

### テキスト署名検索ではどのドキュメント形式がサポートされていますか?

GroupDocs.Signature は、PDF、Microsoft Office ドキュメント (Word、Excel、PowerPoint)、OpenOffice 形式、画像など、幅広いドキュメント形式をサポートしています。

### 太字や斜体などの特定の書式が設定されたテキスト署名を検索できますか?

はい、特定の書式のテキスト署名を検索するには、 `FontBold` そして `FontItalic` プロパティ `TextSearchOptions`：

```csharp
TextSearchOptions options = new TextSearchOptions
{
    FontBold = true,
    FontItalic = true
};
```

### 大きなドキュメントの検索パフォーマンスを向上させるにはどうすればよいですか?

大きなドキュメントの場合、次の操作によって検索パフォーマンスを最適化できます。

1. 文書全体を検索するのではなく、特定のページのみを検索する
2. より具体的な検索条件を使用して一致数を減らす
3. 検索範囲を指定するには、 `Rectangle` 署名が通常どこにあるのか知っている場合のプロパティ
4. アプリケーションにページ区切りを実装して検索結果を一括処理する

### テキスト署名が電子的に追加されたのか、それとも元の文書コンテンツの一部なのかを検出できますか?

GroupDocs.Signatureは、文書内の異なる種類のテキスト要素を区別することができます。 `SignatureImplementation` の所有物 `TextSignature` テキストが正式な署名であるか、通常の文書コンテンツであるかを示します。ただし、最終的な判断は、テキストが元々どのように文書に追加されたかによって異なります。

## 参照

* [APIリファレンス](https://reference.groupdocs.com/signature/net/)
* [GitHub のコード例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [製品ドキュメント](https://docs.groupdocs.com/signature/net/)
* [製品ページ](https://products.groupdocs.com/signature/net/)
* [最新バージョンをダウンロード](https://releases.groupdocs.com/signature/net/)
* [ブログ記事](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [無料サポートフォーラム](https://forum.groupdocs.com/c/signature/13)
* [一時ライセンス](https://purchase.groupdocs.com/temporary-license/)