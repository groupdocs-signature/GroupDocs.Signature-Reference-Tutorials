---
title: 複数のオプションを使用した署名
linktitle: 複数のオプションを使用した署名
second_title: GroupDocs.Signature .NET API
description: GroupDocs.Signature for .NET を使用して、複数のオプションでドキュメントに署名する方法を学びます。テキスト、バーコード、QR コード、デジタル、画像を使用してドキュメントのセキュリティを強化します。
type: docs
weight: 14
url: /ja/net/advanced-signature-techniques/sign-with-multiple-options/
---
## 導入
このチュートリアルでは、.NET 用の GroupDocs.Signature ライブラリを使用して、複数の署名オプションを使用してドキュメントに署名する方法を説明します。テキスト、バーコード、QR コード、デジタル、画像、メタデータ署名などのさまざまなオプションを使用してドキュメントに署名すると、汎用性が高まり、ドキュメントのセキュリティが強化されます。
## 前提条件
始める前に、次の前提条件を満たしていることを確認してください。
1.  GroupDocs.Signature for .NET ライブラリ: GroupDocs.Signature for .NET ライブラリを次からダウンロードしてインストールします。[ここ](https://releases.groupdocs.com/signature/net/).
2. 開発環境: .NET Framework がインストールされた開発環境をセットアップします。
3. 署名する文書: 署名する文書 (sample.docx など) を準備します。
4. 証明書とイメージ: デジタル署名とイメージ署名に必要な証明書とイメージを準備します。

## 名前空間のインポート
まず、.NET アプリケーションで GroupDocs.Signature ライブラリを使用するために必要な名前空間をインポートします。
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## ステップ 1: ドキュメントをロードする
```csharp
string filePath = "sample.docx";
string outputFilePath = Path.Combine("Your Document Directory", "SignWithMultiple", "SignWithMultiple.docx");
using (Signature signature = new Signature(filePath))
{
    //コードは続きます...
}
```
## ステップ 2: 署名オプションを定義する
テキスト、バーコード、QR コード、デジタル、画像、メタデータ署名など、さまざまなタイプと設定のいくつかの署名オプションを定義します。
```csharp
TextSignOptions textOptions = new TextSignOptions("Text signature")
{
    VerticalAlignment = VerticalAlignment.Top,
    HorizontalAlignment = HorizontalAlignment.Left
};
BarcodeSignOptions barcodeOptions = new BarcodeSignOptions("123456")
{
    EncodeType = BarcodeTypes.Code128,
    Left = 0,
    Top = 150,
    Height = 50,
    Width = 200
};
//他の署名オプション (QR コード、デジタル、画像、メタデータなど) を定義します...
```
## ステップ 3: 署名オプションのリストを作成する
以前に定義したすべてのオプションを含む署名オプションのリストを定義します。
```csharp
List<SignOptions> listOptions = new List<SignOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
//他の署名オプションをリストに追加します...
```
## ステップ 4: 文書に署名する
署名オプションのリストを使用してドキュメントに署名し、署名されたドキュメントを保存します。
```csharp
SignResult result = signature.Sign(outputFilePath, listOptions);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## 結論
GroupDocs.Signature for .NET を使用して複数のオプションでドキュメントに署名すると、ドキュメントのセキュリティと汎用性を強化するための堅牢なソリューションが提供されます。このチュートリアルで概説されている手順に従うことで、さまざまな署名タイプを .NET アプリケーションにシームレスに統合できます。
## よくある質問
### デジタル署名にカスタム イメージを使用できますか?
はい、GroupDocs.Signature ライブラリを使用して、デジタル署名のカスタム イメージを指定できます。
### GroupDocs.Signature はさまざまなドキュメント形式と互換性がありますか?
はい、GroupDocs.Signature は、DOCX、PDF、PPTX など、さまざまなドキュメント形式をサポートしています。
### テキスト署名の外観をカスタマイズできますか?
もちろん、フォント サイズ、色、スタイルなど、テキスト署名の外観をカスタマイズできます。
### GroupDocs.Signature はデジタル署名の暗号化を提供しますか?
はい、GroupDocs.Signature は、ドキュメントのセキュリティを確保するためにデジタル署名の暗号化オプションを提供します。
### GroupDocs.Signature for .NET の試用版はありますか?
はい、GroupDocs.Signature for .NET の無料試用版を次からダウンロードできます。[ここ](https://releases.groupdocs.com/).