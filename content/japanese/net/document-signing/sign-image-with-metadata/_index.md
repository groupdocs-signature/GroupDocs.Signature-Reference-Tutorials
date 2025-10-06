---
"description": "GroupDocs.Signature for .NET を使用して画像に署名し、メタデータを埋め込む方法を学びます。作成者情報、タイムスタンプ、カスタムデータを追加することで、画像の信頼性とトレーサビリティを強化します。"
"linktitle": "メタデータ付き署名画像"
"second_title": "GroupDocs.Signature .NET API"
"title": "C# .NET でメタデータを使用して画像に署名する"
"url": "/ja/net/document-signing/sign-image-with-metadata/"
"weight": 10
type: docs
---
## 導入

メタデータを用いたデジタル画像署名は、真正性、所有権、そしてトレーサビリティを確立するためにますます重要になっています。GroupDocs.Signature for .NETは、様々な画像形式にメタデータ署名を追加するための、強力かつ使いやすいソリューションを提供します。このチュートリアルでは、C#を用いてメタデータを用いた画像署名のプロセス全体を解説します。

メタデータ署名を使用すると、作成者情報、作成日時、一意の識別子など、貴重な情報を画像ファイルに直接埋め込むことができます。これらの情報は画像ファイル自体の一部となり、画像の真正性を追跡・検証するための信頼性の高い手段となります。

## 前提条件

このチュートリアルを進める前に、次のものを用意してください。

1. [.NET 用 GroupDocs.Signature](https://releases.groupdocs.com/signature/net/) - ライブラリをダウンロードしてインストールする
2. 開発環境 - Visual Studio または .NET をサポートする互換性のある IDE
3. 画像ファイル - サポートされている形式 (PNG、JPG、TIFF など) のサンプル画像ファイル
4. 基本的な C# プログラミング知識 - C# プログラミングの概念に関する知識

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

ソース イメージのパスと、署名された出力を保存する場所を定義します。

```csharp
// ソース画像ファイルへのパスを指定します
string filePath = "sample.png";

// 署名された画像の出力ディレクトリとファイル名を定義する
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignImageWithMetadata", "SignedWithMetadata.png");

// 出力ディレクトリが存在することを確認する
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## ステップ2: 署名オブジェクトの初期化

ソース イメージ ファイルを使用して Signature クラスのインスタンスを作成します。

```csharp
using (Signature signature = new Signature(filePath))
{
    // 残りのコードはここに記述します
}
```

## ステップ3: メタデータ署名の作成と構成

次に、画像に埋め込むメタデータを定義します。GroupDocs.Signature は、メタデータのさまざまなデータ型をサポートしています。

```csharp
// メタデータIDを初期化する（画像形式に固有）
ushort imgsMetadataId = 41996;

// メタデータ オプション オブジェクトを作成する
MetadataSignOptions options = new MetadataSignOptions();

// さまざまな種類のメタデータ署名を追加する
options
    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes"))  // 文字列値
    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // 日付時刻値
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // 整数値
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // 二重価値
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // 小数値
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // 浮動小数点値
```

## ステップ4: メタデータでイメージに署名する

メタデータ署名を画像に適用し、結果を保存します。

```csharp
// 文書に署名し、出力ファイルパスに保存します
SignResult result = signature.Sign(outputFilePath, options);

// 成功メッセージを表示する
Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed image saved at: {outputFilePath}");
```

## 完全な例

すべてのステップをまとめた完全なコード例を次に示します。

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignImageWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // ファイルパスを指定する
            string filePath = "sample.png";            
            string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
            
            // 出力ディレクトリが存在することを確認する
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // メタデータで画像に署名する
            using (Signature signature = new Signature(filePath))
            {
                // メタデータIDを初期化する（画像形式に固有）
                ushort imgsMetadataId = 41996;
                
                // メタデータオプションの作成
                MetadataSignOptions options = new MetadataSignOptions();
                
                // さまざまな種類のメタデータ署名を追加する
                options
                    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes")) // 文字列値
                    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // 日付時刻値
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // 整数値
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // 二重価値
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // 小数値
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // 浮動小数点値
                
                // 文書に署名してファイルに保存する
                SignResult result = signature.Sign(outputFilePath, options);
                
                // 結果を表示
                Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## 高度なメタデータ署名技術

### カスタムメタデータの操作

特定の ID を使用してカスタム メタデータ フィールドを作成することもできます。

```csharp
// 特定のIDでカスタムメタデータを作成する
options.Add(new ImageMetadataSignature(42000, "CustomValue"));
```

### メタデータ署名の検証

署名後、メタデータ署名を検証する必要がある場合があります。

```csharp
// 検証オプションを作成する
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// メタデータ署名を検索する
SearchResult result = signature.Search(searchOptions);

// 見つかった署名を表示する
Console.WriteLine($"Found {result.Signatures.Count} metadata signatures:");
foreach(var metadataSignature in result.Signatures)
{
    Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value}");
}
```

## 結論

このチュートリアルでは、GroupDocs.Signature for .NET を使用してメタデータで画像に署名する方法を学習しました。画像にメタデータを埋め込むことで、画像の信頼性を高め、重要な情報を追加し、ドキュメント管理ワークフローを改善する優れた方法となります。このプロセスはシンプルでありながら強力で、特定の要件に合わせてカスタマイズできます。

画像ファイルに埋め込まれたメタデータは、著作権保護、画像の出所追跡、説明情報の追加、デジタル管理の確立など、様々な目的に使用できます。メタデータ署名を実装することで、画像のライフサイクル全体を通して、その完全性と真正性を維持できます。

## よくある質問

### 既存の署名済みイメージにメタデータを追加できますか?

はい、すでにメタデータ署名が含まれている画像にメタデータを追加できます。既存のメタデータは保持され、それに応じて新しいメタデータが追加されます。

### メタデータ署名ではどの画像形式がサポートされていますか?

GroupDocs.Signature for .NETは、PNG、JPEG、TIFF、BMP、GIFなど、さまざまな画像形式のメタデータ署名をサポートしています。完全なリストについては、 [公式文書](https://docs。groupdocs.com/signature/net/).

### 画像のメタデータを暗号化することは可能ですか?

はい、GroupDocs.Signature には、セキュリティ強化のためにメタデータを暗号化するオプションが用意されています。ライブラリが提供する暗号化オプションを使用することで、機密性の高いメタデータ情報を保護できます。

### 署名された画像の信頼性をプログラムで検証できますか?

はい、もちろんです。GroupDocs.Signature の検証メソッドを使用して、メタデータ署名を検証し、署名された画像の信頼性を確認できます。

### メタデータを使用して画像に署名する場合、ファイル サイズの制限はありますか?

ライブラリ自体にはファイルサイズに関する特別な制限はありませんが、非常に大きなファイルはより多くの処理時間とメモリを必要とする可能性があります。非常に大きな画像を扱う場合は、システムリソースを考慮することをお勧めします。

### テスト目的で一時ライセンスを取得するにはどうすればよいですか?

あなたは [一時ライセンス](https://purchase.groupdocs.com/temporary-license/) 購入前に GroupDocs.Signature をテストできます。

### さらにリソースやサポートはどこで見つかりますか?

- [APIリファレンス](https://reference.groupdocs.com/signature/net/)
- [ダウンロード](https://releases.groupdocs.com/signature/net/)
- [例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [ドキュメント](https://docs.groupdocs.com/signature/net/)
- [製品ページ](https://products.groupdocs.com/signature/net/)
- [ブログ](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [サポートフォーラム](https://forum.groupdocs.com/c/signature/13)