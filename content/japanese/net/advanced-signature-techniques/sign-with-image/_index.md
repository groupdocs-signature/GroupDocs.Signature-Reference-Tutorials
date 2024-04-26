---
title: GroupDocs.Signature を使用した画像付きドキュメントへの署名
linktitle: 画像による署名
second_title: GroupDocs.Signature .NET API
description: Groupdocs.Signature for .NET を使用して、.NET アプリケーションで画像を使用してドキュメントに署名する方法を学びます。ドキュメントのセキュリティと信頼性を簡単に強化します。
type: docs
weight: 13
url: /ja/net/advanced-signature-techniques/sign-with-image/
---
## 導入
このチュートリアルでは、Groupdocs.Signature for .NET を使用して画像を使用してドキュメントに署名する方法を説明します。ドキュメントに署名すると、ファイルの信頼性とセキュリティがさらに強化され、改ざん防止と法的拘束力が強化されます。 Groupdocs.Signature for .NET を利用すると、ドキュメント署名機能を .NET アプリケーションにシームレスに統合できます。
## 前提条件
チュートリアルに入る前に、次の前提条件を満たしていることを確認してください。
1.  Groupdocs.Signature for .NET: 開発環境に Groupdocs.Signature for .NET がインストールされていることを確認します。からダウンロードできます。[Webサイト](https://releases.groupdocs.com/signature/net/).
2. .NET 開発環境: マシン上に動作する .NET 開発環境がセットアップされていることを確認してください。

## 名前空間のインポート
コーディング部分を開始する前に、必要なクラスとメソッドにアクセスするために必要な名前空間をインポートします。
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## ステップ 1: ドキュメントをロードする
最初のステップは、署名する文書をロードすることです。署名するドキュメントのファイル パスを指定します。
```csharp
string filePath = "sample.pdf";
```
## ステップ 2: 署名画像を指定する
次に、署名に使用する署名画像へのパスを指定します。
```csharp
string imagePath = "signature_handwrite.jpg";
```
## ステップ 3: 出力ファイルのパスを設定する
署名されたドキュメントを保存するパスを定義します。
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithImage", fileName);
```
## ステップ 4: 署名オブジェクトを初期化する
ドキュメント ファイルのパスを渡して、Signature オブジェクトを初期化します。
```csharp
using (Signature signature = new Signature(filePath))
```
## ステップ 5: イメージ署名オプションを設定する
署名の位置、すべてのページに署名するかどうかなど、画像署名のオプションを設定します。
```csharp
ImageSignOptions options = new ImageSignOptions(imagePath)
{
    Left = 50,
    Top = 50,
    AllPages = true
};
```
## ステップ6: 文書に署名する
指定された画像とオプションを使用してドキュメントに署名します。
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
## ステップ 7: 結果の表示
最後に、署名プロセスの成功と署名されたドキュメントの場所を示す結果を表示します。
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## 結論
このチュートリアルでは、Groupdocs.Signature for .NET を使用して .NET アプリケーションで画像を使用してドキュメントに署名する方法を学習しました。ドキュメントの署名はドキュメント管理の重要な側面であり、ファイルの信頼性とセキュリティを提供します。
## よくある質問
### 1 つの文書内で複数の署名画像を使用できますか?
はい、Groupdocs.Signature for .NET を使用して、複数のイメージを含むドキュメントに署名できます。画像ごとに署名プロセスを繰り返すだけです。
### Groupdocs.Signature for .NET はあらゆる種類のドキュメントと互換性がありますか?
Groupdocs.Signature for .NET は、PDF、Word、Excel などを含む幅広いドキュメント形式をサポートしています。
### 署名の外観をカスタマイズできますか?
はい、サイズ、位置、透明度など、署名の外観のさまざまな側面をカスタマイズできます。
### テスト用に利用できる試用版はありますか?
はい、Web サイトから無料試用版をダウンロードして、購入前に機能をテストできます。
### Groupdocs.Signature for .NET のテクニカル サポートを受けるにはどうすればよいですか?
 Groupdocs.Signature フォーラムにアクセスすると、技術サポートを受けることができます。[ここ](https://forum.groupdocs.com/c/signature/13).