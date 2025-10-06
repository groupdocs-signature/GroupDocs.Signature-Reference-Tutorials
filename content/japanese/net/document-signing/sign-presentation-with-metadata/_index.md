---
"description": "GroupDocs.Signature for .NET を使用して、PowerPoint プレゼンテーションにメタデータ署名を埋め込む方法を学びます。作成者の詳細、タイムスタンプ、カスタムプロパティを追加することで、プレゼンテーションの信頼性とトレーサビリティを向上させます。"
"linktitle": "メタデータでプレゼンテーションに署名する"
"second_title": "GroupDocs.Signature .NET API"
"title": "C# .NET でメタデータ署名を使用して PowerPoint プレゼンテーションを強化する"
"url": "/ja/net/document-signing/sign-presentation-with-metadata/"
"weight": 12
type: docs
---
## 導入

今日のデジタルワークプレイスにおいて、プレゼンテーションはコミュニケーションと情報共有のための重要なツールです。これらのプレゼンテーションファイルの真正性と整合性を確保することは、特に企業や教育機関においてますます重要になっています。プレゼンテーションのセキュリティとトレーサビリティを強化する効果的な方法の一つは、メタデータ署名を埋め込むことです。

この包括的なチュートリアルでは、GroupDocs.Signature for .NET を使用して、PowerPoint プレゼンテーション (PPTX、PPT) にメタデータ署名を追加する手順を解説します。メタデータ署名を追加することで、作成者の詳細、作成日時、ドキュメント識別子、その他のカスタムプロパティといった貴重な情報をプレゼンテーションのファイル構造に直接埋め込むことができます。

## 前提条件

このチュートリアルを進める前に、次のものを用意してください。

