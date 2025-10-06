---
"description": "GroupDocs.Signature for .NET を使用して、Word 文書にメタデータ署名を追加します。作成者の詳細、タイムスタンプ、カスタムプロパティを埋め込むことで、ドキュメントのセキュリティとトレーサビリティを強化します。"
"linktitle": "メタデータを使用した署名ワードプロセッシング"
"second_title": "GroupDocs.Signature .NET API"
"title": "C# .NET でメタデータ署名を使用して Word 文書を強化する"
"url": "/ja/net/document-signing/sign-word-processing-with-metadata/"
"weight": 14
type: docs
---
## 導入

ワープロ文書は、ビジネス、教育、そして個人的なコミュニケーションにおいて最も一般的に使用されるファイル形式の一つです。これらの文書の真正性を確保し、出所を追跡し、整合性を維持することは、多くの専門的な環境において極めて重要です。文書のセキュリティとトレーサビリティを強化する効果的な方法の一つは、メタデータ署名を埋め込むことです。

この包括的なチュートリアルでは、GroupDocs.Signature for .NET を使用して、Word文書にメタデータで署名する手順を解説します。メタデータ署名を追加することで、作成者の詳細、作成日時、文書識別子、その他のカスタムプロパティといった貴重な情報を文書ファイル構造に直接埋め込むことができます。

## 前提条件

このチュートリアルを進める前に、次のものを用意してください。

