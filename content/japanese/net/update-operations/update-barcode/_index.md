---
"description": "GroupDocs.Signature for .NET を使用して、複数のドキュメント形式のバーコード署名をプログラムで更新する方法を学びます。ドキュメント管理ソリューションを構築する開発者向けの包括的なチュートリアルです。"
"linktitle": "バーコードを更新"
"second_title": "GroupDocs.Signature .NET API"
"title": "ドキュメント内のバーコード署名を更新する"
"url": "/ja/net/update-operations/update-barcode/"
"weight": 10
type: docs
---
## 導入
バーコード署名は、デジタルドキュメントワークフローにおいて構造化データをエンコードするために広く利用されており、効率的な追跡、識別、検証を可能にします。GroupDocs.Signature for .NETは、ドキュメント内の既存のバーコード署名を更新する機能など、高度な署名機能をアプリケーションに統合できる包括的なドキュメント署名ソリューションです。

このチュートリアルでは、GroupDocs.Signature for .NET を使用してドキュメント内のバーコード署名を更新する方法に焦点を当てています。既存のバーコードの位置、サイズ、エンコードされたデータなどを変更する必要がある場合でも、このガイドでは、わかりやすいコード例と解説を用いて手順を順を追って説明します。

## 前提条件
GroupDocs.Signature for .NET を使用してバーコード署名の更新を実装する前に、次の前提条件が満たされていることを確認してください。

