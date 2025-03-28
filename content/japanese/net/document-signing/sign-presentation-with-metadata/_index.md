---
title: メタデータを使用してプレゼンテーションに署名する
linktitle: メタデータを使用してプレゼンテーションに署名する
second_title: GroupDocs.Signature .NET API
description: GroupDocs.Signature for .NET を使用して、メタデータを含むプレゼンテーション ファイルに署名する方法を学びます。文書の整合性を強化し、貴重な情報を追加します。
weight: 12
url: /ja/net/document-signing/sign-presentation-with-metadata/
---

# メタデータを使用してプレゼンテーションに署名する

## 導入
このチュートリアルでは、GroupDocs.Signature for .NET ライブラリを使用して、メタデータでプレゼンテーション ファイル (PPTX) に署名する方法を学習します。メタデータでプレゼンテーションに署名すると、作成者の名前、作成日、ドキュメント ID、署名 ID、さまざまな数値などの貴重な情報がドキュメントに追加されます。
## 前提条件
始める前に、以下のものがあることを確認してください。
1.  GroupDocs.Signature for .NET Library: からライブラリをダウンロードしてインストールします。[ここ](https://releases.groupdocs.com/signature/net/).
2. 開発環境: .NET 開発環境が設定されていることを確認します。
3. プレゼンテーション ファイル: 署名用のサンプル プレゼンテーション ファイル (PPTX 形式) を用意します。
4. C# の基本的な理解: C# プログラミング言語に精通していると有利です。

## 名前空間のインポート
コードに入る前に、必要な名前空間をインポートしましょう。
```csharp
using System;
using System.IO;
    using GroupDocs.Signature;
    using GroupDocs.Signature.Domain;
    using GroupDocs.Signature.Options;
```
## ステップ1: プレゼンテーションファイルを読み込む
```csharp
string filePath = "sample.pptx";
```
交換する`"sample.pptx"`プレゼンテーション ファイルへのパスを入力します。
## ステップ 2: 出力ファイルのパスを指定する
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPresentationWithMetadata", "SignedWithMetadata.pptx");
```
署名されたプレゼンテーション ファイルを保存するディレクトリとファイル名を指定します。
## ステップ3: 署名オブジェクトの初期化
```csharp
using (Signature signature = new Signature(filePath))
```
プレゼンテーション ファイルへのパスを指定して、Signature オブジェクトを初期化します。
## ステップ4: メタデータ署名オプションを定義する
```csharp
MetadataSignOptions options = new MetadataSignOptions();
```
メタデータ署名オプションを定義するには、MetadataSignOptions のインスタンスを作成します。
## ステップ 5: メタデータ署名を作成する
```csharp
PresentationMetadataSignature[] signatures = new PresentationMetadataSignature[]
{
    new PresentationMetadataSignature("Author", "Mr.Scherlock Holmes"),
    new PresentationMetadataSignature("CreatedOn", DateTime.Now),
    new PresentationMetadataSignature("DocumentId", 123456),
    new PresentationMetadataSignature("SignatureId", 123.456D),
    new PresentationMetadataSignature("Amount", 123.456M),
    new PresentationMetadataSignature("Total", 123.456F)
};
```
それぞれがメタデータ署名を表す PresentationMetadataSignature オブジェクトの配列を作成します。文字列、DateTime、整数、double、10 進数、float など、さまざまなタイプのメタデータを追加できます。
## ステップ 6: オプションに署名を追加する
```csharp
options.Signatures.AddRange(signatures);
```
作成したメタデータ署名を MetadataSignOptions オブジェクトに追加します。
## ステップ 7: 文書に署名する
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
指定されたオプションを使用してメタデータを含むプレゼンテーション ファイルに署名し、署名されたファイルを出力パスに保存します。
## ステップ 8: 結果の表示
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
適用された署名の数と署名されたファイルが保存されるパスとともに成功メッセージを表示します。

## 結論
このチュートリアルでは、GroupDocs.Signature for .NET ライブラリを使用して、メタデータを含むプレゼンテーション ファイルに署名する方法を学習しました。メタデータ署名を追加すると、ドキュメントの整合性が強化され、そのコンテンツに関する貴重な情報が提供されます。

## よくある質問
### GroupDocs.Signature for .NET を使用して、メタデータを含む PPTX 以外の他のドキュメント形式に署名できますか?
はい。GroupDocs.Signature は、メタデータを使用した署名用に、Word、Excel、PDF などのさまざまなドキュメント形式をサポートしています。
### GroupDocs.Signature for .NET は .NET Core と互換性がありますか?
はい、このライブラリは .NET Framework と .NET Core の両方と互換性があります。
### メタデータ署名の外観をカスタマイズできますか?
はい、要件に応じてメタデータ署名の外観、位置、その他のプロパティをカスタマイズできます。
### GroupDocs.Signature for .NET は署名付きドキュメントの暗号化を提供しますか?
はい、GroupDocs.Signature は、署名されたドキュメントを不正アクセスから保護するための暗号化オプションを提供します。
### 購入前にテストできる試用版はありますか?
はい、次のサイトから GroupDocs.Signature for .NET の無料トライアルを利用できます。[ここ](https://releases.groupdocs.com/).