---
"description": "GroupDocs.Signature for .NET を使用して、さまざまなドキュメント形式のテキスト署名を効率的に更新する方法を学びます。この包括的なチュートリアルで、ドキュメント認証をマスターしましょう。"
"linktitle": "テキストを更新"
"second_title": "GroupDocs.Signature .NET API"
"title": "ドキュメント内のテキスト署名を更新する"
"url": "/ja/net/update-operations/update-text/"
"weight": 13
---

## 導入
GroupDocs.Signature for .NETは、開発者が強力な署名機能を.NETアプリケーションに統合できるようにする包括的なドキュメント署名ソリューションです。この多用途ライブラリを使えば、様々なドキュメント形式（テキスト署名を含む）の署名を簡単に追加、検索、検証、更新できます。このチュートリアルでは、ドキュメント内のテキスト署名の更新に特に焦点を当て、シームレスな実装のためのステップバイステップのガイダンスを提供します。

## 前提条件
GroupDocs.Signature for .NET を使用してテキスト署名を更新する前に、次の前提条件が満たされていることを確認してください。

1. Visual Studio: システムに最新バージョンの Visual Studio IDE をインストールします。
2. GroupDocs.Signature for .NET: GroupDocs.Signature for .NETライブラリを以下のサイトからダウンロードしてインストールします。 [ダウンロードページ](https://releases。groupdocs.com/signature/net/).
3. .NET Framework または .NET Core: 開発マシンに .NET Framework または .NET Core のいずれかがインストールされていることを確認します。
4. 基本的な C# の知識: C# プログラミングの基礎を熟知していること。

## 名前空間のインポート
ドキュメント内のテキスト署名を更新する前に、必要な名前空間をプロジェクトにインポートする必要があります。これらの名前空間は、GroupDocs.Signature のクラスとメソッドへのアクセスを提供します。

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## ステップ1: ドキュメントパスを設定する
まず、更新するテキスト署名が含まれているドキュメントへのパスを確立します。

```csharp
string filePath = "sample_multiple_signatures.docx";
```

この行はソースドキュメントへのパスを指定します。 `"sample_multiple_signatures.docx"` ドキュメントへの実際のパスを入力します。

## ステップ2: ドキュメントのコピー
以来、 `Update` この方法は同じ文書で機能しますが、元の文書のバックアップ コピーを作成することをお勧めします。

```csharp
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "UpdateText", fileName);
File.Copy(filePath, outputFilePath, true);
```

このコードスニペットは、指定されたディレクトリにソースドキュメントのコピーを作成します。 `"Your Document Directory"` 更新されたドキュメントを保存する実際のパスを入力します。

## ステップ3: 署名オブジェクトの初期化
さて、初期化します `Signature` ドキュメントのコピーへのパスを持つオブジェクト。

```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // ここにあなたのコード
}
```

その `Signature` クラスはGroupDocs.Signature機能へのメインエントリポイントです。 `using` この声明により、リソースが使用後に適切に廃棄されることが保証されます。

## ステップ4: テキスト署名を検索する
テキスト署名を更新する前に、ドキュメント内でその署名を見つける必要があります。

```csharp
TextSearchOptions options = new TextSearchOptions();
List<TextSignature> signatures = signature.Search<TextSignature>(options);
```

このコードは、デフォルトの検索オプションを使用して文書内のすべてのテキスト署名を検索します。検索をカスタマイズするには、追加のプロパティを設定します。 `TextSearchOptions` クラス。

## ステップ5: テキスト署名を更新する
テキスト署名が見つかったら、そのうちの 1 つを選択してそのプロパティを更新できます。

```csharp
if (signatures.Count > 0)
{
    TextSignature textSignature = signatures[0];
    textSignature.Text = "John Walkman";
    textSignature.Left = textSignature.Left + 10;
    textSignature.Top = textSignature.Top + 10;
    textSignature.Width = 200;
    textSignature.Height = 100;
    bool result = signature.Update(textSignature);
    if (result)
    {
        Console.WriteLine($"Signature with Text '{textSignature.Text}' was updated in the document ['{fileName}'].");
    }
    else
    {
        Console.WriteLine($"Signature was not updated in the document! Signature with Text '{textSignature.Text}' was not found!");
    }
}
```

このコード:
1. テキスト署名が見つかったかどうかを確認します
2. リストから最初の署名を取得します
3. テキストの内容、位置（左、上）、サイズ（幅、高さ）を変更します
4. 呼び出し `Update` 変更を適用する方法
5. 結果に基づいて成功または失敗のメッセージを表示します

## 完全な例
ドキュメント内のテキスト署名を更新する方法を示した完全な例を次に示します。

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace UpdateTextSignature
{
    class Program
    {
        static void Main(string[] args)
        {
            // ドキュメントパス
            string filePath = "sample_multiple_signatures.docx";
            
            // ドキュメントをコピー
            string fileName = Path.GetFileName(filePath);
            string outputFilePath = Path.Combine("OutputDirectory", "UpdateText", fileName);
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
            File.Copy(filePath, outputFilePath, true);
            
            // 署名オブジェクトを初期化する
            using (Signature signature = new Signature(outputFilePath))
            {
                // テキスト署名を検索する
                TextSearchOptions options = new TextSearchOptions();
                List<TextSignature> signatures = signature.Search<TextSignature>(options);
                
                // テキスト署名を更新する
                if (signatures.Count > 0)
                {
                    TextSignature textSignature = signatures[0];
                    textSignature.Text = "John Walkman";
                    textSignature.Left = textSignature.Left + 10;
                    textSignature.Top = textSignature.Top + 10;
                    textSignature.Width = 200;
                    textSignature.Height = 100;
                    
                    // 変更を適用する
                    bool result = signature.Update(textSignature);
                    
                    // 結果を確認する
                    if (result)
                    {
                        Console.WriteLine($"Signature with Text '{textSignature.Text}' was updated in the document ['{fileName}'].");
                    }
                    else
                    {
                        Console.WriteLine($"Signature was not updated in the document! Signature with Text '{textSignature.Text}' was not found!");
                    }
                }
                else
                {
                    Console.WriteLine("No text signatures found in the document.");
                }
            }
        }
    }
}
```

## 高度なテキスト署名のカスタマイズ
GroupDocs.Signatureは、テキスト署名の幅広いカスタマイズオプションを提供しています。以下のような様々なプロパティを変更できます。

- フォント: フォントファミリー、サイズ、スタイル、色を変更します
- 境界線: 境界線のスタイルと色を追加または変更します
- 背景: 背景色または透明度を設定します
- 回転: テキスト署名を特定の角度に回転します
- 透明度: 署名の不透明度を調整します

フォント プロパティをカスタマイズする方法の例を次に示します。

```csharp
textSignature.ForeColor = System.Drawing.Color.Blue;
textSignature.Font.FontFamily = "Arial";
textSignature.Font.FontSize = 16;
textSignature.Font.Bold = true;
textSignature.Font.Italic = true;
textSignature.Font.Underline = true;
```

## 結論
GroupDocs.Signature for .NETは、ドキュメント内のテキスト署名をプログラムで更新するための堅牢で柔軟なソリューションを提供します。このチュートリアルで説明する手順に従うことで、開発者はテキスト署名の更新機能を.NETアプリケーションに効率的に統合し、ドキュメント管理と認証プロセスを強化できます。

GroupDocs.Signature は包括的な機能セットとユーザーフレンドリーな API を備えており、開発者は現代のビジネス アプリケーションの要件を満たす高度なドキュメント署名ソリューションを構築できます。

## よくある質問
### つのドキュメント内の複数のテキスト署名を更新できますか?
はい、見つかった署名のリストを反復処理し、それぞれに必要な変更を個別に適用することで、複数のテキスト署名を更新できます。

### GroupDocs.Signature はテキスト以外の種類の署名もサポートしていますか?
はい、もちろんです！GroupDocs.Signatureは、画像、デジタル、バーコード、QRコード、スタンプなど、様々な種類の署名をサポートしています。署名の種類ごとに、作成、検索、更新のための独自のプロパティとメソッドが用意されています。

### GroupDocs.Signature for .NET の試用版はありますか?
はい、無料試用版は以下からダウンロードできます。 [ここ](https://releases.groupdocs.com/) 購入する前にライブラリの機能を評価します。

### テキスト署名の外観をカスタマイズできますか?
はい、GroupDocs.Signature では、フォント プロパティ (ファミリ、サイズ、スタイル)、色、境界線、背景、回転、透明度など、テキスト署名の広範なカスタマイズ オプションが提供されます。

### GroupDocs.Signature for .NET はすべてのドキュメント形式で動作しますか?
GroupDocs.Signatureは、PDF、Microsoft Office形式（Word、Excel、PowerPoint）、OpenDocument形式、画像など、幅広いドキュメント形式をサポートしています。完全なリストについては、 [ドキュメント](https://docs。groupdocs.com/signature/net/).

### GroupDocs.Signature のテクニカル サポートを受けるにはどうすればよいですか?
以下のチャネルを通じてテクニカル サポートを受けることができます。
- [フォーラム](https://forum.groupdocs.com/c/signature/13)
- [ドキュメント](https://docs.groupdocs.com/signature/net/)
- [APIリファレンス](https://reference.groupdocs.com/signature/net/)
- [GitHubの例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [ブログ](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)