1. 開発環境: Visual Studio 2017 以降などの動作する .NET 開発環境。
2. GroupDocs.Signature ライブラリ: GroupDocs.Signature for .NET ライブラリは、次の場所からダウンロードできます。 [ダウンロードページ](https://releases。groupdocs.com/signature/net/).
3. 基本的な C# の知識: C# プログラミングの概念に関する知識。
4. サンプル ドキュメント: 更新するバーコード署名を含むドキュメント。

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

ここで、バーコード署名を更新するプロセスを管理しやすいステップに分解してみましょう。

## ステップ1: ドキュメントパスを設定する
まず、ソース ドキュメントのパスと更新されたドキュメントを保存する場所を定義します。

```csharp
// バーコード署名付きのソース文書へのパス
string filePath = "sample_multiple_signatures.docx";

// 出力ファイル名を取得する
string fileName = Path.GetFileName(filePath);

// 出力ディレクトリとファイルパスを定義する
string outputDirectory = Path.Combine("Your Document Directory", "UpdateBarcode");
string outputFilePath = Path.Combine(outputDirectory, fileName);

// 出力ディレクトリが存在することを確認する
Directory.CreateDirectory(outputDirectory);
```

## ステップ2: ソースドキュメントをコピーする
更新操作によってドキュメントが直接変更されるため、元のドキュメントのコピーを作成して保存します。

```csharp
// 元の文書のコピーを作成する
File.Copy(filePath, outputFilePath, true);
```

## ステップ3: 署名インスタンスを初期化する
インスタンスを作成する `Signature` ドキュメントを操作するクラス:

```csharp
// 出力ファイルパスでSignatureインスタンスを初期化します
using (Signature signature = new Signature(outputFilePath))
{
    // 署名操作はここで実行されます
}
```

## ステップ4: バーコード検索オプションを設定する
ドキュメント内の既存のバーコード署名を見つけるための検索オプションを設定します。

```csharp
// バーコード署名の検索オプションを設定する
BarcodeSearchOptions options = new BarcodeSearchOptions()
{
    // テキストコンテンツでフィルタリングできます
    Text = "12345",
    MatchType = TextMatchType.Contains
    
    // すべてのページを検索するにはコメントを解除してください
    // AllPages = true
};
```

## ステップ5: バーコード署名を検索する
構成された検索オプションを使用して、ドキュメント内のバーコード署名を検索します。

```csharp
// バーコード署名を検索する
List<BarcodeSignature> signatures = signature.Search<BarcodeSignature>(options);
```

## ステップ6: バーコード署名プロパティを更新する
バーコード署名が見つかった場合は、必要に応じてそのプロパティを更新します。

```csharp
// 署名が見つかったかどうかを確認する
if (signatures.Count > 0)
{
    // 最初のバーコード署名を取得する
    BarcodeSignature barcodeSignature = signatures[0];
    
    // 位置を更新
    barcodeSignature.Left = 100;
    barcodeSignature.Top = 100;
    
    // 更新サイズ
    barcodeSignature.Width = 400;
    barcodeSignature.Height = 100;
    
    // アップデートを適用する
    bool result = signature.Update(barcodeSignature);
    
    // 結果を確認する
    if (result)
    {
        Console.WriteLine($"Signature with Barcode '{barcodeSignature.Text}' and encode type '{barcodeSignature.EncodeType.TypeName}' was updated in the document ['{fileName}'].");
    }
    else
    {
        Console.WriteLine($"Signature was not updated in the document! Signature with Barcode '{barcodeSignature.Text}' and encode type '{barcodeSignature.EncodeType.TypeName}' was not found!");
    }
}
else
{
    Console.WriteLine("No barcode signatures found in the document.");
}
```

## 完全な例
以下は、ドキュメント内のバーコード署名を更新する方法を示した完全な機能例です。

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace UpdateBarcodeSignatureExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // ドキュメントパス
            string filePath = "sample_multiple_signatures.docx";
            
            // 出力パスを定義する
            string fileName = Path.GetFileName(filePath);
            string outputDirectory = Path.Combine(Environment.CurrentDirectory, "UpdateBarcode");
            string outputFilePath = Path.Combine(outputDirectory, fileName);
            
            // 出力ディレクトリが存在することを確認する
            Directory.CreateDirectory(outputDirectory);
            
            // 元の文書のコピーを作成する
            File.Copy(filePath, outputFilePath, true);
            
            // 署名インスタンスを初期化する
            using (Signature signature = new Signature(outputFilePath))
            {
                // 検索オプションを設定する
                BarcodeSearchOptions options = new BarcodeSearchOptions
                {
                    Text = "12345",
                    MatchType = TextMatchType.Contains
                };
                
                // バーコード署名を検索する
                List<BarcodeSignature> signatures = signature.Search<BarcodeSignature>(options);
                
                // 署名が見つかったかどうかを確認する
                if (signatures.Count > 0)
                {
                    // 最初の署名を取得する
                    BarcodeSignature barcodeSignature = signatures[0];
                    
                    // 位置とサイズを更新する
                    barcodeSignature.Left = 100;
                    barcodeSignature.Top = 100;
                    barcodeSignature.Width = 400;
                    barcodeSignature.Height = 100;
                    
                    // アップデートを適用する
                    bool result = signature.Update(barcodeSignature);
                    
                    // 結果を確認する
                    if (result)
                    {
                        Console.WriteLine($"Barcode signature was successfully updated in document '{fileName}'.");
                        Console.WriteLine($"Barcode text: {barcodeSignature.Text}");
                        Console.WriteLine($"Encode type: {barcodeSignature.EncodeType.TypeName}");
                        Console.WriteLine($"New position: {barcodeSignature.Left}x{barcodeSignature.Top}");
                        Console.WriteLine($"New size: {barcodeSignature.Width}x{barcodeSignature.Height}");
                        Console.WriteLine($"Output file path: {outputFilePath}");
                    }
                    else
                    {
                        Console.WriteLine("Failed to update barcode signature!");
                    }
                }
                else
                {
                    Console.WriteLine("No barcode signatures found in the document.");
                }
            }
            
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## 高度なバーコード署名のカスタマイズ
GroupDocs.Signature には、基本的な位置とサイズ以外にも、バーコード署名をカスタマイズするための追加オプションが用意されています。

### 外観プロパティの調整
バーコードの視覚的な側面をカスタマイズします。

```csharp
// 前景色（バーコードの色）を設定する
barcodeSignature.ForeColor = System.Drawing.Color.Blue;

// 背景色を設定する
barcodeSignature.BackgroundColor = System.Drawing.Color.LightYellow;

// 透明度を調整する
barcodeSignature.Opacity = 0.8;
```

### 境界線を追加する
カスタムの境界線でバーコードを強調します。

```csharp
barcodeSignature.Border.Color = System.Drawing.Color.Red;
barcodeSignature.Border.DashStyle = System.Drawing.Drawing2D.DashStyle.Dash;
barcodeSignature.Border.Weight = 2;
barcodeSignature.Border.Visible = true;
```

### バーコードを回転させる
バーコード署名を特定の角度に回転させます。

```csharp
barcodeSignature.Angle = 30; // 30度回転
```

## 結論
GroupDocs.Signature for .NETは、ドキュメント内のバーコード署名を更新するための強力で柔軟なソリューションを提供します。このチュートリアルで説明する手順に従うことで、開発者は.NETアプリケーションにバーコード署名更新機能を効率的に実装し、ドキュメント管理と自動化機能を強化することができます。

GroupDocs.Signature は包括的な機能セットと直感的な API を備えており、開発者はドキュメントの整合性とアクセシビリティを確保しながら、最新のビジネス アプリケーションの要件を満たす高度なドキュメント署名ソリューションを構築できます。

## よくある質問
### つのドキュメント内で複数のバーコード署名を更新できますか?
はい、GroupDocs.Signature では、同じドキュメント内の複数のバーコード署名を更新できます。署名を検索した後、結果リストを反復処理して、各バーコード署名を個別に更新できます。

### GroupDocs.Signature はさまざまなバーコード形式をサポートしていますか?
はい、GroupDocs.Signature は、線形バーコード (コード 128、コード 39、EAN、UPC など) や 2D バーコード (QR コード、データ マトリックス、PDF417 など) を含む、さまざまなバーコード形式をサポートしています。

### GroupDocs.Signature for .NET の試用版はありますか?
はい、無料試用版をこちらからダウンロードできます。 [GroupDocsウェブサイト](https://releases.groupdocs.com/signature/net/) 購入する前にライブラリの機能を評価します。

### 更新時にバーコードの種類を別の種類に変換できますか?
アップデート中は、バーコードの種類を直接変換することはできません。ただし、既存のバーコードを削除し、希望する形式の新しいバーコードを追加することで、変換が可能です。

### バーコードを更新するとスキャン機能に影響しますか?
GroupDocs.Signature は、バーコードのサイズや位置などのプロパティを更新する際に、バーコードのスキャンの整合性を維持します。ただし、バーコードのサイズが極端に小さい場合や、回転角度が大きい場合、一部のリーダーではスキャンのパフォーマンスに影響が出る可能性があります。

### GroupDocs.Signature for .NET の追加サポートはどこで入手できますか?
以下のリソースを通じて包括的なサポートを受けることができます。
- [APIドキュメント](https://docs.groupdocs.com/signature/net/)
- [APIリファレンス](https://reference.groupdocs.com/signature/net/)
- [GitHubの例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [サポートフォーラム](https://forum.groupdocs.com/c/signature/13)
- [ブログ](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [無料サポート](https://forum.groupdocs.com/c/signature)
- [一時ライセンス](https://purchase.groupdocs.com/temporary-license/)