---
"description": "GroupDocs.Signature for .NET を使用してメタデータ署名を埋め込むことで、Excel スプレッドシートを保護および強化できます。作成者情報、タイムスタンプ、カスタムデータを追加することで、ドキュメントの追跡可能性と信頼性が向上します。"
"linktitle": "メタデータでスプレッドシートに署名する"
"second_title": "GroupDocs.Signature .NET API"
"title": "C# .NET で Excel スプレッドシートにメタデータ署名を追加する"
"url": "/ja/net/document-signing/sign-spreadsheet-with-metadata/"
"weight": 13
type: docs
---
## 導入

Excelスプレッドシートには、重要なビジネスデータ、財務情報、重要な計算が含まれることがよくあります。これらのデータの真正性を確保し、その出所を追跡し、整合性を保護することは、多くのビジネス環境において不可欠です。スプレッドシートのセキュリティとトレーサビリティを強化する効果的な方法の一つは、メタデータ署名を埋め込むことです。

この包括的なチュートリアルでは、GroupDocs.Signature for .NET を使用してメタデータでExcelスプレッドシートに署名するプロセスを解説します。メタデータ署名を追加することで、作成者の詳細、作成日時、ドキュメント識別子、その他のカスタムプロパティといった貴重な情報をスプレッドシートのファイル構造に直接埋め込むことができます。

## 前提条件

このチュートリアルを進める前に、次のものを用意してください。

1. [.NET 用 GroupDocs.Signature](https://releases.groupdocs.com/signature/net/) - ライブラリをダウンロードしてインストールする
2. 開発環境 - Visual Studio またはその他の .NET 互換 IDE
3. Excel スプレッドシート - サンプルのスプレッドシート ファイル (XLSX、XLS など)
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

ソース スプレッドシートのパスと、署名された出力を保存する場所を定義します。

```csharp
// Excelファイルへのパスを指定します
string filePath = "sample.xlsx";

// 署名されたスプレッドシートの出力ディレクトリとファイル名を定義します
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");

// 出力ディレクトリが存在することを確認する
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## ステップ2: 署名オブジェクトの初期化

ソース スプレッドシート ファイルを使用して Signature クラスのインスタンスを作成します。

```csharp
using (Signature signature = new Signature(filePath))
{
    // 残りのコードはここに記述します
}
```

## ステップ3: メタデータ署名の作成と構成

次に、メタデータ オプションを定義し、スプレッドシートのメタデータ署名の配列を作成します。

```csharp
// メタデータ オプション オブジェクトを作成する
MetadataSignOptions options = new MetadataSignOptions();

// 異なるデータ型のスプレッドシートメタデータ署名の配列を作成する
SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // 文字列値
    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // 日時値
    new SpreadsheetMetadataSignature("DocumentId", 123456),           // 整数値
    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // 二重価値
    new SpreadsheetMetadataSignature("Amount", 123.456M),             // 小数値
    new SpreadsheetMetadataSignature("Total", 123.456F)               // 浮動小数点値
};

// オプションに署名コレクションを追加する
options.Signatures.AddRange(signatures);
```

## ステップ4: メタデータでスプレッドシートに署名する

メタデータ署名をスプレッドシートに適用し、結果を保存します。

```csharp
// 文書に署名し、出力ファイルパスに保存します
SignResult result = signature.Sign(outputFilePath, options);

// 成功メッセージを表示する
Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed spreadsheet saved at: {outputFilePath}");
```

## 完全な例

すべてのステップをまとめた完全なコード例を次に示します。

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignSpreadsheetWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // ファイルパスを指定する
            string filePath = "sample.xlsx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");
            
            // 出力ディレクトリが存在することを確認する
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // メタデータでスプレッドシートに署名する
            using (Signature signature = new Signature(filePath))
            {
                // メタデータ オプション オブジェクトを作成する
                MetadataSignOptions options = new MetadataSignOptions();
                
                // 異なるデータ型のスプレッドシートメタデータ署名の配列を作成する
                SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
                {
                    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // 文字列値
                    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // 日時値
                    new SpreadsheetMetadataSignature("DocumentId", 123456),           // 整数値
                    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // 二重価値
                    new SpreadsheetMetadataSignature("Amount", 123.456M),             // 小数値
                    new SpreadsheetMetadataSignature("Total", 123.456F)               // 浮動小数点値
                };
                
                // オプションに署名コレクションを追加する
                options.Signatures.AddRange(signatures);
                
                // 文書に署名してファイルに保存する
                SignResult result = signature.Sign(outputFilePath, options);
                
                // 結果を表示
                Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## 高度なスプレッドシートメタデータテクニック

### カスタムおよび組み込みのスプレッドシートプロパティの操作

Excelスプレッドシートには、ファイルプロパティダイアログからアクセスできる組み込みプロパティとカスタムプロパティの両方があります。GroupDocs.Signatureでは、両方のプロパティを操作できます。

```csharp
// 組み込みプロパティを追加する
signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Company", "Sherlock Holmes Consulting"),
    new SpreadsheetMetadataSignature("Category", "Financial"),
    new SpreadsheetMetadataSignature("Keywords", "budget,forecast,analysis"),
    new SpreadsheetMetadataSignature("Comments", "This spreadsheet contains confidential information"),
    new SpreadsheetMetadataSignature("Manager", "John Watson")
};
options.Signatures.AddRange(signatures);

