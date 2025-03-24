---
title: 画像署名の削除
linktitle: 画像署名の削除
second_title: GroupDocs.Signature .NET API
description: GroupDocs.Signature for .NET を使用してドキュメントからイメージ署名を削除する方法を学習します。効率的な署名管理については、ステップバイステップのガイドに従ってください。
weight: 14
url: /ja/net/delete-operations/delete-image-signature/
---
## 導入
このチュートリアルでは、GroupDocs.Signature for .NET を使用してドキュメントからイメージ署名を削除する方法を説明します。 GroupDocs.Signature は、開発者がさまざまなドキュメント形式内のデジタル署名、スタンプ、フォーム フィールドを操作できるようにする強力なライブラリです。
## 前提条件
始める前に、以下のものがあることを確認してください。
### 1. .NET 用の GroupDocs.Signature
 GroupDocs.Signature for .NET を次の場所からダウンロードしてインストールします。[Webサイト](https://releases.groupdocs.com/signature/net/)。ドキュメントに記載されているインストール手順に従ってください。
### 2..NETフレームワーク
マシンに .NET Framework がインストールされていることを確認してください。
## 名前空間のインポート
必要な名前空間をプロジェクトに含めます。
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
イメージ署名を削除するプロセスを複数のステップに分けてみましょう。
## ステップ 1: ファイル パスを定義する
まず、署名を削除した後の入力ドキュメントと出力ドキュメントのパスを指定します。
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteImage", fileName);
```
## ステップ 2: ソース ファイルをコピーする
以来、`Delete`このメソッドは同じドキュメントで機能するため、ソース ファイルを別の場所にコピーすることが重要です。
```csharp
File.Copy(filePath, outputFilePath, true);
```
## ステップ3: 署名オブジェクトの初期化
インスタンスを作成する`Signature`クラスを作成し、出力ドキュメントへのパスを指定します。
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    //ここにコードが入ります
}
```
## ステップ 4: 画像署名を検索する
検索オプションを定義し、ドキュメント内の画像署名を検索します。
```csharp
ImageSearchOptions options = new ImageSearchOptions();
List<ImageSignature> signatures = signature.Search<ImageSignature>(options);
```
## ステップ 5: 画像署名を削除する
イメージ署名が見つかった場合は、最初の署名を削除します。
```csharp
if (signatures.Count > 0)
{
    ImageSignature imageSignature = signatures[0];
    bool result = signature.Delete(imageSignature);
    if (result)
    {
        Console.WriteLine($"Image signature at location {imageSignature.Left}x{imageSignature.Top} and Size {imageSignature.Size} was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature at location {imageSignature.Left}x{imageSignature.Top} and Size {imageSignature.Size} was not found!");
    }
}
```
## 結論
このチュートリアルでは、GroupDocs.Signature for .NET を使用してドキュメントからイメージ署名を削除する方法を学びました。段階的なガイドに従うことで、開発者はアプリケーション内でデジタル署名を効率的に管理できます。
## よくある質問
### 文書から複数の画像署名を削除できますか?
はい、コードを変更して、`signatures`リスト。
### GroupDocs.Signature は DOCX 以外のドキュメント形式をサポートしていますか?
はい。GroupDocs.Signature は、PDF、PPT、XLS などを含む幅広いドキュメント形式をサポートしています。
### GroupDocs.Signature for .NET の試用版はありますか?
はい、無料試用版を次のサイトからダウンロードできます。[Webサイト](https://releases.groupdocs.com/).
### GroupDocs.Signature のサポートを受けるにはどうすればよいですか?
を訪問できます。[GroupDocs.Signature フォーラム](https://forum.groupdocs.com/c/signature/13)援助とサポートのために。
### GroupDocs.Signature の一時ライセンスを購入できますか?
はい、次から一時ライセンスを購入できます。[購入ページ](https://purchase.groupdocs.com/temporary-license/).