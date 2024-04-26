---
title: GroupDocs.Signature for .NET を使用してテキストで署名する
linktitle: テキストによる署名
second_title: GroupDocs.Signature .NET API
description: GroupDocs.Signature for .NET を使用してテキストでドキュメントに署名する方法を学びます。プログラムでテキスト署名を追加するためのステップバイステップ ガイド。
type: docs
weight: 17
url: /ja/net/advanced-signature-techniques/sign-with-text/
---
## 導入
デジタル時代では、文書に電子的に署名することが標準的な方法となり、時間とリソースを節約しています。GroupDocs.Signature for .NET は、さまざまな文書形式にプログラムでテキスト署名を追加するための包括的なソリューションを提供します。このチュートリアルでは、GroupDocs.Signature for .NET を使用して文書にテキストで署名するプロセスについて説明します。
## 前提条件
チュートリアルに進む前に、次の前提条件を満たしていることを確認してください。
1.  GroupDocs.Signature for .NET: GroupDocs.Signature for .NETライブラリがインストールされていることを確認してください。ダウンロードはここから行えます。[ここ](https://releases.groupdocs.com/signature/net/).
2. 開発環境: .NET 開発用に作業環境をセットアップします。
3. ドキュメント: テキストで署名するドキュメント (PDF、Word など) を準備します。

## 名前空間のインポート
まず、GroupDocs.Signature 機能を使用するには、必要な名前空間を .NET プロジェクトにインポートする必要があります。
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

テキストを使用して文書に署名するプロセスを複数のステップに分けてみましょう。
## ステップ 1: ドキュメントをロードする
テキストで署名したい文書を読み込みます。
```csharp
string filePath = "sample.pdf"; //ドキュメントへのパス
string fileName = Path.GetFileName(filePath);
```
## ステップ 2: 出力ファイルのパスを設定する
署名された文書が保存される出力ファイルのパスを定義します。
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithText", fileName);
```
## ステップ 3: 署名オプションを作成する
テキストの内容、位置、サイズ、色、フォントなどのテキスト署名のオプションを設定します。
```csharp
TextSignOptions options = new TextSignOptions("John Smith")
{
    Left = 50, //署名位置を設定する
    Top = 200,
    Width = 100, //署名の四角形を設定する
    Height = 30,
    ForeColor = Color.Red, //文字色の設定
    Font = new SignatureFont { Size = 14, FamilyName = "Comic Sans MS" } //フォントを設定する
};
```
## ステップ 4: 文書に署名する
GroupDocs.Signature を使用して、指定されたオプションでドキュメントに署名し、署名されたドキュメントを出力ファイル パスに保存します。
```csharp
using (Signature signature = new Signature(filePath))
{
    SignResult result = signature.Sign(outputFilePath, options); //文書に署名する
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## 結論
このチュートリアルでは、GroupDocs.Signature for .NET を使用してテキストでドキュメントに署名する方法を学習しました。これらの手順に従うことで、プログラムで文書にテキスト署名を効率的に追加し、セキュリティと信頼性を強化できます。
## よくある質問
### テキスト署名の外観をカスタマイズできますか?
はい、好みに応じてテキスト署名の色、フォント、サイズ、位置などのさまざまなパラメータをカスタマイズできます。
### GroupDocs.Signature は複数のドキュメント形式と互換性がありますか?
はい。GroupDocs.Signature は、PDF、Word、Excel、PowerPoint などを含むさまざまなドキュメント形式をサポートしています。
### 1 つの文書に複数のテキスト署名を追加できますか?
もちろん、複数のテキスト署名を文書に追加でき、それぞれに独自のカスタマイズ オプションのセットが付いています。
### GroupDocs.Signature は署名後のドキュメントの整合性を保証しますか?
はい。GroupDocs.Signature は、文書の整合性を確保し、署名後の改ざんを防ぐために堅牢な暗号化アルゴリズムを採用しています。
### 購入前にテストできる試用版はありますか?
はい、無料試用版を次からダウンロードできます。[ここ](https://releases.groupdocs.com/)購入する前に機能を調べてください。