1. [.NET 用 GroupDocs.Signature](https://releases.groupdocs.com/signature/net/) - ライブラリをダウンロードしてインストールする
2. 開発環境 - Visual Studio またはその他の .NET 互換 IDE
3. PowerPoint プレゼンテーション - サンプル プレゼンテーション ファイル (PPTX または PPT 形式)
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

ソース プレゼンテーションのパスと、署名された出力を保存する場所を定義します。

```csharp
// プレゼンテーションファイルへのパスを指定します
string filePath = "sample.pptx";

// 署名されたプレゼンテーションの出力ディレクトリとファイル名を定義します
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignPresentationWithMetadata", "SignedWithMetadata.pptx");

// 出力ディレクトリが存在することを確認する
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## ステップ2: 署名オブジェクトの初期化

ソース プレゼンテーション ファイルを使用して、Signature クラスのインスタンスを作成します。

```csharp
using (Signature signature = new Signature(filePath))
{
    // 残りのコードはここに記述します
}
```

## ステップ3: メタデータ署名の作成と構成

次に、メタデータ オプションを定義し、プレゼンテーション メタデータ署名の配列を作成します。

```csharp
// メタデータ オプション オブジェクトを作成する
MetadataSignOptions options = new MetadataSignOptions();

// 異なるデータ型のプレゼンテーションメタデータ署名の配列を作成する
PresentationMetadataSignature[] signatures = new PresentationMetadataSignature[]
{
    new PresentationMetadataSignature("Author", "Mr.Sherlock Holmes"), // 文字列値
    new PresentationMetadataSignature("CreatedOn", DateTime.Now),      // 日時値
    new PresentationMetadataSignature("DocumentId", 123456),           // 整数値
    new PresentationMetadataSignature("SignatureId", 123.456D),        // 二重価値
    new PresentationMetadataSignature("Amount", 123.456M),             // 小数値
    new PresentationMetadataSignature("Total", 123.456F)               // 浮動小数点値
};

// オプションに署名コレクションを追加する
options.Signatures.AddRange(signatures);
```

## ステップ4: メタデータでプレゼンテーションに署名する

プレゼンテーションにメタデータ署名を適用し、結果を保存します。

```csharp
// 文書に署名し、出力ファイルパスに保存します
SignResult result = signature.Sign(outputFilePath, options);

// 成功メッセージを表示する
Console.WriteLine($"\nSource presentation signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed presentation saved at: {outputFilePath}");
```

## 完全な例

すべてのステップをまとめた完全なコード例を次に示します。

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignPresentationWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // ファイルパスを指定する
            string filePath = "sample.pptx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignPresentationWithMetadata", "SignedWithMetadata.pptx");
            
            // 出力ディレクトリが存在することを確認する
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // メタデータでプレゼンテーションに署名する
            using (Signature signature = new Signature(filePath))
            {
                // メタデータ オプション オブジェクトを作成する
                MetadataSignOptions options = new MetadataSignOptions();
                
                // 異なるデータ型のプレゼンテーションメタデータ署名の配列を作成する
                PresentationMetadataSignature[] signatures = new PresentationMetadataSignature[]
                {
                    new PresentationMetadataSignature("Author", "Mr.Sherlock Holmes"), // 文字列値
                    new PresentationMetadataSignature("CreatedOn", DateTime.Now),      // 日時値
                    new PresentationMetadataSignature("DocumentId", 123456),           // 整数値
                    new PresentationMetadataSignature("SignatureId", 123.456D),        // 二重価値
                    new PresentationMetadataSignature("Amount", 123.456M),             // 小数値
                    new PresentationMetadataSignature("Total", 123.456F)               // 浮動小数点値
                };
                
                // オプションに署名コレクションを追加する
                options.Signatures.AddRange(signatures);
                
                // 文書に署名してファイルに保存する
                SignResult result = signature.Sign(outputFilePath, options);
                
                // 結果を表示
                Console.WriteLine($"\nSource presentation signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## 高度なプレゼンテーションメタデータテクニック

### カスタムおよび組み込みのプレゼンテーションプロパティの操作

PowerPoint プレゼンテーションには、ファイル プロパティ ダイアログからアクセスできる組み込みプロパティとカスタム プロパティの両方があります。GroupDocs.Signature では、両方のプロパティを操作できます。

```csharp
// 組み込みプロパティを追加する
signatures = new PresentationMetadataSignature[]
{
    new PresentationMetadataSignature("Company", "Sherlock Holmes Consulting"),
    new PresentationMetadataSignature("Category", "Presentation"),
    new PresentationMetadataSignature("Keywords", "metadata,signing,groupdocs"),
    new PresentationMetadataSignature("Comments", "This document was signed with GroupDocs.Signature"),
    new PresentationMetadataSignature("Manager", "John Watson")
};
options.Signatures.AddRange(signatures);

// カスタムプロパティを追加する
options.Signatures.Add(new PresentationMetadataSignature("CustomProperty1", "Custom Value 1"));
options.Signatures.Add(new PresentationMetadataSignature("CustomProperty2", "Custom Value 2"));
```

### 署名されたプレゼンテーションのメタデータの検索

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

### 既存のメタデータの更新

同じプロパティ名を使用して、プレゼンテーション内の既存のメタデータを更新できます。

```csharp
// 既存のメタデータを更新する
options.Signatures.Add(new PresentationMetadataSignature("Author", "Updated Author Name"));
```

## 結論

この包括的なチュートリアルでは、GroupDocs.Signature for .NET を使用して、PowerPoint プレゼンテーションにメタデータで署名する方法を学習しました。プレゼンテーションファイルにメタデータを埋め込むことで、ドキュメントの追跡可能性が向上し、貴重なコンテキストが提供され、信頼性が確保されます。

プレゼンテーション内のメタデータ署名は、ドキュメントの出所、作成者、バージョン管理が重要なビジネス環境や教育環境で特に役立ちます。埋め込まれたメタデータには、作成者、作成日時、ドキュメント識別子、組織のニーズに関連するカスタムプロパティなどの情報を含めることができます。

GroupDocs.Signature を使用してメタデータ署名を実装することで、PowerPoint プレゼンテーションの整合性を維持し、ライフサイクル全体にわたって検証可能な情報を提供できるようになります。

## よくある質問

### すでにいくつかのプロパティが定義されているプレゼンテーションにメタデータを追加できますか?

はい、プレゼンテーションに新しいメタデータを追加したり、既存のメタデータを更新したりできます。GroupDocs.Signature は、新しいプロパティを追加するか、同じ名前の既存のプロパティを更新することで、統合を処理します。

### メタデータ署名ではどのプレゼンテーション形式がサポートされていますか?

GroupDocs.Signature for .NETは、PPT、PPTX、PPTM、PPS、PPSX、その他のPowerPoint形式のPowerPointプレゼンテーションのメタデータ署名をサポートしています。完全なリストについては、 [公式文書](https://docs。groupdocs.com/signature/net/).

### プレゼンテーション内のメタデータ署名は視聴者に表示されますか?

メタデータ署名はプレゼンテーションスライド自体には表示されませんが、PowerPointやその他の互換性のあるアプリケーションのドキュメントプロパティパネルから表示できます。

### プレゼンテーション内の機密メタデータを暗号化できますか?

個々のメタデータプロパティを暗号化することはできませんが、GroupDocs.Signature にはドキュメント全体を保護するためのオプションが用意されています。パスワード保護を適用することで、プレゼンテーションとそのメタデータへのアクセスを制限できます。

### メタデータを追加するとプレゼンテーションのパフォーマンスに影響しますか?

メタデータの追加はファイルサイズへの影響を最小限に抑え、プレゼンテーションのパフォーマンスにも影響を与えません。ユーザーエクスペリエンスに影響を与えることなく、ドキュメントのプロパティを拡張できる軽量な方法です。

### さらにリソースやサポートはどこで見つかりますか?

- [APIリファレンス](https://reference.groupdocs.com/signature/net/)
- [ダウンロード](https://releases.groupdocs.com/signature/net/)
- [例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [ドキュメント](https://docs.groupdocs.com/signature/net/)
- [製品ページ](https://products.groupdocs.com/signature/net/)
- [ブログ](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [サポートフォーラム](https://forum.groupdocs.com/c/signature/13)
- [一時ライセンス](https://purchase.groupdocs.com/temporary-license/)