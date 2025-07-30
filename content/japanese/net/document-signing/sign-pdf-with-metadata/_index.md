---
"description": "GroupDocs.Signature for .NET を使用して、PDF ドキュメントにメタデータ署名を統合します。作成者情報、タイムスタンプ、カスタムデータを埋め込むことで、PDF の信頼性とトレーサビリティを向上させる方法を学習します。"
"linktitle": "メタデータでPDFに署名する"
"second_title": "GroupDocs.Signature .NET API"
"title": "C# .NET で PDF ドキュメントにメタデータ署名を追加する"
"url": "/ja/net/document-signing/sign-pdf-with-metadata/"
"weight": 11
---

## 導入

PDF（Portable Document Format）文書は、その一貫性とプラットフォーム非依存の点から、様々な業界で広く利用されています。これらの文書の真正性とトレーサビリティを確保することは、多くの専門的な環境において極めて重要です。これを実現する効果的な方法の一つは、PDFファイル自体にメタデータを埋め込むことです。

この包括的なチュートリアルでは、GroupDocs.Signature for .NET を使用してPDFドキュメントにメタデータで署名する方法を説明します。メタデータ署名を使用すると、ドキュメントの外観を目に見える形で変更することなく、作成者の詳細、作成タイムスタンプ、ドキュメント識別子、カスタム値などの追加情報をドキュメント内に埋め込むことができます。

## 前提条件

始める前に、以下のものが用意されていることを確認してください。

1. [.NET 用 GroupDocs.Signature](https://releases.groupdocs.com/signature/net/) - ライブラリをダウンロードしてインストールする
2. 開発環境 - Visual Studio またはその他の .NET 互換 IDE
3. PDFドキュメント - 署名用のサンプルPDFファイル
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

まず、PDF ドキュメントへのパスを定義し、署名された出力を保存する場所を指定します。

```csharp
// PDF文書へのパスを指定します
string filePath = "sample.pdf";

// 出力ディレクトリとファイルパスを定義する
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignPdfWithMetadata", "SignedWithMetadata.pdf");

// 出力ディレクトリが存在することを確認する
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## ステップ2: 署名オブジェクトの初期化

ソース PDF ドキュメントを使用して Signature クラスのインスタンスを作成します。

```csharp
using (Signature signature = new Signature(filePath))
{
    // 署名用のコードはここに記入します
}
```

## ステップ3: メタデータオプションを定義する

メタデータ オプションを作成して構成し、さまざまな種類のメタデータ署名を追加します。

```csharp
// メタデータ オプション オブジェクトを作成する
MetadataSignOptions options = new MetadataSignOptions();

// 流暢なインターフェースを使用してさまざまな種類のメタデータを追加します
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // 文字列値
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // 日時値
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // 整数値
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // 二重価値
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // 小数値
    .Add(new PdfMetadataSignature("Total", 123.456F));              // 浮動小数点値
```

## ステップ4: メタデータでPDFに署名する

メタデータ署名を PDF ドキュメントに適用し、結果を保存します。

```csharp
// 文書に署名し、出力パスに保存します
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

namespace SignPdfWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // ファイルパスを指定する
            string filePath = "sample.pdf";
            string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
            
            // 出力ディレクトリが存在することを確認する
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // メタデータでPDFに署名する
            using (Signature signature = new Signature(filePath))
            {
                // メタデータ オプション オブジェクトを作成する
                MetadataSignOptions options = new MetadataSignOptions();
                
                // さまざまな種類のメタデータ署名を追加する
                options
                    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // 文字列値
                    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // 日時値
                    .Add(new PdfMetadataSignature("DocumentId", 123456))            // 整数値
                    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // 二重価値
                    .Add(new PdfMetadataSignature("Amount", 123.456M))              // 小数値
                    .Add(new PdfMetadataSignature("Total", 123.456F));              // 浮動小数点値
                
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

## 高度なPDFメタデータ操作

### 名前空間サポートによるカスタムメタデータの追加

PDF ドキュメントは、XML 名前空間をサポートするカスタム メタデータをサポートします。

```csharp
// 名前空間を使用してカスタムメタデータを追加する
options.Add(new PdfMetadataSignature("CustomProperty", "Custom Value")
{
    NamespaceUri = "http://your-namespace.com/schema"
});
```

### 署名されたPDF内のメタデータの検索

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

### 標準PDFメタデータの操作

PDF ドキュメントには、アクセスして変更できる標準のメタデータ フィールドがあります。

```csharp
// 標準のPDFメタデータフィールドを設定する
options
    .Add(new PdfMetadataSignature("Title", "Important Contract"))
    .Add(new PdfMetadataSignature("Subject", "Legal Agreement"))
    .Add(new PdfMetadataSignature("Keywords", "contract, agreement, legal, binding"))
    .Add(new PdfMetadataSignature("Creator", "Legal Department"))
    .Add(new PdfMetadataSignature("Producer", "GroupDocs.Signature"));
```

## 結論

このチュートリアルでは、GroupDocs.Signature for .NET を使用して、メタデータでPDFドキュメントに署名する方法を学習しました。PDFファイルにメタデータを埋め込むことで、ドキュメントの信頼性を高め、重要な情報を追加し、ドキュメント管理ワークフローを改善できます。

PDFのメタデータ署名は、文書のトレーサビリティと真正性の検証が不可欠なビジネス環境で特に役立ちます。埋め込まれたメタデータには、文書の出所、作成者、作成日時、バージョン、組織のワークフローに関連するカスタムプロパティなどの情報を含めることができます。

GroupDocs.Signature を使用してメタデータ署名を実装することで、PDF ドキュメントの整合性を維持し、ライフサイクル全体にわたって検証可能な情報を提供できるようになります。

## よくある質問

### PDF ドキュメント内の既存のメタデータを変更できますか?

はい、PDFドキュメント内の既存のメタデータを変更できます。既存のメタデータ署名と同じ名前の新しいメタデータ署名を適用すると、値もそれに応じて更新されます。

### PDF ドキュメント内のメタデータ署名はエンドユーザーに表示されますか?

メタデータ署名はドキュメントコンテンツ自体には表示されません。ただし、Adobe AcrobatなどのPDFリーダーのドキュメントプロパティパネル、またはメタデータ表示用の専用ツールを使用することで表示できます。

### PDF 内のメタデータを暗号化または保護できますか?

GroupDocs.Signatureは、暗号化を含むドキュメントのセキュリティ保護オプションを提供します。ドキュメントレベルの暗号化を適用することで、メタデータを含むPDF全体を保護できます。

### PDF に追加できるメタデータの量に制限はありますか?

PDF仕様には厳密な制限はありませんが、メタデータを過剰に追加するとファイルサイズが大きくなる可能性があります。メタデータには、関連性のある必要な情報のみを含めることをお勧めします。

### メタデータを追加した後に PDF が改ざんされたかどうかをプログラムで検証できますか?

はい、GroupDocs.Signature は、メタデータの変更など、署名後にドキュメントが変更されたかどうかを検出するのに役立つ検証機能を提供します。

### さらにリソースやサポートはどこで見つかりますか?

- [APIリファレンス](https://reference.groupdocs.com/signature/net/)
- [ダウンロード](https://releases.groupdocs.com/signature/net/)
- [例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [ドキュメント](https://docs.groupdocs.com/signature/net/)
- [製品ページ](https://products.groupdocs.com/signature/net/)
- [ブログ](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [サポートフォーラム](https://forum.groupdocs.com/c/signature/13)
- [一時ライセンス](https://purchase.groupdocs.com/temporary-license/)