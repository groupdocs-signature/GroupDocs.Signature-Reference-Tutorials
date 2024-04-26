---
title: GroupDocs.Signature を使用して QR コードでドキュメントに署名する
linktitle: QRコードで署名する
second_title: GroupDocs.Signature .NET API
description: GroupDocs.Signature for .NET を使用してドキュメントに QR コード署名を追加する方法を学びます。セキュリティと認証を簡単に強化できます。
type: docs
weight: 15
url: /ja/net/advanced-signature-techniques/sign-with-qr-code/
---
## 導入
このチュートリアルでは、GroupDocs.Signature for .NET を使用して、QR コードでドキュメントに署名するプロセスを説明します。 GroupDocs.Signature for .NET は、開発者がさまざまな種類の署名をプログラムでデジタル ドキュメントに追加できる強力な API です。 QR コードを使用してドキュメントに署名すると、ドキュメントに追加のセキュリティ層と認証層を提供できます。
## 前提条件
始める前に、次の前提条件がインストールされていることを確認してください。
1.  GroupDocs.Signature for .NET: ライブラリは次の場所からダウンロードできます。[Webサイト](https://releases.groupdocs.com/signature/net/).
2. 開発環境: マシン上に .NET 開発環境がセットアップされていることを確認します。
3. サンプルドキュメント: QR コードで署名するサンプルドキュメント (PDF など) を準備します。

## 必要な名前空間のインポート
コードに入る前に、必要な名前空間をインポートしましょう。
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## ステップ 1: ファイル パスを定義する
```csharp
string filePath = "sample.pdf";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "SignWithQRCode", fileName);
```
必ず交換してください`"Your Document Directory"`署名付き文書を保存するディレクトリへのパスを置き換えます。
## ステップ 2: 署名オブジェクトを初期化する
```csharp
using (Signature signature = new Signature(filePath))
{
    //署名用のコードはここに記入してください
}
```
初期化する`Signature`署名するドキュメントへのパスを持つオブジェクト。
## ステップ3: QRCodeSignOptionsを作成する
```csharp
QrCodeSignOptions options = new QrCodeSignOptions("JohnSmith")
{
    EncodeType = QrCodeTypes.QR,
    Left = 50,
    Top = 150,
    Width = 200,
    Height = 200
};
```
作成する`QrCodeSignOptions`QR コード署名に必要な設定を持つオブジェクト。エンコードするテキスト、位置、QR コードのサイズなどのパラメータをカスタマイズできます。
## ステップ 4: 文書に署名する
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
使用`Sign`方法の`Signature`指定されたオプションで文書に署名するためのオブジェクト。このメソッドは`SignResult`署名プロセスに関する情報を含むオブジェクト。
## ステップ5: 結果を表示する
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
署名プロセスが成功したことと、署名されたドキュメントが保存された場所を示すメッセージを表示します。

## 結論
このチュートリアルでは、GroupDocs.Signature for .NET を使用して QR コードでドキュメントに署名する方法を学習しました。これらの簡単な手順に従うことで、デジタル ドキュメントに QR コード署名を追加し、セキュリティと認証を強化できます。

## よくある質問
### QR コードの外観をカスタマイズできますか?
はい、要件に応じて QR コードのサイズ、位置、エンコード タイプなどのさまざまなパラメータをカスタマイズできます。
### QR コードを使用した署名ではどの文書形式がサポートされていますか?
GroupDocs.Signature for .NET は、PDF、Word、Excel、PowerPoint などを含む幅広いドキュメント形式をサポートしています。
### バッチ処理で複数の文書に署名することは可能ですか?
もちろん、GroupDocs.Signature for .NET を使用すると、複数のドキュメントに同時に署名でき、ワークフローを合理化できます。
### QR コードで署名された文書の信頼性を検証できますか?
はい、GroupDocs.Signature for .NET は、署名されたドキュメントの整合性と信頼性を保証するための検証メカニズムを提供します。
### 購入前に機能をテストできる試用版はありますか?
はい、無料試用版を次のサイトからダウンロードできます。[Webサイト](https://releases.groupdocs.com/) GroupDocs.Signature for .NET の機能を評価します。