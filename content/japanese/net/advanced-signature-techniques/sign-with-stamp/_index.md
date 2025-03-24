---
title: GroupDocs.Signature を使用したスタンプによる署名
linktitle: スタンプで署名する
second_title: GroupDocs.Signature .NET API
description: GroupDocs.Signature for .NET を使用して、.NET ドキュメントにスタンプ署名を簡単に追加する方法を学びます。ドキュメントのセキュリティを強化します。
weight: 16
url: /ja/net/advanced-signature-techniques/sign-with-stamp/
---

# GroupDocs.Signature を使用したスタンプによる署名

## 導入
このチュートリアルでは、GroupDocs.Signature for .NET を使用してスタンプでドキュメントに署名するプロセスを説明します。これらの段階的な手順に従うことで、書類にスタンプ署名を簡単に追加できるようになります。
## 前提条件
始める前に、次の前提条件を満たしていることを確認してください。
1.  GroupDocs.Signature for .NET SDK: SDK を次の場所からダウンロードしてインストールします。[Webサイト](https://releases.groupdocs.com/signature/net/).
2. 開発環境: .NET 開発に適切な開発環境がセットアップされていることを確認してください。
3. 署名する文書: スタンプを押して署名する文書 (PDF など) を準備します。

## 名前空間のインポート
まず、必要な名前空間をプロジェクトにインポートします。
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## ステップ 1: ドキュメントをロードする
```csharp
string filePath = "sample.pdf";
using (Signature signature = new Signature(filePath))
{
    //コードはここに入力します
}
```
## ステップ 2: スタンプ署名オプションを設定する
```csharp
StampSignOptions options = new StampSignOptions()
{
    Left = 50,
    Top = 150,                    
    Width = 200,
    Height = 200
};
```
## ステップ 3: スタンプの外観を構成する
```csharp
StampLine outerLine = new StampLine();
outerLine.Text = " * European Union ";
outerLine.TextRepeatType = StampTextRepeatType.FullTextRepeat;
outerLine.Font.Size = 12;
outerLine.Height = 22;
outerLine.TextBottomIntent = 6;
outerLine.TextColor = Color.WhiteSmoke;
outerLine.BackgroundColor = Color.DarkSlateBlue;
options.OuterLines.Add(outerLine);
StampLine innerLine = new StampLine();
innerLine.Text = "John Smith";
innerLine.TextColor = Color.MediumVioletRed;
innerLine.Font.Size = 20;
innerLine.Font.Bold = true;
innerLine.Height = 40;
options.InnerLines.Add(innerLine);
```
## ステップ 4: 文書に署名する
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithStamp", fileName);
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## 結論
このチュートリアルで示すように、GroupDocs.Signature for .NET を使用してドキュメントにスタンプ署名を追加するのは簡単なプロセスです。提供されている手順を使用すると、ドキュメントのセキュリティと信頼性を簡単に強化できます。
## よくある質問
### スタンプの署名の外観をカスタマイズできますか?
はい、要件に応じてスタンプ署名のテキスト、フォント、色、位置などのさまざまな側面をカスタマイズできます。
### GroupDocs.Signature は複数のドキュメント形式の署名をサポートしていますか?
はい。GroupDocs.Signature は、PDF、Microsoft Word、Excel、PowerPoint などを含む幅広いドキュメント形式をサポートしています。
### GroupDocs.Signature の試用版はありますか?
はい、無料試用版には次からアクセスできます。[Webサイト](https://releases.groupdocs.com/).
### 1 つの文書に複数の署名を追加できますか?
もちろん、GroupDocs.Signature を使用すると、スタンプ、テキスト、画像、デジタル署名などの複数の署名を 1 つのドキュメントに追加できます。
### 実装中に問題が発生した場合、どこでサポートを受けることができますか?
 GroupDocs.Signatureコミュニティフォーラムからサポートと支援を受けることができます[ここ](https://forum.groupdocs.com/c/signature/13).