// カスタムプロパティを追加する
options.Signatures.Add(new SpreadsheetMetadataSignature("Department", "Finance"));
options.Signatures.Add(new SpreadsheetMetadataSignature("SecurityLevel", "Confidential"));
```

### 署名されたスプレッドシート内のメタデータの検索

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

同じプロパティ名を使用して、スプレッドシート内の既存のメタデータを更新できます。

```csharp
// 既存のメタデータを更新する
options.Signatures.Add(new SpreadsheetMetadataSignature("Author", "Updated Author Name"));
```

## 結論

この包括的なチュートリアルでは、GroupDocs.Signature for .NET を使用してメタデータでExcelスプレッドシートに署名する方法を学習しました。スプレッドシートファイルにメタデータを埋め込むことで、ドキュメントの追跡可能性が向上し、貴重なコンテキストが提供され、信頼性が確保されます。

スプレッドシートのメタデータ署名は、ドキュメントの出所、作成者、バージョン管理が重要なビジネス環境で特に役立ちます。埋め込まれたメタデータには、作成者、作成日時、ドキュメント識別子、組織のニーズに関連するカスタムプロパティなどの情報を含めることができます。

GroupDocs.Signature を使用してメタデータ署名を実装することで、Excel スプレッドシートの整合性を維持し、ライフサイクル全体にわたって検証可能な情報を提供できるようになります。

## よくある質問

### すでにいくつかのプロパティが定義されているスプレッドシートにメタデータを追加できますか?

はい、スプレッドシートに新しいメタデータを追加したり、既存のメタデータを更新したりできます。GroupDocs.Signature は、新しいプロパティを追加するか、同じ名前の既存のプロパティを更新することで、統合を処理します。

### メタデータ署名にはどのスプレッドシート形式がサポートされていますか?

GroupDocs.Signature for .NETは、XLSX、XLS、XLSM、ODSなど、さまざまなスプレッドシート形式のメタデータ署名をサポートしています。完全なリストについては、 [公式文書](https://docs。groupdocs.com/signature/net/).

### スプレッドシート内のメタデータ署名はユーザーに表示されますか?

メタデータ署名はスプレッドシートのコンテンツ自体には表示されませんが、Excelやその他の互換性のあるアプリケーションのドキュメントプロパティパネルから表示できます。

### メタデータを追加した後にスプレッドシートが改ざんされたかどうかをプログラムで検証できますか?

はい、GroupDocs.Signature は、メタデータの変更など、署名後にドキュメントが変更されたかどうかを検出するのに役立つ検証機能を提供します。

### メタデータを追加するとスプレッドシートの機能に影響しますか?

メタデータを追加してもファイルサイズへの影響は最小限で、スプレッドシートの機能にも影響はありません。計算、数式、その他のExcel機能に影響を与えることなく、ドキュメントのプロパティを拡張できる軽量な方法です。

### さらにリソースやサポートはどこで見つかりますか?

- [APIリファレンス](https://reference.groupdocs.com/signature/net/)
- [ダウンロード](https://releases.groupdocs.com/signature/net/)
- [例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [ドキュメント](https://docs.groupdocs.com/signature/net/)
- [製品ページ](https://products.groupdocs.com/signature/net/)
- [ブログ](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [サポートフォーラム](https://forum.groupdocs.com/c/signature/13)
- [一時ライセンス](https://purchase.groupdocs.com/temporary-license/)