1. [.NET 用 GroupDocs.Signature](https://releases.groupdocs.com/signature/net/) - ライブラリをダウンロードしてインストールする
2. 開発環境 - Visual Studio またはその他の .NET 互換 IDE
3. Word 文書 - サンプル ドキュメント ファイル (DOCX、DOC など)
4. C#の基礎知識 - C#プログラミング言語に精通していること

## 名前空間のインポート

まず、GroupDocs.Signature 機能にアクセスするために必要な名前空間をインポートします。

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## ステップ1: ファイルパスを設定する

ソース Word 文書のパスと、署名された出力を保存する場所を定義します。

```csharp
// Word文書へのパスを指定します
string filePath = "sample.docx";

// 署名された文書の出力ディレクトリとファイル名を定義する
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignWordProcessingWithMetadata", "SignedWithMetadata.docx");

// 出力ディレクトリが存在することを確認する
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## ステップ2: 署名オブジェクトの初期化

ソース Word 文書を使用して Signature クラスのインスタンスを作成します。

```csharp
using (Signature signature = new Signature(filePath))
{
    // 残りのコードはここに記述します
}
```

## ステップ3: メタデータ署名の作成と構成

次に、メタデータ オプションを定義し、さまざまなタイプのメタデータ署名を追加します。

```csharp
// メタデータ オプション オブジェクトを作成する
MetadataSignOptions options = new MetadataSignOptions();

// 流暢なインターフェースを使用してさまざまな種類のメタデータを追加します
options
    .Add(new WordProcessingMetadataSignature("Author", "Mr.Sherlock Holmes")) // 文字列値
    .Add(new WordProcessingMetadataSignature("CreatedOn", DateTime.Now))      // 日時値
    .Add(new WordProcessingMetadataSignature("DocumentId", 123456))           // 整数値
    .Add(new WordProcessingMetadataSignature("SignatureId", 123.456D))        // 二重価値
    .Add(new WordProcessingMetadataSignature("Amount", 123.456M))             // 小数値
    .Add(new WordProcessingMetadataSignature("Total", 123.456F));             // 浮動小数点値
```

## ステップ4: メタデータでドキュメントに署名する

メタデータ署名を Word 文書に適用し、結果を保存します。

```csharp
// 文書に署名し、出力ファイルパスに保存します
SignResult result = signature.Sign(outputFilePath, options);

// 成功メッセージを表示する
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed document saved at: {outputFilePath}");
```

## 完全な例

すべてのステップをまとめた完全なコード例を次に示します。

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignWordProcessingWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // ファイルパスを指定する
            string filePath = "sample.docx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignWordProcessingWithMetadata", "SignedWithMetadata.docx");
            
            // 出力ディレクトリが存在することを確認する
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // メタデータを使用してWord文書に署名する
            using (Signature signature = new Signature(filePath))
            {
                // メタデータ オプション オブジェクトを作成する
                MetadataSignOptions options = new MetadataSignOptions();
                
                // さまざまな種類のメタデータ署名を追加する
                options
                    .Add(new WordProcessingMetadataSignature("Author", "Mr.Sherlock Holmes")) // 文字列値
                    .Add(new WordProcessingMetadataSignature("CreatedOn", DateTime.Now))      // 日時値
                    .Add(new WordProcessingMetadataSignature("DocumentId", 123456))           // 整数値
                    .Add(new WordProcessingMetadataSignature("SignatureId", 123.456D))        // 二重価値
                    .Add(new WordProcessingMetadataSignature("Amount", 123.456M))             // 小数値
                    .Add(new WordProcessingMetadataSignature("Total", 123.456F));             // 浮動小数点値
                
                // 文書に署名してファイルに保存する
                SignResult result = signature.Sign(outputFilePath, options);
                
                // 結果を表示
                Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## 高度なWord文書メタデータテクニック

### カスタムおよび組み込みドキュメントプロパティの操作

Word文書には、ドキュメントプロパティパネルからアクセスできる組み込みプロパティとカスタムプロパティの両方があります。GroupDocs.Signatureでは、両方のプロパティを操作できます。

```csharp
// 組み込みプロパティを追加する
options
    .Add(new WordProcessingMetadataSignature("Company", "Sherlock Holmes Consulting"))
    .Add(new WordProcessingMetadataSignature("Category", "Legal Document"))
    .Add(new WordProcessingMetadataSignature("Keywords", "contract,agreement,legal"))
    .Add(new WordProcessingMetadataSignature("Comments", "This document is confidential"))
    .Add(new WordProcessingMetadataSignature("Manager", "John Watson"));

// カスタムプロパティを追加する
options.Add(new WordProcessingMetadataSignature("Department", "Legal"));
options.Add(new WordProcessingMetadataSignature("SecurityLevel", "Confidential"));
```

### 署名されたWord文書内のメタデータの検索

署名後、メタデータを検証または抽出する必要がある場合があります。

```csharp
// メタデータの検索オプションを作成する
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// メタデータ署名を検索する
SearchResult searchResult = signature.Search(searchOptions);

// 見つかった署名を表示する
Console.WriteLine($"Found {searchResult.Signatures.Count} metadata signatures:");
foreach (var foundSignature in searchResult.Signatures)
{
    MetadataSignature metadataSignature = foundSignature as MetadataSignature;
    if (metadataSignature != null)
    {
        Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value} ({metadataSignature.Value.GetType().Name})");
    }
}
```

### ドキュメント変数の操作

Word 文書は、別の形式のメタデータであるドキュメント変数もサポートしています。

```csharp
// ドキュメント変数を追加する
options.Add(new WordProcessingMetadataSignature("DocVariable1", "Custom Value 1", true));
options.Add(new WordProcessingMetadataSignature("DocVariable2", DateTime.Now, true));
```

## 結論

この包括的なチュートリアルでは、GroupDocs.Signature for .NET を使用して、Word文書にメタデータで署名する方法を学習しました。Word文書にメタデータを埋め込むことで、文書の追跡可能性が向上し、貴重なコンテキストが提供され、信頼性が確保されます。

Word文書のメタデータ署名は、文書の出所、作成者、バージョン管理が重要なビジネス環境や法務環境で特に役立ちます。埋め込まれたメタデータには、作成者、作成日時、文書識別子、組織のニーズに関連するカスタムプロパティなどの情報を含めることができます。

GroupDocs.Signature を使用してメタデータ署名を実装することで、Word 文書の整合性を維持し、ライフサイクル全体にわたって検証可能な情報を提供できるようになります。

## よくある質問

### すでにいくつかのプロパティが定義されている Word 文書にメタデータを追加できますか?

はい、Word 文書に新しいメタデータを追加したり、既存のメタデータを更新したりできます。GroupDocs.Signature は、新しいプロパティを追加するか、同じ名前の既存のプロパティを更新することで、統合を処理します。

### メタデータ署名ではどのワードプロセッシング形式がサポートされていますか?

GroupDocs.Signature for .NETは、DOCX、DOC、RTF、ODTなど、さまざまなWord文書形式のメタデータ署名をサポートしています。完全なリストについては、 [ドキュメント](https://docs。groupdocs.com/signature/net/).

### Word 文書内のメタデータ署名は読者に表示されますか?

メタデータ署名はドキュメントコンテンツ自体には表示されませんが、Microsoft Wordなどの互換性のあるアプリケーションのドキュメントプロパティパネルから表示できます。

### メタデータを追加した後に Word 文書が改ざんされたかどうかをプログラムで検証できますか?

はい、GroupDocs.Signature は、メタデータの変更など、署名後にドキュメントが変更されたかどうかを検出するのに役立つ検証機能を提供します。

### Word 文書からメタデータを削除することは可能ですか?

はい、GroupDocs.Signatureには、必要に応じてドキュメントからメタデータ署名を削除するオプションがあります。これは、ドキュメントを外部に共有する前に機密情報を消去するのに役立ちます。

### さらにリソースやサポートはどこで見つかりますか?

- [APIリファレンス](https://reference.groupdocs.com/signature/net/)
- [ダウンロード](https://releases.groupdocs.com/signature/net/)
- [例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [ドキュメント](https://docs.groupdocs.com/signature/net/)
- [製品ページ](https://products.groupdocs.com/signature/net/)
- [ブログ](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [サポートフォーラム](https://forum.groupdocs.com/c/signature/13)
- [一時ライセンス](https://purchase.groupdocs.com/temporary-license/)